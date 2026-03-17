# Workflow: Archivar Feature

Ejecuta este workflow cuando una feature está completamente implementada, testeada y mergeada.
Su propósito es mantener `docs/spec/` limpio y activo, moviendo la documentación de trabajo
ya consumida a `docs/lab/history/`.

Un directorio `docs/spec/` con specs viejas de features ya implementadas es ruido cognitivo.
Contamina las sesiones de IA con contexto obsoleto y dificulta encontrar lo que está activo.

---

## Prerequisitos

Antes de archivar, confirma que la feature cumple estos criterios:

- [ ] El código está mergeado en la rama principal
- [ ] Las pruebas pasan en CI
- [ ] La feature fue revisada y aprobada (revisión de código completa)
- [ ] Si aplica: la documentación pública fue generada (`docs/ai/workflows/` → Escritor Técnico)

Si algún punto no está cumplido, no archives todavía.

---

## Paso 1 — Preparar el registro histórico

Antes de mover archivos, abre `docs/lab/history/index.md`.
Si no existe, créalo con esta estructura:

```markdown
# Índice del Historial

| Feature | Fecha de archivo | Spec de Ingeniería | Archivo de Tareas | Notas |
|---|---|---|---|---|
```

Añade una fila con los datos de la feature que vas a archivar:

| Campo | Valor |
|---|---|
| Feature | nombre de la feature en kebab-case |
| Fecha de archivo | fecha actual en formato YYYY-MM-DD |
| Spec de Ingeniería | ruta original del archivo |
| Archivo de Tareas | ruta original del archivo |
| Notas | cualquier observación relevante (deuda técnica pendiente, decisiones tomadas durante implementación, etc.) |

### Paso 2 — Mover la spec de ingeniería

Mueve el archivo:
```
docs/spec/engineering/[feature-name]-engineering.md
→
docs/lab/history/[feature-name]-engineering.md
```

### Paso 3 — Mover el archivo de tareas

Mueve el archivo:
```
docs/spec/tasks/[feature-name]-tasks.md
→
docs/lab/history/[feature-name]-tasks.md
```

### Paso 4 — Decidir sobre la feature spec

La feature spec en `docs/spec/features/[feature-name]-spec.md` tiene valor de referencia
a largo plazo. No se archiva automáticamente.

Evalúa con el ingeniero:

- **Mantener en `docs/spec/features/`** si la feature puede ser modificada o extendida en el futuro
- **Archivar en `docs/lab/history/`** si la feature es definitivamente estable y no se tocará

Si decides archivar la feature spec, muévela igual que los pasos 2 y 3.

### Paso 5 — Verificar que `docs/spec/` solo tiene specs activas

Después de mover los archivos, revisa:

- [ ] `docs/spec/engineering/` — solo contiene features pendientes de implementar
- [ ] `docs/spec/tasks/` — solo contiene features pendientes de implementar
- [ ] `docs/spec/features/` — contiene solo features activas o modificables
- [ ] `docs/lab/history/index.md` — tiene la fila de la feature recién archivada

### Paso 6 — Commit del archivado

Haz un commit específico para el archivado con el mensaje:

```
archive: mover specs de [feature-name] a lab/history

Feature implementada y testeada. Spec de ingeniería y archivo de tareas archivados.
```

---

## Cuándo NO archivar

No archives si:

- La feature tiene deuda técnica documentada que requiere una iteración futura
- Hay un bug conocido que producirá una nueva feature spec derivada
- La feature está parcialmente implementada (solo archiva cuando está 100% completa)

En estos casos, añade una nota en `docs/lab/history/index.md` con el estado real
y espera a que la situación esté resuelta.

---

## Estado esperado tras el archivado

```
docs/spec/          ← solo specs activas, pendientes de implementar
docs/lab/
└── history/
    ├── index.md                              ← registro de todo lo archivado
    ├── [feature-name]-engineering.md
    └── [feature-name]-tasks.md
```
