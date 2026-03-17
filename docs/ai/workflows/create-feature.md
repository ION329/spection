# Workflow: Create a new feature

Usa este workflow cuando el proyecto ya tiene arquitectura validada y necesitas añadir
una feature nueva. Si es el primer feature del proyecto, usa `init-project.md`.

---

## Prerequisitos

Antes de comenzar, verifica que existen y están validados:

- [ ] `docs/spec/product/product.md` — con `**Status: Validated**`
- [ ] `docs/spec/architecture/architecture.md` — con `**Status: Validated**`

Si la nueva feature requiere un cambio de arquitectura, ejecuta primero
`docs/ai/workflows/architecture-decision.md` para registrar el ADR correspondiente.

---

## Fase 1 — Feature Specification

**Prompt a usar:** `docs/ai/prompts/feature-spec.md`
**Agente:** `docs/ai/agents/systems-engineer.md`

1. Abre una sesión nueva de IA
2. Carga el prompt `docs/ai/prompts/feature-spec.md`
3. Describe al agente el objetivo de la nueva feature en una o dos oraciones
4. Responde el paso de clarificación del agente (obligatorio, no lo omitas)
5. Revisa la spec generada en `docs/spec/features/[feature-name]-spec.md`
6. Ejecuta `docs/ai/prompts/review.md` sobre la feature spec antes de validar

> **GATE 1 — Aprobación humana requerida**
> Añade `**Status: Validated**` al inicio de `docs/spec/features/[feature-name]-spec.md`.
> No abras la siguiente sesión hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/systems-engineer.md` → sección Handoff.

---

## Fase 2 — Engineering Specification + Tasks

**Prompt a usar:** `docs/ai/prompts/engineering.md`
**Agente:** `docs/ai/agents/lead-engineer.md`

1. Abre una sesión nueva de IA
2. Carga el prompt `docs/ai/prompts/engineering.md`
3. Indica al agente el nombre exacto de la feature: `[feature-name]`
4. El agente verificará el `**Status: Validated**` de la feature spec automáticamente
5. Revisa el engineering spec: `docs/spec/engineering/[feature-name]-engineering.md`
6. Revisa el tasks file: `docs/spec/tasks/[feature-name]-tasks.md`
7. Verifica la estructura del tasks file:
   - [ ] Fase 1 — Infrastructure definida
   - [ ] Fase 2 — Backend con orden: modelos → servicios → controllers → rutas
   - [ ] Fase 3 — Frontend con orden: átomos → compuestos → vistas → store → API
   - [ ] Fase 4 — Tests con al menos un test por endpoint y por componente principal
   - [ ] Tareas paralelizables marcadas con `[P]`
8. Ejecuta `docs/ai/prompts/review.md` sobre el engineering spec antes de validar

> **GATE 2 — Aprobación humana requerida**
> Añade `**Status: Validated**` al inicio de `docs/spec/engineering/[feature-name]-engineering.md`.
> Confirma que `docs/spec/tasks/[feature-name]-tasks.md` tiene todas las fases completas.
> No comiences a codificar hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/lead-engineer.md` → sección Handoff.

---

## Fase 3 — Implementation

Antes de escribir una sola línea de código, ejecuta obligatoriamente:

**`docs/ai/workflows/implementation-hygiene.md`**

---

## Fase 4 — Archive

Una vez que la feature está implementada, testeada y mergeada:

**`docs/ai/workflows/archive-feature.md`**

---

## Archivos generados por este workflow

```
docs/spec/
├── features/
│   └── [feature-name]-spec.md              ← Status: Validated
├── engineering/
│   └── [feature-name]-engineering.md       ← Status: Validated
└── tasks/
    └── [feature-name]-tasks.md
```
