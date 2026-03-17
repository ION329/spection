# Prompt: Discovery

## 1. Rol

Carga y aplica las instrucciones definidas en `docs/ai/agents/product-strategist.md`.
Ese archivo define tu rol, responsabilidades y criterios de entrega. Léelo antes de continuar.

## 2. Contexto a leer

Lee los siguientes archivos en este orden antes de hacer cualquier pregunta:

1. `docs/ai/rules/constitution.md` — principios rectores obligatorios
2. `README.md` (raíz del proyecto) — contexto general del proyecto si existe
3. `docs/spec/product/` — leer todos los archivos si ya existen, para no contradecir definiciones previas

Si alguno de los archivos no existe, continúa. No es un error bloqueante en esta fase.

## 3. Tarea

No generes documentación todavía.

Primero, haz al ingeniero las siguientes preguntas en una sola ronda estructurada.
Numera cada pregunta. Espera las respuestas antes de avanzar.

1. ¿Qué problema resuelve este producto? ¿A quién le duele ese problema hoy?
2. ¿Quiénes son los usuarios objetivo? Describe sus características, contexto y nivel técnico.
3. ¿Cuáles son los 3 casos de uso más importantes que el sistema debe cubrir en su primera versión?
4. ¿Qué restricciones de negocio existen? (presupuesto, plazos, regulaciones, integraciones obligatorias)
5. ¿Cómo se mide el éxito de este producto? ¿Qué métricas o criterios indican que funciona?
6. ¿Qué está explícitamente fuera del alcance de esta versión?

No hagas preguntas adicionales sin permiso del ingeniero.
Si una respuesta es ambigua, pide clarificación sobre esa respuesta específica antes de continuar.

## 4. Template obligatorio

Usa exactamente la estructura de `docs/ai/templates/product-template.md`.
No omitas ninguna sección. No añadas secciones que no estén en el template.
Si una sección no aplica, escríbela con "N/A" y una justificación de una línea.

## 5. Output

- **Ruta:** `docs/spec/product/product.md`
- **Convención de nombres:** si el proyecto tiene múltiples módulos, crear un archivo por módulo usando el patrón `docs/spec/product/[nombre-modulo].md` en kebab-case
- **Formato:** Markdown, siguiendo el template sin modificaciones estructurales

No guardes el archivo hasta haber recibido todas las respuestas del ingeniero.
Confirma la ruta de guardado antes de escribir.
