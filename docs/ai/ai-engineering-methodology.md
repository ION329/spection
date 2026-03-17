# Spection — Metodología de Desarrollo Guiado por Especificación

Versión 2.1

Spection es una metodología de desarrollo donde la especificación es la fuente de verdad.
El código es una consecuencia directa de la documentación, no al revés.
La IA actúa como el motor de documentación. El ingeniero actúa como el director del sistema.

---

## Principios Fundamentales

### La documentación es el sistema

Todo el conocimiento sobre el proyecto vive en `docs/`.
Esto incluye arquitectura, definición de producto, features, especificaciones de ingeniería, decisiones y workflows.
Nada que sea importante vive solo en la cabeza de alguien o en un historial de chat.

### El código es una consecuencia

La implementación comienza solo después de que la especificación esté completa y validada.
Una feature sin spec no se codifica.
Una spec sin detalle de ingeniería no se desglosa en tareas.
Una lista de tareas sin un contexto limpio no se ejecuta.

### La IA genera, los ingenieros validan

La IA es responsable de:
- generar documentación a partir de prompts
- estructurar especificaciones usando plantillas
- expandir el detalle técnico
- mantener la consistencia entre documentos

El ingeniero es responsable de:
- dirigir el análisis
- validar cada salida de la IA antes de que avance a la siguiente fase
- tomar decisiones de arquitectura y producto
- aprobar la transición entre fases

### Inicio mínimo, crecimiento orgánico

Los repositorios comienzan solo con:
```
docs/
README.md
```

Las carpetas de código (`backend/`, `frontend/`, `services/`) aparecen solo cuando comienza la implementación.
Ninguna carpeta se crea de forma especulativa.

### Higiene estricta de contexto para implementación

Cada sesión de implementación debe comenzar con un contexto limpio.
Carga solo la spec de ingeniería y el archivo de tareas de la feature que se está codificando.
No cargues documentos de producto, visiones generales de arquitectura o specs no relacionadas en una sesión de implementación.
Un contexto contaminado degrada la calidad del código y causa desviación de la especificación.

---

## Estructura del Conocimiento

```
docs/
├── ai/       ← motor de la metodología: define cómo se comporta la IA en este proyecto
├── spec/     ← todo el pensamiento técnico del sistema (la única carpeta que evoluciona)
│   ├── product/      ← definición de producto y espacio del problema
│   ├── architecture/ ← arquitectura del sistema y stack tecnológico
│   ├── features/     ← especificaciones funcionales por feature
│   ├── engineering/  ← contratos técnicos implementables por feature
│   ├── tasks/        ← desgloses de tareas ordenados por dependencias
│   └── decisions/    ← ADRs: cada decisión técnica significativa registrada como regla vinculante para la IA
├── public/   ← documentación simplificada para stakeholders y desarrolladores externos
└── lab/      ← experimentos, investigación e historial de features archivadas
```

`docs/ai/` es el motor de la metodología. Su contenido define cómo se comporta la IA en este proyecto.
`docs/spec/` contiene toda la documentación específica del proyecto generada por la IA y validada por el ingeniero.
`docs/spec/decisions/` es especialmente crítica: cada ADR con `status: accepted` es una restricción vinculante que la IA debe respetar en todas las sesiones de arquitectura e ingeniería. No son sugerencias.
`docs/spec/` es la única carpeta que cambia conforme el proyecto evoluciona.

---

## Secuencia de Fases

```
Descubrimiento → Arquitectura → Specs de Features → Specs de Ingeniería → Tareas → Implementación
```

Cada fase produce un documento. Cada documento debe ser validado por el ingeniero antes de que comience la siguiente fase.
Ninguna fase puede ser omitida. Ninguna fase puede revertirse sin revisar todos los documentos derivados.

---

## Roles

### Ingeniero (Director del Sistema)
- guía el análisis y el pensamiento de producto
- valida todas las salidas de la IA
- aprueba las transiciones entre fases
- toma todas las decisiones de arquitectura y producto
- es el único que puede marcar una spec como lista para implementación

### IA (Motor de Documentación)
- genera documentación a partir de prompts
- hace preguntas de clarificación antes de especificar
- sigue las plantillas de forma exacta
- guarda las salidas en las rutas especificadas
- nunca inventa tecnologías, patrones o requisitos no aprobados explícitamente

---

## Archivos canónicos

| Archivo | Propósito |
|---|---|
| `docs/ai/ai-engineering-methodology.md` | Este documento. El motor de la metodología. |
| `docs/ai/rules/constitution.md` | Principios de ingeniería no negociables. |
| `docs/ai/workflows/init-project.md` | Punto de entrada para proyectos nuevos. |
| `docs/spec/architecture/architecture.md` | La arquitectura del sistema de este proyecto. |
