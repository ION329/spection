# Workflow: Ingeniería Inversa de un Proyecto Existente (Brownfield)

Usa este workflow cuando heredas un monolito, repositorio legacy o cualquier base de código
sin documentación técnica formal. Su propósito es generar la capa de especificación que
debería haber existido desde el inicio, antes de añadir cualquier código nuevo.

**No ejecutes `create-feature.md` sobre código existente sin haber completado al menos
las Fases 1 y 2 de este workflow.** Añadir features a un sistema no documentado produce
deuda técnica compuesta y contradicciones entre el código nuevo y el legado.

---

## Prerequisitos

Antes de comenzar, confirma que tienes acceso a:

- [ ] El repositorio completo del proyecto (lectura de todos los archivos)
- [ ] Archivos de configuración de dependencias (`package.json`, `composer.json`, `requirements.txt`, `Gemfile`, `pom.xml`, o equivalente)
- [ ] Esquema de base de datos o migraciones existentes
- [ ] Enrutadores o archivos de rutas principales
- [ ] Al menos un entorno funcional donde el sistema corre (para validar los flujos deducidos)

Si no tienes acceso al repositorio completo, detente. La ingeniería inversa parcial produce
arquitecturas incompletas que son peor que no tener documentación.

---

## Fase 1 — Escaneo de Código y Arquitectura Base

**Agente:** `docs/ai/agents/software-architect.md`

El objetivo de esta fase es reconstruir la arquitectura real del sistema leyendo el código,
no la arquitectura que alguien creyó que tenía o la que está descrita en un wiki desactualizado.

1. Abre una sesión nueva de IA
2. Carga el agente `docs/ai/agents/software-architect.md`
3. Indica al agente que el contexto es ingeniería inversa sobre un repositorio existente
4. El agente debe leer, en este orden:
   - Archivos de configuración de dependencias — para identificar el stack tecnológico real
   - Archivos de configuración de entorno (`.env.example`, `docker-compose.yml`, `config/`) — para identificar servicios externos y variables críticas
   - Esquema de base de datos o migraciones — para reconstruir el modelo de datos
   - Enrutadores o archivos de rutas principales — para mapear los límites del sistema
   - Modelos o entidades del dominio — para identificar las abstracciones principales
5. El agente generará:
   - `docs/spec/architecture/architecture.md` — con el stack real, modelo de datos deducido y estrategia de seguridad existente (aunque sea implícita)
   - `docs/spec/decisions/ADR-[NNN]-[decision].md` — un ADR por cada decisión técnica significativa ya tomada en el código (motor de BD, framework principal, estrategia de autenticación, etc.)
6. Los ADRs de ingeniería inversa deben generarse con `status: accepted` ya que son decisiones existentes, no propuestas
7. Ejecuta `docs/ai/prompts/review.md` sobre la arquitectura generada antes de validar

> **PUERTA 1 — Aprobación humana requerida**
> Revisa las **Notas de Revisión** al final del documento.
> Si la revisión arroja notas *críticas*, no valides. Devuelve el documento al agente creador con el prompt:
> *"Por favor corrige los problemas críticos listados en las notas de revisión"*, y vuelve a revisar.
> Solo cuando no haya notas críticas: añade `**Status: Validated**` al inicio de `docs/spec/architecture/architecture.md`.
> Verifica que cada ADR generado tiene `status: accepted` y describe una decisión real del sistema.
> No avances a la Fase 2 hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/software-architect.md` → sección Handoff.

---

## Fase 2 — Ingeniería Inversa de Producto

**Agente:** `docs/ai/agents/product-strategist.md`

El objetivo de esta fase es deducir el modelo de producto implícito que existe en el código:
quiénes son los usuarios, qué problemas resuelve el sistema y cuáles son los flujos principales,
todo a partir del comportamiento real del sistema, no de suposiciones.

1. Abre una sesión nueva de IA
2. Carga el agente `docs/ai/agents/product-strategist.md`
3. Indica al agente que el contexto es ingeniería inversa y que `docs/spec/architecture/architecture.md` tiene `**Status: Validated**`
4. El agente debe leer:
   - `docs/spec/architecture/architecture.md` — para entender el sistema técnico
   - Archivos de vistas, plantillas o componentes de cliente — para deducir los flujos del usuario real
   - Archivos de rutas con sus verbos HTTP — para identificar las acciones disponibles por actor
   - Cualquier archivo de roles, permisos o guards — para identificar los tipos de usuario existentes
5. El agente generará `docs/spec/product/product.md` con:
   - Tipos de usuario deducidos del sistema (no inventados)
   - Flujos principales existentes (lo que el sistema realmente hace hoy)
   - Declaración del problema que el sistema resuelve (deducida del comportamiento)
   - Alcance actual vs. áreas donde el sistema está claramente incompleto o inconsistente
6. Ejecuta `docs/ai/prompts/review.md` sobre el documento de producto antes de validar

> **PUERTA 2 — Aprobación humana requerida**
> Revisa las **Notas de Revisión** al final del documento.
> Si la revisión arroja notas *críticas*, no valides. Devuelve el documento al agente creador con el prompt:
> *"Por favor corrige los problemas críticos listados en las notas de revisión"*, y vuelve a revisar.
> Solo cuando no haya notas críticas: añade `**Status: Validated**` al inicio de `docs/spec/product/product.md`.
> Verifica que el documento describe el sistema real, no el sistema ideal o deseado.
> No avances a la Fase 3 hasta completar este paso.
> Criterios de aceptación: `docs/ai/agents/product-strategist.md` → sección Handoff.

---

## Fase 3 — Extracción de Features Activas

**Agente:** `docs/ai/agents/systems-engineer.md`

El objetivo de esta fase es mapear los módulos del código existente a especificaciones de
features aisladas y documentadas. Cada feature documentada aquí representa funcionalidad
que ya existe en producción, no funcionalidad planeada.

1. Abre una sesión nueva de IA
2. Carga el agente `docs/ai/agents/systems-engineer.md`
3. Indica al agente que el contexto es extracción de features existentes, no diseño de features nuevas
4. El agente debe leer:
   - `docs/spec/product/product.md` — para mantenerse dentro del alcance del sistema real
   - `docs/spec/architecture/architecture.md` — para respetar las restricciones técnicas documentadas
   - Los módulos, controladores y servicios del repositorio — para mapear responsabilidades reales
5. El agente generará un archivo `docs/spec/features/[feature-name]-spec.md` por cada módulo o conjunto de funcionalidades cohesionado que identifique
6. Las specs de features de ingeniería inversa deben documentar el comportamiento actual, incluyendo:
   - Flujos de error existentes (aunque no estén bien manejados)
   - Reglas de negocio implícitas detectadas en el código
   - Deuda técnica o comportamientos inconsistentes observados (anotar como notas, no como requisitos)
7. Ejecuta `docs/ai/prompts/review.md` sobre cada spec antes de validar

> **PUERTA 3 — Aprobación humana requerida (por cada feature documentada)**
> Revisa las **Notas de Revisión** al final de cada documento.
> Si la revisión arroja notas *críticas*, no valides. Devuelve el documento al agente creador con el prompt:
> *"Por favor corrige los problemas críticos listados en las notas de revisión"*, y vuelve a revisar.
> Solo cuando no haya notas críticas: añade `**Status: Validated**` al inicio de cada `docs/spec/features/[feature-name]-spec.md`.
> Una feature sin validación no puede ser modificada ni extendida con `create-feature.md`.
> Criterios de aceptación: `docs/ai/agents/systems-engineer.md` → sección Handoff.

---

## Regla de Transición — Cuándo puedes usar `create-feature.md`

> ⚠️ **Esta regla es estricta y no tiene excepciones.**

Para iniciar cualquier flujo de `docs/ai/workflows/create-feature.md` sobre este repositorio,
deben estar validadas **obligatoriamente** las siguientes condiciones:

| Condición | Archivo | Estado requerido |
|---|---|---|
| Arquitectura documentada | `docs/spec/architecture/architecture.md` | `**Status: Validated**` |
| Producto documentado | `docs/spec/product/product.md` | `**Status: Validated**` |
| ADRs de decisiones existentes | `docs/spec/decisions/ADR-*.md` | `status: accepted` en todos |

La Fase 3 (features existentes) es recomendada antes de añadir features nuevas, pero no bloquea
la creación de features nuevas si las Fases 1 y 2 están validadas.

**Añadir una feature nueva a un sistema cuya arquitectura no está documentada es la causa
más común de regresiones y deuda técnica compuesta en proyectos brownfield.**

---

## Resumen de archivos generados

```
docs/spec/
├── architecture/
│   └── architecture.md                     ← Status: Validated  (Fase 1)
├── decisions/
│   ├── ADR-001-[decision-existente].md     ← status: accepted   (Fase 1)
│   └── ADR-002-[decision-existente].md     ← status: accepted   (Fase 1)
├── product/
│   └── product.md                          ← Status: Validated  (Fase 2)
└── features/
    ├── [feature-existente]-spec.md         ← Status: Validated  (Fase 3)
    └── [feature-existente]-spec.md         ← Status: Validated  (Fase 3)
```
