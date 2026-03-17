# Constitución de Spection

Estos son los principios no negociables que gobiernan todas las decisiones de ingeniería en este proyecto.
Cada ingeniero y cada sesión de IA debe respetar estas reglas sin excepción.
Cuando haya dudas, consulta este documento antes de proceder.

---

## I. Integridad de la Especificación

**La spec es la fuente de verdad.**
Si el código contradice la spec, el código está mal — no la spec.
Si la spec necesita cambiar, actualiza la spec primero, luego actualiza el código.

**Ninguna feature se implementa sin una spec validada.**
Una solicitud de feature, un acuerdo verbal o un mensaje de chat no es una spec.
La feature no existe hasta que `docs/spec/features/[feature]-spec.md` exista y esté validada.

**Ninguna fase puede ser omitida.**
La secuencia es: Descubrimiento → Arquitectura → Spec de Feature → Spec de Ingeniería → Tareas → Implementación.
Saltarse una fase para avanzar más rápido siempre produce retrabajo. No está permitido.

---

## II. Reglas de Comportamiento de la IA

**La IA no debe alucinar tecnologías.**
La IA solo puede recomendar o usar tecnologías explícitamente presentes en:
- `docs/spec/architecture/architecture.md`
- Un ADR con `status: accepted` en `docs/spec/decisions/`

Si la IA no está segura del stack aprobado, debe preguntar antes de generar.

**La IA debe seguir las plantillas de forma exacta.**
Todos los documentos generados deben usar las plantillas en `docs/ai/templates/`.
Ninguna sección puede omitirse sin la aprobación explícita del ingeniero.

**La IA debe guardar la salida en la ruta especificada.**
Cada prompt define una ruta de salida. La IA debe usar esa ruta.
No debe inventar rutas o nombres de archivo alternativos.

**La IA debe preguntar antes de especificar.**
En la fase de especificación de feature, la IA está obligada a hacer preguntas de clarificación
antes de generar una spec. Este paso es obligatorio y no puede omitirse.

**La IA no debe modificar documentos validados sin instrucción.**
Una vez que el ingeniero ha validado un documento, la IA no debe alterarlo
a menos que el ingeniero solicite explícitamente una revisión.

---

## III. Estándares de Calidad de Código

**Cada función debe hacer una sola cosa.**
Las funciones con múltiples responsabilidades deben dividirse antes de hacer merge.

**No se permiten valores mágicos en el código.**
Todas las constantes deben tener nombre y estar documentadas. No se permiten cadenas de texto, números o URLs hardcodeados en la lógica de negocio.

**No hay implementación sin un plan de pruebas correspondiente.**
Cada spec de ingeniería debe incluir una sección que describa cómo se probará la feature.
El archivo de tareas debe incluir al menos una tarea de prueba.

**La seguridad no es opcional.**
Autenticación, autorización, validación de entradas y sanitización de datos no son features.
Son requisitos en cada endpoint y cada input del usuario.
Deben aparecer en la spec de ingeniería, no ser añadidos como algo secundario.

---

## IV. Puertas de Validación

**El ingeniero es el único que puede aprobar una transición de fase.**
La IA genera. El ingeniero valida. La validación no es automática.

**Un documento no está validado hasta que el ingeniero lo marque explícitamente como tal.**
El ingeniero señala la validación mediante:
- Añadir `**Status: Validated**` al inicio del documento, o
- Avanzar el workflow mediante una instrucción explícita

**Las notas de revisión deben resolverse antes de avanzar.**
Si existe una sección `## Review Notes` en una spec con ítems `critical` sin resolver,
esa spec no puede avanzar a la siguiente fase.

---

## V. Higiene de Contexto

**Cada sesión de implementación comienza con un contexto limpio.**
Antes de codificar, cierra todos los chats de IA activos. Abre una sesión nueva.
Carga solo:
1. `docs/spec/engineering/[feature]-engineering.md`
2. `docs/spec/tasks/[feature]-tasks.md`
3. ADRs con `status: accepted` relevantes para la feature

**No cargues documentos de producto, visiones generales de arquitectura o specs no relacionadas en una sesión de implementación.**
El contexto de alto nivel contamina el razonamiento a nivel de implementación y degrada la calidad de la salida.

---

## VI. Registros de Decisiones de Arquitectura

**Cada decisión técnica significativa debe registrarse como un ADR.**
Una decisión es significativa si:
- afecta el stack tecnológico
- cambia un modelo de datos
- introduce una nueva dependencia externa
- contradice o reemplaza una decisión anterior

**Los ADRs son inmutables una vez aceptados.**
Un ADR aceptado nunca se edita. Si una decisión cambia, se crea un nuevo ADR
con `supersedes: ADR-[id-anterior]` y el anterior se actualiza a `status: superseded`.

**La IA debe cargar los ADRs aceptados al inicio de cada sesión de arquitectura o ingeniería.**
Las reglas definidas en los ADRs son restricciones vinculantes, no sugerencias.
