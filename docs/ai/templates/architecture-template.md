# Arquitectura del Sistema

> 🤖 **Instrucción para la IA:** Este documento describe la arquitectura completa del sistema.
> Completa todas las secciones basándote en docs/spec/product/product.md.
> No inventes tecnologías que no estén aprobadas en docs/spec/decisions/.
> Si una sección no aplica, escribe "N/A" con una justificación de una línea.

## Visión General del Sistema

> 🤖 **Instrucción para la IA:** Escribe 3-5 párrafos describiendo el sistema en términos generales.
> Explica qué hace, cómo se divide en grandes componentes, y qué problema resuelve.
> No menciones tecnologías aún. Enfócate en responsabilidades y límites del sistema.

## Stack Tecnológico

> 🤖 **Instrucción para la IA:** Genera una tabla con columnas: Capa | Tecnología | Justificación.
> Cubre obligatoriamente: frontend, backend, base de datos, autenticación, almacenamiento, hosting y CI/CD.
> Cada fila de justificación debe referenciar de forma explícita uno de los siguientes:
> - Un requisito del producto en docs/spec/product/product.md (cita la sección o el caso de uso)
> - Un ADR aceptado en docs/spec/decisions/ (cita el ID, ej. ADR-001)
> No incluyas ninguna tecnología sin justificación. Si no encuentras justificación, pregunta al ingeniero antes de continuar.

## Arquitectura de Alto Nivel

> 🤖 **Instrucción para la IA:** Describe la arquitectura usando un diagrama ASCII o una lista jerárquica
> de componentes y sus relaciones. Muestra: cliente → API → servicios → base de datos.
> Indica los límites de cada componente y cómo se comunican (REST, eventos, colas, etc.).
> Si el sistema tiene múltiples servicios, explica la estrategia de comunicación entre ellos.

## Modelo de Datos

> 🤖 **Instrucción para la IA:** Esta sección tiene dos partes obligatorias:
>
> **Parte 1 — Diagrama ER en Mermaid:**
> Genera un diagrama erDiagram de Mermaid con todas las entidades principales del sistema y sus relaciones.
> Usa la sintaxis estándar de Mermaid ER. Ejemplo:
>
> ```mermaid
> erDiagram
>   USUARIO ||--o{ PEDIDO : "realiza"
>   PEDIDO }o--|| PRODUCTO : "contiene"
> ```
>
> Incluye cardinalidad correcta: ||, |o, }|, }o según corresponda.
> No omitas ninguna entidad mencionada en docs/spec/product/product.md.
>
> **Parte 2 — Lista de entidades principales:**
> Para cada entidad del diagrama, describe:
> - Nombre de la entidad
> - Atributos clave: nombre | tipo conceptual | restricción relevante
> - Relaciones con otras entidades y su cardinalidad (1:1, 1:N, N:N)
>
> No definas el esquema completo de base de datos aquí (tipos específicos del motor van en engineering-template.md).

## Estrategia de Seguridad

> 🤖 **Instrucción para la IA:** Define la estrategia de seguridad en tres áreas obligatorias. Ninguna puede omitirse sin justificación explícita.
>
> **1. Autenticación:**
> - Mecanismo elegido: JWT, sesión con cookie, OAuth 2.0, API key, etc.
> - Flujo completo: cómo el usuario obtiene credenciales, cómo se validan, cuándo expiran
> - Referencia al ADR correspondiente si la tecnología está registrada
>
> **2. Autorización:**
> - Modelo de permisos: RBAC (roles), ABAC (atributos), por recurso, o combinación
> - Tabla de permisos: qué rol/actor puede ejecutar qué acción sobre qué recurso
> - Cómo se aplica la autorización: middleware, guards, decoradores, políticas
>
> **3. Protección de datos sensibles:**
> - Lista de campos o datos considerados sensibles en este sistema
> - Qué datos se encriptan y con qué mecanismo (en tránsito: TLS; en reposo: AES-256, bcrypt, etc.)
> - Qué datos nunca deben exponerse en logs, respuestas de API o documentación pública
> - Política de retención y eliminación de datos si aplica
>
> También cubre, si aplica: validación de inputs (capa y reglas), protección contra CSRF, rate limiting, cabeceras de seguridad HTTP.

## Estrategia de Escalabilidad

> 🤖 **Instrucción para la IA:** Describe cómo el sistema escala bajo carga. Cubre:
> - Estrategia de escalado (horizontal, vertical, serverless)
> - Puntos de cuello de botella identificados y cómo se mitigan
> - Estrategia de caché si aplica (qué se cachea, dónde, por cuánto tiempo)
> - Límites conocidos del diseño actual y cuándo sería necesario revisarlos
> Si el sistema es pequeño, indica explícitamente que la estrategia de escalado no es una prioridad actual y por qué.
