# Prompt: Especificación de Ingeniería

## 1. Rol

Carga y aplica las instrucciones definidas en `docs/ai/agents/lead-engineer.md`.
Ese archivo define tu rol, las restricciones de tecnología y el protocolo de entrega. Léelo antes de continuar.

## 2. Prerequisito de entrada

El ingeniero debe indicarte el nombre de la feature a especificar.
Antes de continuar, verifica que `docs/spec/features/[feature-name]-spec.md` contiene
la línea `**Status: Validated**` al inicio del documento.

Si no está validado: detente. La feature spec debe estar validada antes de ingeniería. No generes nada.

## 3. Contexto a leer

Lee los siguientes archivos en este orden:

1. `docs/ai/rules/constitution.md` — secciones II, III y V son especialmente relevantes
2. `docs/ai/agents/lead-engineer.md` — tu rol y restricciones
3. `docs/spec/features/[feature-name]-spec.md` — fuente primaria (sustituye `[feature-name]` por el nombre real)
4. `docs/spec/architecture/architecture.md` — restricciones técnicas del sistema
5. `docs/spec/decisions/*.md` — todos los ADRs con `status: accepted` (son restricciones vinculantes, no sugerencias)

Si en algún punto necesitas tomar una decisión técnica que no está cubierta por la arquitectura
ni por un ADR existente, detente y consulta al ingeniero. No asumas.

## 4. Tarea — Spec de Ingeniería

Transforma la feature spec en contratos técnicos implementables.
Cada decisión debe ser trazable a una sección de la feature spec o a un ADR aceptado.
Referencia explícitamente las Reglas de Negocio (`BR-N`) de la feature spec donde aplique.

Reglas de implementación:
- Usa solo los tipos de datos del motor de base de datos aprobado en la arquitectura
- Los endpoints deben cubrir todos los códigos de error posibles, sin omitir casos
- La sección Plan de Pruebas es obligatoria — sin ella, la spec está incompleta
- No uses "etc." en ninguna sección. Si no sabes qué más incluir, pregunta.

## 5. Tarea — Archivo de Tareas

Inmediatamente después de completar la spec de ingeniería, genera el archivo de tareas.
Ambos archivos son parte del mismo output. No entregues uno sin el otro.

Reglas para el archivo de tareas:
- Orden obligatorio de fases: infraestructura → backend → frontend → tests
- Dentro del backend: modelos → repositorios → servicios → controllers → rutas
- Dentro del frontend: componentes atómicos → compuestos → vistas → integración con store → conexión con API
- Marca con `[P]` las tareas que no consumen el output de su tarea hermana inmediata
- Cada tarea del Plan de Pruebas de la spec de ingeniería debe tener su tarea correspondiente en la Fase 4

## 6. Plantillas obligatorias

**Spec de Ingeniería:** usa exactamente la estructura de `docs/ai/templates/engineering-template.md`.
Sigue las instrucciones marcadas con `> 🤖 **Instrucción para la IA:**` al pie de la letra.

**Archivo de Tareas:** usa exactamente la estructura de `docs/ai/templates/tasks-template.md`.
Sustituye los ejemplos de la plantilla con las tareas reales de esta feature.

## 7. Output

**Spec de Ingeniería:**
- **Ruta:** `docs/spec/engineering/[feature-name]-engineering.md`
- **Convención:** kebab-case, sufijo `-engineering`
  - Correcto: `user-authentication-engineering.md`
  - Incorrecto: `engineering-user-auth.md`, `UserAuth-eng.md`

**Archivo de Tareas:**
- **Ruta:** `docs/spec/tasks/[feature-name]-tasks.md`
- **Convención:** kebab-case, sufijo `-tasks`, mismo prefijo que la spec de ingeniería
  - Correcto: `user-authentication-tasks.md`

Confirma ambas rutas antes de escribir. Genera primero la spec de ingeniería, luego el archivo de tareas.
Al finalizar, lista los dos archivos generados con sus rutas completas.
