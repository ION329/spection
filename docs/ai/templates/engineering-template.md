# Engineering Specification

<!-- Instrucción: Este documento convierte la especificación de feature en contratos técnicos
implementables. Lee docs/spec/features/[feature]-spec.md y docs/spec/architecture/architecture.md
antes de completar este template. Cada decisión aquí debe ser trazable a la feature spec o a un ADR aceptado.
Al terminar este documento, genera también docs/spec/tasks/[feature]-tasks.md. -->

## API Contracts

<!-- Instrucción: Define los contratos completos de cada endpoint de la feature.
Para cada endpoint usa exactamente este formato:

---
**[MÉTODO] /ruta/completa**
```
Request Headers:
  Authorization: Bearer <token>  (si aplica)
  Content-Type: application/json

Request Body:
  {
    "campo": "tipo"  // descripción, requerido/opcional, validaciones
  }

Response 200:
  {
    "campo": "tipo"  // descripción
  }

Response 400: { "error": "descripción del error de validación" }
Response 401: { "error": "no autenticado" }
Response 403: { "error": "no autorizado" }
Response 404: { "error": "recurso no encontrado" }
Response 500: { "error": "error interno del servidor" }
```
---

Incluye todos los códigos de error posibles por endpoint. No uses "etc." ni omitas casos. -->

## Database Schema

<!-- Instrucción: Define el schema completo de base de datos para esta feature.
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

## State Management

<!-- Instrucción: Define el estado del lado del cliente para esta feature.
Si la feature es backend-only, escribe "N/A — feature de backend puro" y omite el resto.

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

**Estados derivados (selectors/computed):**
- [nombre]: qué calcula y cuándo se usa

**Estados de carga:**
- loading: boolean — cuándo es true
- error: string | null — qué errores se almacenan
- data: tipo — qué estructura tiene el dato cargado -->

## UI Components

<!-- Instrucción: Lista los componentes de UI que esta feature requiere.
Si la feature es backend-only, escribe "N/A" y omite el resto.

Para cada componente usa este formato:

**[NombreComponente]**
- Propósito: qué hace este componente
- Props: { nombre: tipo | descripción | requerido/opcional }
- Estados internos: qué estado maneja localmente
- Eventos que emite: [nombre-evento] → qué datos transmite
- Dependencias: qué otros componentes usa o requiere
- Notas de accesibilidad: atributos aria, navegación por teclado, contraste

Ordena los componentes de más genérico a más específico (átomos antes que organismos). -->

## Test Plan

<!-- Instrucción: Define cómo se va a probar esta feature. Esta sección es obligatoria.
Cubre las tres categorías:

**Unit tests:**
- [función o método]: qué se prueba y qué casos se cubren

**Integration tests:**
- [endpoint o flujo]: qué se prueba de extremo a extremo

**Edge cases a cubrir:**
- Lista de condiciones límite que deben tener test explícito

No escribas el código de los tests aquí. Define los casos y la cobertura esperada.
Los tests se implementan en el tasks file, no en este documento. -->
