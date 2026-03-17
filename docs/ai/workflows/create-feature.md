# Workflow: Crear una nueva feature

Usa este workflow cuando el proyecto ya tiene arquitectura validada y necesitas añadir
una feature nueva. Si es la primera feature del proyecto, usa `init-project.md`.

---

## Prerequisitos

Antes de comenzar, verifica que existen y están validados:

- [ ] `docs/spec/product/product.md` — con `**Status: Validated**`
- [ ] `docs/spec/architecture/architecture.md` — con `**Status: Validated**`

Si la nueva feature requiere un cambio de arquitectura, ejecuta primero
`docs/ai/workflows/architecture-decision.md` para registrar el ADR correspondiente.

---

## Fase 1 — Especificación de Feature

**Prompt a usar:** `docs/ai/prompts/feature-spec.md`
**Agente:** `docs/ai/agents/systems-engineer.md`

1. Abre una sesión nueva de IA
2. Carga el prompt `docs/ai/prompts/feature-spec.md`
3. Describe al agente el objetivo de la nueva feature en una o dos oraciones
4. Responde el paso de clarificación del agente (obligatorio, no lo omitas)
5. Revisa la spec generada en `docs/spec/features/[feature-name]-spec.md`
6. Ejecuta `docs/ai/prompts/review.md` sobre la feature spec antes de validar

> **PUERTA 1 — Aprobación humana requerida**
> Revisa las **Notas de Revisión** al final del documento.
> Si la revisión arroja notas *críticas*, no valides. Devuelve el documento al agente creador con el prompt:
> *"Por favor corrige los problemas críticos listados en las notas de revisión"*, y vuelve a revisar.
> Solo cuando no haya notas críticas: añade `**Status: Validated**` al inicio de `docs/spec/features/[feature-name]-spec.md`.
> No abras la siguiente sesión hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/systems-engineer.md` → sección Handoff.

---

## Fase 2 — Especificación de Ingeniería + Tareas

**Prompt a usar:** `docs/ai/prompts/engineering.md`
**Agente:** `docs/ai/agents/lead-engineer.md`

1. Abre una sesión nueva de IA
2. Carga el prompt `docs/ai/prompts/engineering.md`
3. Indica al agente el nombre exacto de la feature: `[feature-name]`
4. El agente verificará el `**Status: Validated**` de la feature spec automáticamente
5. Revisa la spec de ingeniería: `docs/spec/engineering/[feature-name]-engineering.md`
6. Revisa el archivo de tareas: `docs/spec/tasks/[feature-name]-tasks.md`
7. Verifica la estructura del archivo de tareas:
   - [ ] Fase 1 — Infraestructura definida
   - [ ] Fase 2 — Backend con orden: modelos → servicios → controllers → rutas
   - [ ] Fase 3 — Frontend con orden: átomos → compuestos → vistas → store → API
   - [ ] Fase 4 — Pruebas con al menos una prueba por endpoint y por componente principal
   - [ ] Tareas paralelizables marcadas con `[P]`
8. Ejecuta `docs/ai/prompts/review.md` sobre el engineering spec antes de validar

> **PUERTA 2 — Aprobación humana requerida**
> Revisa las **Notas de Revisión** al final del documento.
> Si la revisión arroja notas *críticas*, no valides. Devuelve el documento al agente creador con el prompt:
> *"Por favor corrige los problemas críticos listados en las notas de revisión"*, y vuelve a revisar.
> Solo cuando no haya notas críticas: añade `**Status: Validated**` al inicio de `docs/spec/engineering/[feature-name]-engineering.md`.
> Confirma que `docs/spec/tasks/[feature-name]-tasks.md` tiene todas las fases completas.
> No comiences a codificar hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/lead-engineer.md` → sección Handoff.

---

## Fase 3 — Implementación

Antes de escribir una sola línea de código, ejecuta obligatoriamente:

**`docs/ai/workflows/implementation-hygiene.md`**

---

## Fase 4 — Documentación Pública

**Prompt a usar:** `docs/ai/prompts/review.md` (agente: Tech Writer)
**Agente:** `docs/ai/agents/tech-writer.md`

Ejecuta esta fase después de que la implementación esté completa y las pruebas pasen en CI.

1. Abre una sesión nueva de IA
2. Carga el agente `docs/ai/agents/tech-writer.md`
3. Indica al agente qué artefactos generar para esta feature (pregunta si no estás seguro)
4. El agente leerá `docs/spec/features/[feature-name]-spec.md` y `docs/spec/engineering/[feature-name]-engineering.md`
5. El agente generará los documentos públicos correspondientes en `docs/public/`:
   - `docs/public/[feature-name]-guide.md` — guía para desarrolladores externos
   - `docs/public/api-reference.md` — referencia de API pública (acumulativo, actualizar si existe)
   - `docs/public/onboarding.md` — actualizar si la feature impacta el onboarding
6. Revisa cada documento generado: verifica que no expone información interna (esquemas de BD, estrategias de seguridad, detalles de infraestructura)

> **PUERTA 4 — Aprobación humana requerida (documentación pública)**
> Revisa cada documento generado en `docs/public/`.
> Si la revisión arroja notas *críticas*, no valides. Devuelve el documento al agente creador con el prompt:
> *"Por favor corrige los problemas críticos listados en las notas de revisión"*, y vuelve a revisar.
> Solo cuando no haya notas críticas: añade `**Status: Validated**` al inicio de cada documento publicado.
> Criterios de aceptación: `docs/ai/agents/tech-writer.md` → sección Handoff.

---

## Fase 5 — Archivo

Una vez que la feature está implementada, testeada, mergeada y documentada públicamente:

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

docs/public/
├── [feature-name]-guide.md                 ← Status: Validated
└── api-reference.md                        ← actualizado
```
