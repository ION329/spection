# Especificación de Ingeniería

> 🤖 **Instrucción para la IA:** Este documento convierte la especificación de feature en contratos técnicos
> implementables. Lee docs/spec/features/[feature]-spec.md y docs/spec/architecture/architecture.md
> antes de completar esta plantilla. Cada decisión aquí debe ser trazable a la feature spec o a un ADR aceptado.
> Al terminar este documento, genera también docs/spec/tasks/[feature]-tasks.md.

## Contratos de API

> 🤖 **Instrucción para la IA:** Define el contrato completo de cada endpoint que esta feature expone.
> Usa exactamente el siguiente formato para cada uno. No omitas ningún campo.
>
> ---
> **[MÉTODO] /ruta/completa**
>
> Descripción: [qué hace este endpoint en una oración]
> Auth: [pública | Bearer token | rol requerido: ADMIN | OWNER]
>
> ```
> Cabeceras de Solicitud:
>   Authorization: Bearer <token>   ← obligatorio si Auth no es pública
>   Content-Type: application/json
>
> Cuerpo de Solicitud:
>   {
>     "campo": "tipo"   // descripción | requerido | validaciones aplicadas
>   }
>   (escribe "Sin cuerpo" si es GET o DELETE sin body)
>
> Respuesta 200 — [descripción del caso de éxito]:
>   {
>     "campo": "tipo"   // descripción
>   }
>
> Respuesta 201 — [si aplica para creación de recurso]
> Respuesta 400 — [condición exacta que lo produce]: { "error": "mensaje descriptivo" }
> Respuesta 401 — Token ausente o inválido: { "error": "no autenticado" }
> Respuesta 403 — Permisos insuficientes: { "error": "no autorizado" }
> Respuesta 404 — [recurso no encontrado, especifica cuál]: { "error": "mensaje descriptivo" }
> Respuesta 409 — [si aplica: conflicto, duplicado]: { "error": "mensaje descriptivo" }
> Respuesta 422 — [si aplica: datos semánticamente inválidos]: { "error": "mensaje descriptivo" }
> Respuesta 500 — Error interno inesperado: { "error": "error interno del servidor" }
> ```
> ---
>
> Reglas obligatorias:
> - Cada endpoint de la feature spec debe tener su contrato aquí. Si falta alguno, la spec está incompleta.
> - No uses "etc." en ningún campo. Si no sabes qué errores pueden ocurrir, analiza cada validación y cada dependencia.
> - Los mensajes de error deben ser descriptivos y consistentes entre endpoints.
> - Referencia las Reglas de Negocio (BR-NN) de la feature spec en los comentarios donde aplique.

## Esquema de Base de Datos

> 🤖 **Instrucción para la IA:** Define el esquema completo de base de datos para esta feature.
>
> **Regla crítica sobre tipos de datos:**
> Antes de escribir cualquier tipo, verifica el motor de base de datos aprobado en:
> - docs/spec/architecture/architecture.md → sección Stack Tecnológico
> - El ADR correspondiente en docs/spec/decisions/
>
> Usa ÚNICAMENTE los tipos nativos de ese motor. Ejemplos por motor:
> - PostgreSQL: uuid, text, varchar(N), integer, bigint, boolean, jsonb, timestamptz, date, numeric(p,s)
> - MySQL: CHAR(36), VARCHAR(N), INT, BIGINT, TINYINT(1), JSON, DATETIME, DECIMAL(p,s)
> - MongoDB: ObjectId, String, Number, Boolean, Date, Object, Array
> Nunca uses tipos genéricos como "string", "number", "boolean", "date" o "object".
>
> **Formato obligatorio para cada tabla o colección:**
>
> **Tabla: [nombre_tabla]**
> | Campo | Tipo | Restricciones | Descripción |
> |---|---|---|---|
> | id | uuid | PRIMARY KEY, NOT NULL | Identificador único |
> | [campo] | [tipo exacto del motor] | [NULL/NOT NULL, UNIQUE, DEFAULT valor, FK...] | [descripción funcional] |
> | created_at | timestamptz | NOT NULL, DEFAULT now() | Fecha de creación (con zona horaria) |
> | updated_at | timestamptz | NOT NULL | Fecha de última modificación |
>
> Índices (lista uno por línea, justifica cada uno):
> - idx_[tabla]_[campo] en ([campo]) — [motivo: mejora búsqueda por X, enforce unicidad, etc.]
>
> Relaciones (una por línea):
> - [tabla].[campo_fk] → [tabla_referenciada].[campo_pk] (ON DELETE [CASCADE | SET NULL | RESTRICT])
>
> Si la feature no requiere cambios de esquema (usa tablas ya existentes), documenta qué tablas usa y añade solo los índices nuevos necesarios.

## Gestión de Estado

> 🤖 **Instrucción para la IA:** Define el estado del lado del cliente para esta feature.
> Si la feature es solo de backend, escribe "N/A — feature de backend puro" y omite el resto.
>
> Para features con frontend, define:
>
> **Estado global (store):**
> ```
> {
>   [slice_nombre]: {
>     [campo]: tipo  // descripción y valor inicial
>   }
> }
> ```
>
> **Acciones / Mutations:**
> - [NOMBRE_ACCION]: qué hace, qué payload recibe, qué estado modifica
>
> **Estados derivados (selectores/computados):**
> - [nombre]: qué calcula y cuándo se usa
>
> **Estados de carga:**
> - loading: boolean — cuándo es true
> - error: string | null — qué errores se almacenan
> - data: tipo — qué estructura tiene el dato cargado

## Componentes de UI

> 🤖 **Instrucción para la IA:** Lista los componentes de UI que esta feature requiere.
> Si la feature es solo de backend, escribe "N/A" y omite el resto.
>
> Para cada componente usa este formato:
>
> **[NombreComponente]**
> - Propósito: qué hace este componente
> - Props: { nombre: tipo | descripción | requerido/opcional }
> - Estados internos: qué estado maneja localmente
> - Eventos que emite: [nombre-evento] → qué datos transmite
> - Dependencias: qué otros componentes usa o requiere
> - Notas de accesibilidad: atributos aria, navegación por teclado, contraste
>
> Ordena los componentes de más genérico a más específico (átomos antes que organismos).

## Plan de Pruebas

> 🤖 **Instrucción para la IA:** Esta sección es obligatoria. Una spec sin Plan de Pruebas está incompleta y no puede avanzar.
> No escribas código de pruebas aquí. Define únicamente los casos y la cobertura esperada.
> Las pruebas se implementarán en el tasks file (Fase 4).
>
> **Pruebas unitarias obligatorias:**
> Lista cada función, método o servicio que debe tener prueba unitaria.
> Formato: `[NombreFuncion / Servicio]` — casos a cubrir:
> - Caso 1: [descripción del caso y resultado esperado]
> - Caso 2: [caso con input inválido y resultado esperado]
> - ...
>
> Como mínimo, cubre:
> - El flujo feliz de cada función con lógica de negocio
> - Cada Regla de Negocio (BR-NN) referenciada en la feature spec
> - Casos con inputs vacíos, nulos o malformados
> - Casos donde el recurso no existe
>
> **Pruebas de integración obligatorias:**
> Lista cada endpoint o flujo de extremo a extremo que debe tener prueba de integración.
> Formato: `[MÉTODO /ruta]` — escenarios a probar:
> - Escenario exitoso: [descripción, datos de entrada, respuesta esperada]
> - Escenario de error [código]: [condición, respuesta esperada]
> - ...
>
> Como mínimo, cubre:
> - El flujo completo exitoso de cada endpoint definido en Contratos de API
> - Al menos un escenario de error por código de respuesta documentado (400, 401, 403, 404...)
> - El flujo completo del Happy Path descrito en la feature spec
>
> **Casos límite a cubrir explícitamente:**
> - Lista de condiciones de borde identificadas durante el paso de clarificación
> - Incluye casos de concurrencia si aplican (dos usuarios editando el mismo recurso, etc.)
> - Incluye casos de volumen si hay límites definidos en las Reglas de Negocio
