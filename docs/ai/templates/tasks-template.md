# Tareas: [Nombre de la Feature]

> 🤖 **Instrucción para la IA:** Este archivo desglosa docs/spec/engineering/[feature]-engineering.md
> en tareas atómicas y accionables, ordenadas por dependencias.
> Guarda este archivo como: docs/spec/tasks/[feature-name]-tasks.md
> Genera este archivo inmediatamente después de completar la spec de ingeniería.
> [P] indica tareas que pueden ejecutarse en paralelo con la tarea anterior del mismo nivel.

**Feature:** [feature-name]-engineering.md
**Estado:** pendiente | en-progreso | completado

---

## Lista de Tareas

> 🤖 **Instrucción para la IA:** Ordena las tareas siguiendo esta secuencia de dependencias:
> infraestructura → backend → frontend → pruebas
> Numera las tareas en el orden exacto en que deben ejecutarse.
> Marca con [P] las tareas que pueden ejecutarse en paralelo con la tarea inmediatamente anterior
> del mismo nivel de dependencia. Una tarea es paralelizable cuando no consume el output
> de su tarea hermana, solo del mismo padre o de una fase anterior.
>
> Usa el siguiente formato para cada tarea:

### Fase 1 — Infraestructura

- [ ] **TASK-01** — [Descripción de la tarea de infraestructura]
  - Tipo: `infra`
  - Depende de: —
  - Detalle: [qué crear, configurar o provisionar exactamente]

- [ ] **TASK-02** — [P] [Segunda tarea de infraestructura paralelizable]
  - Tipo: `infra`
  - Depende de: —
  - Detalle: [detalle]

### Fase 2 — Backend

> 🤖 **Instrucción para la IA:** Lista las tareas de backend en orden. Empieza por modelos/entidades,
> luego repositorios o acceso a datos, luego servicios/lógica de negocio, luego controladores/handlers,
> y por último rutas o registro de endpoints.

- [ ] **TASK-03** — [Crear modelo o entidad de base de datos]
  - Tipo: `backend`
  - Depende de: TASK-01
  - Detalle: [campos, tipos, migraciones necesarias según el esquema de BD de la spec de ingeniería]

- [ ] **TASK-04** — [Implementar lógica de negocio o servicio]
  - Tipo: `backend`
  - Depende de: TASK-03
  - Detalle: [reglas de negocio que implementa, referencia a BR-N de la feature spec]

- [ ] **TASK-05** — [P] [Implementar otro servicio independiente paralelizable]
  - Tipo: `backend`
  - Depende de: TASK-03
  - Detalle: [detalle]

- [ ] **TASK-06** — [Implementar endpoint o handler]
  - Tipo: `backend`
  - Depende de: TASK-04, TASK-05
  - Detalle: [método HTTP, ruta, contrato según el contrato de API de la spec de ingeniería]

### Fase 3 — Frontend

> 🤖 **Instrucción para la IA:** Lista las tareas de frontend en orden. Empieza por componentes atómicos,
> luego componentes compuestos, luego vistas completas, luego integración con el estado global,
> y por último conexión con la API.

- [ ] **TASK-07** — [Crear componente base o átomo]
  - Tipo: `frontend`
  - Depende de: —
  - Detalle: [props, estados, comportamiento según Componentes de UI de la spec de ingeniería]

- [ ] **TASK-08** — [P] [Crear otro componente base independiente]
  - Tipo: `frontend`
  - Depende de: —
  - Detalle: [detalle]

- [ ] **TASK-09** — [Implementar vista o página]
  - Tipo: `frontend`
  - Depende de: TASK-07, TASK-08
  - Detalle: [qué componentes compone, qué estado consume, qué flujo implementa]

- [ ] **TASK-10** — [Conectar con API y estado global]
  - Tipo: `frontend`
  - Depende de: TASK-06, TASK-09
  - Detalle: [qué endpoints consume, qué acciones del store dispara]

### Fase 4 — Pruebas

> 🤖 **Instrucción para la IA:** Genera una tarea de prueba por cada caso definido en la sección
> "Plan de Pruebas" de la spec de ingeniería. No inventes casos que no estén en el plan de pruebas.
> Las pruebas de backend y frontend pueden marcarse [P] entre sí si son independientes.

- [ ] **TASK-11** — [Pruebas unitarias para [servicio o función]]
  - Tipo: `test`
  - Depende de: TASK-04
  - Detalle: [casos a cubrir según el Plan de Pruebas de la spec de ingeniería]

- [ ] **TASK-12** — [P] [Pruebas unitarias para [componente]]
  - Tipo: `test`
  - Depende de: TASK-07
  - Detalle: [casos a cubrir]

- [ ] **TASK-13** — [Pruebas de integración para [endpoint o flujo completo]]
  - Tipo: `test`
  - Depende de: TASK-10, TASK-11, TASK-12
  - Detalle: [flujo de extremo a extremo a probar, casos límite según el Plan de Pruebas]

---

## Progreso

> 🤖 **Instrucción para la IA:** No modifiques esta sección manualmente. Actualízala al finalizar cada tarea.
> Formato: [completadas] / [total] tareas

Completadas: 0 / 0
