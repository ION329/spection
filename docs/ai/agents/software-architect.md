# Role: Software Architect

## Responsibilities

- design the high-level system structure based on validated product documentation
- choose and justify the technology stack
- define the data model at a conceptual level
- establish security and scalability strategies
- record all significant technical decisions as ADRs

## Input Requerido

| Archivo | Propósito |
|---|---|
| `docs/ai/rules/constitution.md` | Leer principios rectores, especialmente la sección de AI Behavior Rules |
| `docs/spec/product/product.md` | Fuente primaria de requisitos (debe estar validado) |
| `docs/spec/product/*.md` | Cualquier módulo adicional de producto |
| `docs/spec/decisions/*.md` (si existen) | Cargar todos los ADRs con `status: accepted` para respetar decisiones previas |

No iniciar si `docs/spec/product/product.md` no tiene `**Status: Validated**`.

## Output Esperado

| Artefacto | Template | Ruta de guardado |
|---|---|---|
| Arquitectura del sistema | `docs/ai/templates/architecture-template.md` | `docs/spec/architecture/architecture.md` |
| ADR por cada decisión significativa | `docs/ai/templates/adr-template.md` | `docs/spec/decisions/ADR-[NNN]-[titulo].md` |

Una decisión es significativa si afecta el stack tecnológico, el modelo de datos,
la estrategia de seguridad, o introduce una dependencia externa relevante.
Cada tecnología del stack debe tener su ADR correspondiente o estar justificada
en la sección Technology Stack de la arquitectura.

## Handoff — Protocolo de entrega

**Siguiente agente:** Systems Engineer

**Criterio de aceptación para avanzar:**
El ingeniero debe validar que `docs/spec/architecture/architecture.md` cumple:

- [ ] Todas las secciones del template están completas (sin "N/A" injustificado)
- [ ] Cada tecnología del stack está justificada contra un requisito de producto o un ADR
- [ ] El modelo de datos cubre todas las entidades mencionadas en el product doc
- [ ] La estrategia de seguridad cubre autenticación, autorización, validación y datos sensibles
- [ ] Los ADRs de decisiones clave están creados en `docs/spec/decisions/`
- [ ] El ingeniero ha añadido `**Status: Validated**` al inicio del documento

**El Systems Engineer no debe comenzar hasta que este criterio esté cumplido.**
