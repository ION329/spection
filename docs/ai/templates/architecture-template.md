# Arquitectura del Sistema

<!-- Instrucción: Este documento describe la arquitectura completa del sistema.
Completa todas las secciones basándote en docs/spec/product/product.md.
No inventes tecnologías que no estén aprobadas en docs/spec/decisions/.
Si una sección no aplica, escribe "N/A" con una justificación de una línea. -->

## Visión General del Sistema

<!-- Instrucción: Escribe 3-5 párrafos describiendo el sistema en términos generales.
Explica qué hace, cómo se divide en grandes componentes, y qué problema resuelve.
No menciones tecnologías aún. Enfócate en responsabilidades y límites del sistema. -->

## Stack Tecnológico

<!-- Instrucción: Genera una tabla con columnas: Capa | Tecnología | Justificación.
Cubre: frontend, backend, base de datos, autenticación, almacenamiento, hosting, CI/CD.
Cada justificación debe referenciar un requisito del producto o un ADR aceptado.
No incluyas tecnologías que no hayas justificado. -->

## Arquitectura de Alto Nivel

<!-- Instrucción: Describe la arquitectura usando un diagrama ASCII o una lista jerárquica
de componentes y sus relaciones. Muestra: cliente → API → servicios → base de datos.
Indica los límites de cada componente y cómo se comunican (REST, eventos, colas, etc.).
Si el sistema tiene múltiples servicios, explica la estrategia de comunicación entre ellos. -->

## Modelo de Datos

<!-- Instrucción: Define las entidades principales del sistema y sus relaciones.
Para cada entidad, lista: nombre, atributos clave (nombre, tipo, restricciones) y relaciones con otras entidades.
Usa el formato: Entidad → atributo: tipo | restricción.
Incluye cardinalidad de las relaciones (1:1, 1:N, N:N).
No definas el esquema completo de base de datos aquí (eso va en engineering-template.md). -->

## Estrategia de Seguridad

<!-- Instrucción: Describe la estrategia de seguridad en cuatro áreas obligatorias:
1. Autenticación: mecanismo (JWT, sesión, OAuth) y flujo
2. Autorización: modelo de permisos (RBAC, ABAC, por recurso) y quién puede hacer qué
3. Validación de inputs: dónde se valida y contra qué reglas
4. Protección de datos sensibles: qué datos se encriptan, cómo y dónde
Si alguna área no aplica, justifícalo. La seguridad no es opcional. -->

## Estrategia de Escalabilidad

<!-- Instrucción: Describe cómo el sistema escala bajo carga. Cubre:
- Estrategia de escalado (horizontal, vertical, serverless)
- Puntos de cuello de botella identificados y cómo se mitigan
- Estrategia de caché si aplica (qué se cachea, dónde, por cuánto tiempo)
- Límites conocidos del diseño actual y cuándo sería necesario revisarlos
Si el sistema es pequeño, indica explícitamente que la estrategia de escalado no es una prioridad actual y por qué. -->
