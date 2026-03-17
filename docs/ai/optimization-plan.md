# Spection Optimization Plan

## AI Engineering Bootstrap v2 → Spec-Driven Development

**Objetivo:** Evolucionar el framework actual hacia una metodología definitiva y agnóstica llamada **Spection**, donde la IA actúa como motor de documentación y el ingeniero humano como director, con separación estricta entre especificación y código.

---

## Fase 1: Corrección de Vulnerabilidades Base (Gobernanza)

### 1.1 Crear la Constitución del sistema

- [ ] **Crear `docs/ai/rules/constitution.md`**
  Documento de principios rectores que gobierna todas las decisiones técnicas del proyecto. Inspirado en el modelo "Constitution" de GitHub Spec Kit. Debe incluir: principios no negociables, reglas de colaboración humano-IA, criterios de aceptación de decisiones arquitectónicas, y qué tipo de cambios requieren un ADR obligatorio.

- [ ] **Crear `docs/ai/rules/` como carpeta oficial de gobernanza**
  Establecer esta carpeta como el directorio canónico para reglas del sistema. Futuras restricciones operacionales, convenciones de nomenclatura y políticas de versionado vivirán aquí.

### 1.2 Actualizar la plantilla ADR con cabecera YAML ejecutable

- [ ] **Modificar `docs/ai/templates/adr-template.md`**
  Añadir una cabecera YAML obligatoria al inicio del archivo con los campos:
  - `id`: identificador único del ADR (ej. `ADR-001`)
  - `status`: estado actual (`proposed` | `accepted` | `deprecated` | `superseded`)
  - `date`: fecha de la decisión
  - `rule`: instrucción ejecutable en una línea que la IA debe respetar en todos los contextos (ej. `"Always use PostgreSQL. Never use MongoDB."`)
  - `supersedes`: referencia a un ADR anterior si aplica

- [ ] **Documentar en `constitution.md` el protocolo de carga de ADRs**
  Añadir una regla que indique que antes de cada sesión de arquitectura, el ingeniero debe cargar todos los ADRs con `status: accepted` para que la IA respete las decisiones previas.

---

## Fase 2: Nuevos Flujos de Trabajo y Plantillas (El Puente al Código)

### 2.1 Incorporar el paso de Clarificación al Systems Engineer

- [ ] **Modificar `docs/ai/agents/systems-engineer.md`**
  Añadir una responsabilidad explícita: antes de generar cualquier especificación funcional, el Systems Engineer debe ejecutar una ronda de preguntas estructuradas al humano cubriendo: casos límite, comportamiento ante errores, reglas de negocio ambiguas, y restricciones de rendimiento o seguridad no documentadas.

- [ ] **Crear `docs/ai/prompts/clarification.md`**
  Prompt dedicado al paso de clarificación. Debe instruir a la IA a generar una lista numerada de preguntas estructuradas sobre el feature o arquitectura en análisis, agrupadas por categoría: funcionalidad, casos límite, integraciones, y restricciones no funcionales. La IA no debe avanzar a la especificación hasta recibir respuestas.

- [ ] **Actualizar `docs/ai/workflows/create-feature.md`**
  Insertar el paso de clarificación entre "Define feature goal" y "Generate feature specification", dejando explícito que es un paso bloqueante.

### 2.2 Crear la plantilla de tareas de ingeniería

- [ ] **Crear `docs/ai/templates/tasks-template.md`**
  Plantilla que el Lead Engineer completa antes de implementar. Estructura:
  - `feature`: referencia al archivo de especificación de origen
  - Lista de tareas ordenadas por dependencias con campos: `id`, `description`, `depends_on`, `type` (`backend` | `frontend` | `infra` | `test`), `status` (`pending` | `in-progress` | `done`)
  - Sección de notas de implementación y restricciones activas

- [ ] **Crear `docs/ai/prompts/task-breakdown.md`**
  Prompt que instruye a la IA a leer una especificación de ingeniería y descomponerla en tareas atómicas ordenadas por dependencias, generando el archivo de tareas usando `tasks-template.md`.

- [ ] **Modificar `docs/ai/agents/lead-engineer.md`**
  Añadir como responsabilidad obligatoria la generación del archivo de tareas antes de cualquier actividad de implementación. El Lead Engineer no entrega una especificación como output final, sino una especificación más un archivo de tareas listo para ejecutar.

### 2.3 Conectar los flujos con la codificación

- [ ] **Actualizar `docs/ai/workflows/init-project.md`**
  Extender el flujo más allá de la documentación. Añadir los pasos finales:
  - Paso 9: Run task breakdown prompt
  - Paso 10: Generate tasks file per feature
  - Paso 11: Begin implementation using engineering spec + tasks file

- [ ] **Actualizar `docs/ai/workflows/create-feature.md`**
  Extender el flujo para que no termine en la especificación de ingeniería. Añadir:
  - Paso 5: Run clarification prompt (bloqueante)
  - Paso 6: Run task breakdown prompt
  - Paso 7: Generate tasks file
  - Paso 8: Load engineering spec + tasks file in a clean context and begin coding

---

## Fase 3: Higiene y Mantenimiento (Prácticas de OpenSpec)

### 3.1 Crear el flujo de higiene de implementación

- [ ] **Crear `docs/ai/workflows/implementation-hygiene.md`**
  Regla estricta y protocolo paso a paso que el desarrollador debe seguir antes de empezar a programar cualquier feature. Debe incluir:
  - Paso 1: Cerrar todos los chats de IA activos (limpiar contexto contaminado)
  - Paso 2: Abrir una sesión nueva
  - Paso 3: Cargar únicamente el archivo de especificación de ingeniería final del feature (`docs/spec/engineering/[feature].md`)
  - Paso 4: Cargar el archivo de tareas correspondiente (`docs/spec/tasks/[feature]-tasks.md`)
  - Paso 5: Cargar únicamente los ADRs con `status: accepted` relevantes
  - Paso 6: No cargar ningún otro documento de spec, product o arquitectura de alto nivel
  - Justificación: el contexto contaminado con documentación de alto nivel degrada la calidad del código generado

- [ ] **Referenciar `implementation-hygiene.md` desde `constitution.md`**
  Añadir en la constitución una regla que declare este flujo como obligatorio para toda implementación, sin excepciones.

### 3.2 Crear el flujo de archivado de features implementadas

- [ ] **Crear `docs/ai/workflows/archive-feature.md`**
  Proceso estándar para archivar especificaciones ya implementadas. Pasos:
  - Paso 1: Confirmar que el feature está completamente implementado y testeado
  - Paso 2: Mover el archivo de ingeniería de `docs/spec/engineering/` a `docs/lab/history/`
  - Paso 3: Mover el archivo de tareas de `docs/spec/tasks/` a `docs/lab/history/`
  - Paso 4: Actualizar el archivo de arquitectura si el feature modificó la estructura del sistema
  - Paso 5: Registrar en un `docs/lab/history/index.md` la fecha, el feature archivado y el estado final
  - Objetivo: mantener `docs/spec/` únicamente con especificaciones activas y pendientes de implementar

- [ ] **Crear `docs/lab/history/index.md`**
  Registro histórico de features implementadas. Estructura tabular con columnas: feature, fecha de implementación, archivos archivados, notas.

---

## Fase 4: Empaquetado y CLI (Spection Init)

### 4.1 Diseñar la estructura del paquete CLI

- [ ] **Crear `docs/spec/engineering/spection-cli.md`**
  Especificación de ingeniería completa del CLI. Debe definir:
  - Nombre del comando: `spection`
  - Subcomandos iniciales: `init`, `add-agent`, `add-workflow`, `add-template`
  - Comportamiento de `spection init`: detectar si el repositorio es nuevo o legacy, crear la estructura de carpetas, inyectar todos los archivos base (prompts, agents, templates, workflows, constitution)
  - Flags: `--lang` para elegir idioma de los archivos generados, `--minimal` para instalar solo la estructura base sin contenido, `--force` para sobreescribir en repos legacy
  - Output esperado: árbol de archivos creados y mensaje de siguiente paso apuntando a `init-project.md`

- [ ] **Crear `docs/spec/tasks/spection-cli-tasks.md`**
  Desglose de tareas de implementación del CLI usando `tasks-template.md`:
  - Tarea: inicializar proyecto Node.js o Python con estructura de paquete CLI
  - Tarea: implementar comando `init` con generación de árbol de carpetas
  - Tarea: implementar copia de archivos base desde templates embebidos en el paquete
  - Tarea: implementar detección de repo legacy vs nuevo
  - Tarea: implementar flag `--minimal`
  - Tarea: escribir tests de integración para cada subcomando
  - Tarea: configurar publicación en npm y/o PyPI

### 4.2 Definir la estructura de carpetas que `spection init` genera

- [ ] **Documentar en `spection-cli.md` el árbol de salida exacto**
  El comando `spection init` debe generar la siguiente estructura mínima:

  ```
  docs/
    ai/
      agents/
      prompts/
      templates/
      workflows/
      rules/
    spec/
      product/
      architecture/
      features/
      engineering/
      tasks/
    public/
    lab/
      history/
  README.md
  ```

### 4.3 Preparar los assets embebidos del CLI

- [ ] **Crear `docs/spec/architecture/spection-cli-architecture.md`**
  Documentar la estrategia de empaquetado de los archivos base: los prompts, agents, templates y workflows del framework vivirán como archivos estáticos dentro del paquete CLI y se copiarán al proyecto destino durante `spection init`.

- [ ] **Definir el mecanismo de actualización**
  Documentar en la especificación cómo un proyecto existente puede actualizar sus archivos base cuando salga una nueva versión de Spection (ej. `spection update --templates`, `spection update --prompts`) sin sobreescribir los archivos personalizados del proyecto.

### 4.4 Validar completitud antes de publicar

- [ ] **Crear checklist de publicación en `docs/spec/engineering/spection-cli.md`**
  Sección final del spec con los criterios de aceptación antes del primer release:
  - [ ] `spection init` funciona en un repositorio vacío
  - [ ] `spection init` funciona en un repositorio legacy con archivos existentes
  - [ ] Todos los prompts, agents, templates y workflows se copian correctamente
  - [ ] El README generado apunta a `docs/ai/workflows/init-project.md`
  - [ ] El paquete es instalable via `npx spection init` sin instalación previa
  - [ ] Documentación de uso publicada en `docs/public/`

---

## Orden de ejecución recomendado

1. Fase 1 completa — establece las reglas antes de cualquier cambio
2. Fase 2.2 (tasks-template) — necesaria para ejecutar Fase 2.3
3. Fase 2.1 (clarification) — independiente, puede ir en paralelo con 2.2
4. Fase 2.3 (actualizar flujos) — depende de 2.1 y 2.2
5. Fase 3 completa — independiente de Fase 2
6. Fase 4 completa — depende de que todas las fases anteriores estén cerradas
