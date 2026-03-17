# Feature Specification

<!-- Instrucción: Este documento especifica una feature individual del sistema.
Complétalo después de tener docs/spec/architecture/architecture.md validado.
Ejecuta el paso de clarificación (docs/ai/prompts/feature-spec.md) antes de rellenar este template.
Una feature = un archivo. Si la feature es demasiado grande, divídela en sub-features. -->

## Feature Name

<!-- Instrucción: Escribe el nombre oficial de la feature en formato título.
Usa el mismo nombre que aparecerá en el nombre de archivo: [feature-name]-spec.md.
Ejemplo: "User Authentication", "Nutritional Calculator", "Export to PDF". -->

## Description

<!-- Instrucción: Escribe 2-4 oraciones describiendo qué hace esta feature, para quién es,
y qué valor entrega al usuario. No incluyas detalles de implementación aquí.
Responde: ¿Qué hace? ¿Para quién? ¿Por qué importa? -->

## User Flow

<!-- Instrucción: Describe el flujo completo del usuario paso a paso, en orden cronológico.
Usa numeración. Incluye todos los caminos: flujo feliz, flujos alternativos y flujos de error.
Formato:
1. [Actor] [acción]
2. [Sistema] [respuesta]
3. ...
Flujo alternativo A (condición): ...
Flujo de error E1 (condición): ...
No omitas los flujos de error. Son requisitos, no excepciones. -->

## Business Rules

<!-- Instrucción: Lista todas las reglas de negocio que gobiernan esta feature.
Una regla de negocio es una restricción, condición o política que el sistema debe respetar.
Formato: BR-[N]: [descripción de la regla en una sola oración afirmativa].
Ejemplo: BR-1: Un usuario no puede tener más de una sesión activa simultáneamente.
Sé exhaustivo. Las reglas omitidas aquí se convierten en bugs en implementación. -->

## States and Transitions

<!-- Instrucción: Si la feature involucra entidades con estados (pedidos, sesiones, publicaciones, etc.),
define el ciclo de vida completo. Lista los estados posibles y las transiciones permitidas.
Formato:
- Estados: [estado_1, estado_2, estado_3]
- [estado_origen] → [estado_destino]: [condición que dispara la transición]
Si la feature no tiene estados, escribe "N/A". No omitas esta sección. -->

## Dependencies

<!-- Instrucción: Lista las dependencias de esta feature en dos categorías:
1. Internas: otras features de este proyecto que deben existir antes que esta
2. Externas: APIs de terceros, servicios externos, librerías específicas
Para cada dependencia, indica: nombre | tipo (interna/externa) | por qué es necesaria.
Incluye también qué features dependen de esta (dependencias inversas). -->

## API Endpoints

<!-- Instrucción: Define los endpoints de API que esta feature requiere.
Para cada endpoint usa el siguiente formato:

**[MÉTODO] /ruta/del/endpoint**
- Descripción: qué hace este endpoint
- Auth: requerida | pública | rol requerido
- Request body: { campo: tipo | descripción | requerido/opcional }
- Response 200: { campo: tipo | descripción }
- Response [código de error]: condición que produce este error

Si la feature no expone endpoints (solo UI, solo backend interno), escribe "N/A". -->

## UI Requirements

<!-- Instrucción: Describe los requisitos de interfaz de usuario. Cubre:
- Vistas o pantallas involucradas (lista con su propósito)
- Componentes clave que deben existir en cada vista
- Comportamientos de UI: loading states, empty states, error states, estados de éxito
- Restricciones de accesibilidad o internacionalización si aplican
Si la feature es exclusivamente backend, escribe "N/A". -->
