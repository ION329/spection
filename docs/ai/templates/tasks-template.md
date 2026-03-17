# Tasks: [Feature Name]

<!-- Instrucción: Este archivo desglosa docs/spec/engineering/[feature]-engineering.md
en tareas atómicas y accionables, ordenadas por dependencias.
Guarda este archivo como: docs/spec/tasks/[feature-name]-tasks.md
Genera este archivo inmediatamente después de completar el engineering spec.
[P] indica tareas que pueden ejecutarse en paralelo con la tarea anterior del mismo nivel. -->

**Feature:** [feature-name]-engineering.md
**Status:** pending | in-progress | completed

---

## Task List

<!-- Instrucción: Ordena las tareas siguiendo esta secuencia de dependencias:
infrastructure → backend → frontend → tests
Numera las tareas en el orden exacto en que deben ejecutarse.
Marca con [P] las tareas que pueden ejecutarse en paralelo con la tarea inmediatamente anterior
del mismo nivel de dependencia. Una tarea es paralelizable cuando no consume el output
de su tarea hermana, solo del mismo padre o de una fase anterior.

Usa el siguiente formato para cada tarea: -->

### Phase 1 — Infrastructure

- [ ] **TASK-01** — [Descripción de la tarea de infraestructura]
  - Type: `infra`
  - Depends on: —
  - Detail: [qué crear, configurar o provisionar exactamente]

- [ ] **TASK-02** — [P] [Segunda tarea de infraestructura paralelizable]
  - Type: `infra`
  - Depends on: —
  - Detail: [detalle]

### Phase 2 — Backend

<!-- Instrucción: Lista las tareas de backend en orden. Empieza por modelos/entidades,
luego repositorios o acceso a datos, luego servicios/lógica de negocio, luego controladores/handlers,
y por último rutas o registro de endpoints. -->

- [ ] **TASK-03** — [Crear modelo o entidad de base de datos]
  - Type: `backend`
  - Depends on: TASK-01
  - Detail: [campos, tipos, migraciones necesarias según el database schema del engineering spec]

- [ ] **TASK-04** — [Implementar lógica de negocio o servicio]
  - Type: `backend`
  - Depends on: TASK-03
  - Detail: [reglas de negocio que implementa, referencia a BR-N de la feature spec]

- [ ] **TASK-05** — [P] [Implementar otro servicio independiente paralelizable]
  - Type: `backend`
  - Depends on: TASK-03
  - Detail: [detalle]

- [ ] **TASK-06** — [Implementar endpoint o handler]
  - Type: `backend`
  - Depends on: TASK-04, TASK-05
  - Detail: [método HTTP, ruta, contrato según el API contract del engineering spec]

### Phase 3 — Frontend

<!-- Instrucción: Lista las tareas de frontend en orden. Empieza por componentes atómicos,
luego componentes compuestos, luego vistas completas, luego integración con el estado global,
y por último conexión con la API. -->

- [ ] **TASK-07** — [Crear componente base o átomo]
  - Type: `frontend`
  - Depends on: —
  - Detail: [props, estados, comportamiento según UI Components del engineering spec]

- [ ] **TASK-08** — [P] [Crear otro componente base independiente]
  - Type: `frontend`
  - Depends on: —
  - Detail: [detalle]

- [ ] **TASK-09** — [Implementar vista o página]
  - Type: `frontend`
  - Depends on: TASK-07, TASK-08
  - Detail: [qué componentes compone, qué estado consume, qué flujo implementa]

- [ ] **TASK-10** — [Conectar con API y estado global]
  - Type: `frontend`
  - Depends on: TASK-06, TASK-09
  - Detail: [qué endpoints consume, qué acciones del store dispara]

### Phase 4 — Tests

<!-- Instrucción: Genera una tarea de test por cada caso definido en la sección
"Test Plan" del engineering spec. No inventes casos que no estén en el test plan.
Los tests de backend y frontend pueden marcarse [P] entre sí si son independientes. -->

- [ ] **TASK-11** — [Unit tests para [servicio o función]]
  - Type: `test`
  - Depends on: TASK-04
  - Detail: [casos a cubrir según el Test Plan del engineering spec]

- [ ] **TASK-12** — [P] [Unit tests para [componente]]
  - Type: `test`
  - Depends on: TASK-07
  - Detail: [casos a cubrir]

- [ ] **TASK-13** — [Integration tests para [endpoint o flujo completo]]
  - Type: `test`
  - Depends on: TASK-10, TASK-11, TASK-12
  - Detail: [flujo de extremo a extremo a probar, casos límite según el Test Plan]

---

## Progress

<!-- Instrucción: No modifiques esta sección manualmente. Actualízala al finalizar cada tarea.
Formato: [completadas] / [total] tareas -->

Completed: 0 / 0
