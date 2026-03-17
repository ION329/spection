# Workflow: Initialize a new project

Este workflow cubre el ciclo completo desde cero hasta tener el primer feature listo para codificar.
Sigue las fases en orden. Ninguna fase puede comenzar sin la aprobación explícita del ingeniero.

---

## Fase 1 — Discovery

**Prompt a usar:** `docs/ai/prompts/discovery.md`
**Agente:** `docs/ai/agents/product-strategist.md`

1. Abre una sesión nueva de IA
2. Carga el prompt `docs/ai/prompts/discovery.md`
3. Responde las preguntas estructuradas del agente
4. Revisa el borrador generado en `docs/spec/product/product.md`
5. Ejecuta el prompt de review si necesitas una segunda opinión: `docs/ai/prompts/review.md`

> **GATE 1 — Aprobación humana requerida**
> Añade `**Status: Validated**` al inicio de `docs/spec/product/product.md`.
> No abras la siguiente sesión hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/product-strategist.md` → sección Handoff.

---

## Fase 2 — Architecture

**Prompt a usar:** `docs/ai/prompts/architecture.md`
**Agente:** `docs/ai/agents/software-architect.md`

1. Abre una sesión nueva de IA
2. Carga el prompt `docs/ai/prompts/architecture.md`
3. El agente verificará que `docs/spec/product/product.md` tiene `**Status: Validated**`
4. Revisa el documento generado en `docs/spec/architecture/architecture.md`
5. Revisa los ADRs generados en `docs/spec/decisions/`
6. Ejecuta `docs/ai/prompts/review.md` sobre la arquitectura si es necesario

> **GATE 2 — Aprobación humana requerida**
> Añade `**Status: Validated**` al inicio de `docs/spec/architecture/architecture.md`.
> Verifica que cada ADR generado tiene `status: accepted` o `status: proposed` según corresponda.
> No abras la siguiente sesión hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/software-architect.md` → sección Handoff.

---

## Fase 3 — Feature Specification

**Prompt a usar:** `docs/ai/prompts/feature-spec.md`
**Agente:** `docs/ai/agents/systems-engineer.md`

1. Abre una sesión nueva de IA
2. Carga el prompt `docs/ai/prompts/feature-spec.md`
3. El agente verificará que `docs/spec/architecture/architecture.md` tiene `**Status: Validated**`
4. Responde el paso de clarificación del agente (obligatorio, una ronda por feature)
5. Revisa cada spec generada en `docs/spec/features/[feature-name]-spec.md`
6. Ejecuta `docs/ai/prompts/review.md` sobre cada feature spec antes de validar

> **GATE 3 — Aprobación humana requerida (por cada feature)**
> Añade `**Status: Validated**` al inicio de cada `docs/spec/features/[feature-name]-spec.md`.
> Una feature sin validación no puede avanzar a ingeniería.
> Criterios de aceptación: `docs/ai/agents/systems-engineer.md` → sección Handoff.

---

## Fase 4 — Engineering Specification + Tasks

**Prompt a usar:** `docs/ai/prompts/engineering.md`
**Agente:** `docs/ai/agents/lead-engineer.md`

1. Abre una sesión nueva de IA por cada feature (una sesión = una feature)
2. Carga el prompt `docs/ai/prompts/engineering.md`
3. Indica al agente el nombre de la feature a especificar
4. El agente verificará que la feature spec tiene `**Status: Validated**`
5. Revisa el engineering spec generado en `docs/spec/engineering/[feature-name]-engineering.md`
6. Revisa el tasks file generado en `docs/spec/tasks/[feature-name]-tasks.md`
7. Verifica que el tasks file tiene tareas en las 4 fases: infra → backend → frontend → tests
8. Ejecuta `docs/ai/prompts/review.md` sobre el engineering spec antes de validar

> **GATE 4 — Aprobación humana requerida (por cada feature)**
> Añade `**Status: Validated**` al inicio de `docs/spec/engineering/[feature-name]-engineering.md`.
> Confirma que `docs/spec/tasks/[feature-name]-tasks.md` está completo.
> No comiences a codificar hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/lead-engineer.md` → sección Handoff.

---

## Fase 5 — Implementation

Antes de escribir una sola línea de código, ejecuta obligatoriamente:

**`docs/ai/workflows/implementation-hygiene.md`**

Una vez completada la implementación y los tests, ejecuta:

**`docs/ai/workflows/archive-feature.md`**

---

## Resumen de archivos generados

Al completar las 4 primeras fases, el proyecto debe tener:

```
docs/spec/
├── product/
│   └── product.md                          ← Status: Validated
├── architecture/
│   └── architecture.md                     ← Status: Validated
├── decisions/
│   └── ADR-001-[decision].md
├── features/
│   └── [feature-name]-spec.md              ← Status: Validated (por feature)
├── engineering/
│   └── [feature-name]-engineering.md       ← Status: Validated (por feature)
└── tasks/
    └── [feature-name]-tasks.md
```
