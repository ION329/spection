# Spection

Desarrollo Guiado por Especificación. La especificación es la fuente de verdad.
El código es una consecuencia directa de la documentación.

## Estructura

```
docs/
├── ai/                              ← motor de metodología (reglas del framework, no modificar por proyecto)
│   ├── ai-engineering-methodology.md   ← documento canónico de la metodología
│   ├── agents/                      ← definiciones de roles de IA
│   ├── prompts/                     ← prompts ejecutables con contratos de entrada/salida
│   ├── templates/                   ← plantillas de documentos
│   ├── workflows/                   ← guías de procesos paso a paso
│   └── rules/                       ← gobernanza y reglas constitucionales
│       └── constitution.md          ← principios de ingeniería no negociables
│
├── spec/                            ← especificaciones del proyecto (generadas por IA, validadas por el ingeniero)
│   ├── product/                     ← definición de producto y espacio del problema
│   ├── architecture/                ← arquitectura del sistema y stack tecnológico
│   ├── features/                    ← especificaciones individuales de features
│   ├── engineering/                 ← especificaciones de ingeniería listas para implementar
│   ├── tasks/                       ← desgloses de tareas por feature
│   └── decisions/                   ← registros de decisiones de arquitectura (ADRs)
│
├── public/                          ← documentación simplificada para stakeholders
└── lab/                             ← experimentos, investigación e historial de implementación
    └── history/                     ← especificaciones archivadas de features implementadas
```

## Cómo funciona

Spection ejecuta un pipeline de agentes de IA especializados. Cada fase produce un documento validado
antes de que comience la siguiente. Ninguna fase puede ser omitida.

```
Descubrimiento → Arquitectura → Spec de Feature → Spec de Ingeniería + Tareas → Implementación → Archivo
```

| Agente | Prompt | Salida |
|---|---|---|
| Estratega de Producto | `prompts/discovery.md` | `docs/spec/product/product.md` |
| Arquitecto de Software | `prompts/architecture.md` | `docs/spec/architecture/architecture.md` + ADRs |
| Ingeniero de Sistemas | `prompts/feature-spec.md` | `docs/spec/features/[feature]-spec.md` |
| Ingeniero Líder | `prompts/engineering.md` | `docs/spec/engineering/[feature]-engineering.md` + `tasks.md` |
| Escritor Técnico | `prompts/review.md` | `docs/public/` |

Cada transición de fase requiere la aprobación explícita del ingeniero (`**Status: Validated**`).

## Comienza aquí

**Proyecto nuevo:**
1. Lee la metodología: `docs/ai/ai-engineering-methodology.md`
2. Lee las reglas del proyecto: `docs/ai/rules/constitution.md`
3. Ejecuta el workflow completo: `docs/ai/workflows/init-project.md`

**Añadir una feature a un proyecto existente:**
- `docs/ai/workflows/create-feature.md`

**Antes de escribir cualquier código:**
- `docs/ai/workflows/implementation-hygiene.md`

**Después de que una feature esté implementada y mergeada:**
- `docs/ai/workflows/archive-feature.md`
