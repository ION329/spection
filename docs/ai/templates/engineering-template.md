# Especificación de Ingeniería

<!-- Instrucción: Este documento convierte la especificación de feature en contratos técnicos
implementables. Lee docs/spec/features/[feature]-spec.md y docs/spec/architecture/architecture.md
antes de completar esta plantilla. Cada decisión aquí debe ser trazable a la feature spec o a un ADR aceptado.
Al terminar este documento, genera también docs/spec/tasks/[feature]-tasks.md. -->

## Contratos de API

<!-- Instrucción: Define los contratos completos de cada endpoint de la feature.
Para cada endpoint usa exactamente este formato:

---
**[MÉTODO] /ruta/completa**
```
Cabeceras de Solicitud:
  Authorization: Bearer <token>  (si aplica)
  Content-Type: application/json

Cuerpo de Solicitud:
  {
    "campo": "tipo"  // descripción, requerido/opcional, validaciones
  }

Respuesta 200:
  {
    "campo": "tipo"  // descripción
  }

Respuesta 400: { "error": "descripción del error de validación" }
Respuesta 401: { "error": "no autenticado" }
Respuesta 403: { "error": "no autorizado" }
Respuesta 404: { "error": "recurso no encontrado" }
Respuesta 500: { "error": "error interno del servidor" }
```
---

Incluye todos los códigos de error posibles por endpoint. No uses "etc." ni omitas casos. -->

## Esquema de Base de Datos

<!-- Instrucción: Define el esquema completo de base de datos para esta feature.
Para cada tabla o colección usa este formato:

**Tabla: [nombre_tabla]**
| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | uuid | PRIMARY KEY, NOT NULL | Identificador único |
| [campo] | [tipo] | [NULL/NOT NULL, UNIQUE, FK...] | [descripción] |
| created_at | timestamp | NOT NULL, DEFAULT now() | Fecha de creación |
| updated_at | timestamp | NOT NULL | Fecha de última modificación |

Índices:
- [nombre_indice] en ([campos]) — motivo del índice

Relaciones:
- [tabla].[campo] → [tabla_referenciada].[campo] (ON DELETE [acción])

No uses tipos genéricos como "string" o "number". Usa tipos específicos del motor de base de datos aprobado. -->

## Gestión de Estado

<!-- Instrucción: Define el estado del lado del cliente para esta feature.
Si la feature es solo de backend, escribe "N/A — feature de backend puro" y omite el resto.

Para features con frontend, define:

**Estado global (store):**
```
{
  [slice_nombre]: {
    [campo]: tipo  // descripción y valor inicial
  }
}
```

**Acciones / Mutations:**
- [NOMBRE_ACCION]: qué hace, qué payload recibe, qué estado modifica

**Estados derivados (selectores/computados):**
- [nombre]: qué calcula y cuándo se usa

**Estados de carga:**
- loading: boolean — cuándo es true
- error: string | null — qué errores se almacenan
- data: tipo — qué estructura tiene el dato cargado -->

## Componentes de UI

<!-- Instrucción: Lista los componentes de UI que esta feature requiere.
Si la feature es solo de backend, escribe "N/A" y omite el resto.

Para cada componente usa este formato:

**[NombreComponente]**
- Propósito: qué hace este componente
- Props: { nombre: tipo | descripción | requerido/opcional }
- Estados internos: qué estado maneja localmente
- Eventos que emite: [nombre-evento] → qué datos transmite
- Dependencias: qué otros componentes usa o requiere
- Notas de accesibilidad: atributos aria, navegación por teclado, contraste

Ordena los componentes de más genérico a más específico (átomos antes que organismos). -->

## Plan de Pruebas

<!-- Instrucción: Define cómo se va a probar esta feature. Esta sección es obligatoria.
Cubre las tres categorías:

**Pruebas unitarias:**
- [función o método]: qué se prueba y qué casos se cubren

**Pruebas de integración:**
- [endpoint o flujo]: qué se prueba de extremo a extremo

**Casos límite a cubrir:**
- Lista de condiciones límite que deben tener prueba explícita

No escribas el código de las pruebas aquí. Define los casos y la cobertura esperada.
Las pruebas se implementan en el archivo de tareas, no en este documento. -->
