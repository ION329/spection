# Workflow: Higiene de Implementación

Esta es una regla de obligatorio cumplimiento. No es opcional ni negociable.
Ejecuta este protocolo antes de escribir una sola línea de código de cualquier feature.

El principio es simple: el contexto contaminado produce código contaminado.
Una sesión de IA que ha procesado documentos de producto, arquitecturas y múltiples features
razona diferente a una sesión enfocada únicamente en implementar una cosa concreta.
La higiene de contexto es la diferencia entre un LLM que genera código preciso
y uno que alucina patrones de otras features o contradice los contratos de la spec de ingeniería.

---

## Protocolo paso a paso

### Paso 1 — Verificar prerequisitos

Antes de abrir cualquier sesión, confirma que existen los siguientes archivos y tienen `**Status: Validated**`:

- [ ] `docs/spec/engineering/[feature-name]-engineering.md`
- [ ] `docs/spec/tasks/[feature-name]-tasks.md` (no necesita validación, solo debe existir)

Si la spec de ingeniería no está validada, detente. No hay implementación sin spec validada.
Vuelve al workflow `create-feature.md` y completa la Puerta 2.

### Paso 2 — Cerrar todo

- [ ] Cierra todas las pestañas o sesiones de IA activas
- [ ] Cierra cualquier chat o conversación en curso, sin importar el tema
- [ ] No uses "continuar conversación" ni "resumir contexto anterior"

No hay excepciones. Una sesión "casi limpia" no es una sesión limpia.

### Paso 3 — Abrir una sesión nueva

- [ ] Abre una sesión completamente nueva en tu herramienta de IA (Cursor, Claude, Windsurf, etc.)
- [ ] No cargues ningún archivo todavía

### Paso 4 — Cargar el contexto de implementación

Carga los archivos en este orden exacto y ningún otro:

1. **`docs/ai/rules/constitution.md`** — las reglas de calidad de código (sección III) e higiene de contexto (sección V)
2. **`docs/spec/engineering/[feature-name]-engineering.md`** — los contratos técnicos de esta feature
3. **`docs/spec/tasks/[feature-name]-tasks.md`** — las tareas ordenadas por dependencias
4. **ADRs relevantes** — únicamente los `docs/spec/decisions/ADR-*.md` con `status: accepted` que afecten esta feature

**No cargues ninguno de los siguientes:**

| Archivo | Motivo para no cargarlo |
|---|---|
| `docs/spec/product/product.md` | Nivel de abstracción demasiado alto para implementación |
| `docs/spec/architecture/architecture.md` | Ya está destilado en la spec de ingeniería y los ADRs |
| `docs/spec/features/[feature]-spec.md` | Ya está destilado en la spec de ingeniería |
| Specs de otras features | Contexto innecesario que introduce ruido y confusión |
| `docs/ai/ai-engineering-methodology.md` | Metodología, no implementación |

### Paso 5 — Iniciar la implementación

Con el contexto cargado, indica a la IA:

```
Lee el archivo de tareas. Identifica la primera tarea con estado: pendiente que no tenga
dependencias sin resolver. Implementa esa tarea siguiendo los contratos de la spec de ingeniería.
No implementes más de una tarea por prompt.
```

Trabaja tarea por tarea. Actualiza el `estado` de cada tarea a `completada` en el archivo de tareas
antes de pasar a la siguiente.

### Paso 6 — Gestión de sesión durante implementación

- Si la sesión se vuelve lenta o incoherente: cierra y abre una sesión nueva con el mismo contexto
- Si necesitas consultar algo de la feature spec o la arquitectura: hazlo en una sesión separada, no en la sesión de implementación
- Si descubres que la spec de ingeniería tiene un error: detente, corrígelo con el prompt `docs/ai/prompts/review.md`, valida el cambio con el ingeniero, y reinicia la sesión de implementación

---

## Regla de oro

> Una sesión de implementación contiene exactamente tres cosas:
> la constitución, la spec de ingeniería de la feature, y el archivo de tareas de la feature.
> Todo lo demás es ruido.
