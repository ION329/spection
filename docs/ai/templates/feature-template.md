# Especificación de Feature

> 🤖 **Instrucción para la IA:** Este documento especifica una feature individual del sistema.
> Complétalo después de tener docs/spec/architecture/architecture.md validado.
> Ejecuta el paso de clarificación (docs/ai/prompts/feature-spec.md) antes de rellenar esta plantilla.
> Una feature = un archivo. Si la feature es demasiado grande, divídela en sub-features.

## Nombre de la Feature

> 🤖 **Instrucción para la IA:** Escribe el nombre oficial de la feature en formato título.
> Usa el mismo nombre que aparecerá en el nombre de archivo: [feature-name]-spec.md.
> Ejemplo: "Autenticación de Usuario", "Calculadora Nutricional", "Exportar a PDF".

## Descripción

> 🤖 **Instrucción para la IA:** Escribe 2-4 oraciones describiendo qué hace esta feature, para quién es,
> y qué valor entrega al usuario. No incluyas detalles de implementación aquí.
> Responde: ¿Qué hace? ¿Para quién? ¿Por qué importa?

## Flujo de Usuario

> 🤖 **Instrucción para la IA:** Documenta el flujo completo en tres bloques obligatorios. No omitas ninguno.
>
> **Flujo feliz (Happy Path):**
> Describe el camino ideal paso a paso, en orden cronológico estricto.
> Usa el formato: N. [Actor] → [acción o respuesta del sistema]
> El Actor puede ser: Usuario, Sistema, Servicio externo, etc.
>
> **Flujos alternativos:**
> Cada variación válida del flujo principal que produce un resultado diferente pero correcto.
> Formato: Alternativo A — [condición que lo dispara]: [pasos del flujo alternativo]
> Ejemplo: Alternativo A — El usuario ya tiene sesión activa: el sistema omite el paso de login.
>
> **Flujos de error:**
> Cada condición de fallo que el sistema debe manejar de forma explícita.
> Formato: Error E[N] — [condición]: [qué hace el sistema], [qué ve el usuario]
> Ejemplo: Error E1 — Credenciales incorrectas: el sistema devuelve 401 y muestra el mensaje "Correo o contraseña inválidos".
>
> No uses lenguaje vago como "el sistema responde" sin especificar qué responde.
> Cada paso de error es un requisito funcional, no una excepción.

## Reglas de Negocio

> 🤖 **Instrucción para la IA:** Lista todas las restricciones, condiciones y políticas que el sistema debe respetar para esta feature.
>
> **Formato obligatorio para cada regla:**
> BR-[NN]: [descripción de la regla en una sola oración afirmativa y verificable]
>
> Reglas para asignar identificadores:
> - Usa numeración de dos dígitos con cero a la izquierda: BR-01, BR-02, BR-03...
> - El ID es único dentro de este archivo. No reutilices IDs entre features.
> - Si una regla modifica otra de otro archivo, referencia la original: BR-01 (extiende user-authentication-spec BR-03)
>
> Ejemplos de buenas reglas:
> - BR-01: Un usuario no puede tener más de una sesión activa simultáneamente.
> - BR-02: El precio total del pedido no puede ser negativo.
> - BR-03: Solo usuarios con rol ADMIN pueden eliminar registros.
>
> Sé exhaustivo. Cada regla omitida aquí se convierte en un bug o comportamiento indefinido durante la implementación.
> Las reglas de esta sección serán referenciadas como restricciones vinculantes en el engineering spec y en el tasks file.

## Estados y Transiciones

> 🤖 **Instrucción para la IA:** Si la entidad principal de esta feature cambia de estado a lo largo de su ciclo de vida,
> esta sección tiene dos partes obligatorias.
>
> **Parte 1 — Diagrama Mermaid State:**
> Genera un diagrama stateDiagram-v2 de Mermaid que muestre todos los estados posibles y todas las transiciones válidas.
> Usa la sintaxis estándar de Mermaid. Ejemplo:
>
> ```mermaid
> stateDiagram-v2
>   [*] --> Borrador
>   Borrador --> EnRevisión : el usuario envía el formulario
>   EnRevisión --> Aprobado : el admin aprueba
>   EnRevisión --> Rechazado : el admin rechaza
>   Rechazado --> Borrador : el usuario corrige y reenvía
>   Aprobado --> [*]
> ```
>
> Incluye el estado inicial [*] y el estado final [*] si aplica.
> Cada flecha debe tener una etiqueta que indique la condición o acción que dispara la transición.
>
> **Parte 2 — Tabla de transiciones:**
> Para cada transición del diagrama, especifica:
> - Estado origen → Estado destino
> - Condición o evento que dispara la transición
> - Actor que ejecuta la acción (usuario, sistema, servicio externo, tiempo)
> - Efecto secundario si lo hay (notificación enviada, campo actualizado, etc.)
>
> Si la feature no involucra entidades con estados, escribe "N/A" con una justificación de una línea.

## Dependencias

> 🤖 **Instrucción para la IA:** Lista las dependencias de esta feature en dos categorías:
> 1. Internas: otras features de este proyecto que deben existir antes que esta
> 2. Externas: APIs de terceros, servicios externos, librerías específicas
> Para cada dependencia, indica: nombre | tipo (interna/externa) | por qué es necesaria.
> Incluye también qué features dependen de esta (dependencias inversas).

## Endpoints de API

> 🤖 **Instrucción para la IA:** Define los endpoints de API que esta feature requiere.
> Para cada endpoint usa el siguiente formato:
>
> **[MÉTODO] /ruta/del/endpoint**
> - Descripción: qué hace este endpoint
> - Auth: requerida | pública | rol requerido
> - Cuerpo de solicitud: { campo: tipo | descripción | requerido/opcional }
> - Respuesta 200: { campo: tipo | descripción }
> - Respuesta [código de error]: condición que produce este error
>
> Si la feature no expone endpoints (solo UI, solo backend interno), escribe "N/A".

## Requisitos de UI

> 🤖 **Instrucción para la IA:** Describe los requisitos de interfaz de usuario. Cubre:
> - Vistas o pantallas involucradas (lista con su propósito)
> - Componentes clave que deben existir en cada vista
> - Comportamientos de UI: estados de carga, estados vacíos, estados de error, estados de éxito
> - Restricciones de accesibilidad o internacionalización si aplican
> Si la feature es exclusivamente backend, escribe "N/A".
