# Prompt: Feature Specification

## 1. Rol

Carga y aplica las instrucciones definidas en `docs/ai/agents/systems-engineer.md`.
Ese archivo define tu rol, el paso de clarificación obligatorio y los criterios de entrega. Léelo antes de continuar.

## 2. Prerequisito de entrada

Antes de leer cualquier otro archivo, verifica que `docs/spec/architecture/architecture.md` contiene
la línea `**Status: Validated**` al inicio del documento.

Si no está validado: detente y comunica al ingeniero que la arquitectura debe estar validada
antes de especificar features. No generes nada.

## 3. Contexto a leer

Lee los siguientes archivos en este orden:

1. `docs/ai/rules/constitution.md` — principios rectores obligatorios
2. `docs/ai/agents/systems-engineer.md` — tu rol y el protocolo de clarificación
3. `docs/spec/architecture/architecture.md` — fuente primaria para identificar las features
4. `docs/spec/product/product.md` — contexto de producto para no contradecir requisitos
5. `docs/spec/decisions/*.md` — todos los ADRs con `status: accepted`
6. `docs/spec/features/` — leer specs existentes para no duplicar features ya definidas

## 4. Paso de clarificación (obligatorio y bloqueante)

No generes ninguna especificación sin antes ejecutar este paso.

Identifica las features que vas a especificar a partir de la arquitectura.
Para cada feature que vayas a especificar, presenta al ingeniero las siguientes preguntas
en una sola ronda. Espera todas las respuestas antes de continuar.

**Para la feature "[nombre de la feature]":**

1. ¿Cuál es el comportamiento exacto en el flujo principal?
2. ¿Qué ocurre si el usuario envía datos vacíos, inválidos o malformados?
3. ¿Qué ocurre si el recurso solicitado no existe o ya fue eliminado?
4. ¿Hay límites de volumen, frecuencia o tamaño que deba respetar?
5. ¿Qué estados puede tener la entidad principal y qué transiciones son válidas?
6. ¿Esta feature depende de servicios externos? ¿Cuáles exactamente?
7. ¿Qué comportamientos están explícitamente fuera del alcance de esta feature?

Si hay múltiples features, agrupa las preguntas por feature en una sola ronda.
No inicies la especificación hasta recibir respuestas para todas las features.

## 5. Tarea

Una vez recibidas las respuestas de clarificación, genera una especificación por cada feature.
Una feature = un archivo. No combines múltiples features en un solo archivo.
Si una feature es demasiado grande, divídela y consulta al ingeniero antes de continuar.

## 6. Template obligatorio

Usa exactamente la estructura de `docs/ai/templates/feature-template.md`.
Lee los comentarios `<!-- Instrucción: ... -->` del template y sígelos al pie de la letra.
Incorpora las respuestas del paso de clarificación en las secciones correspondientes:
- Casos límite → Business Rules y User Flow (flujos de error)
- Estados y transiciones → States and Transitions
- Dependencias externas → Dependencies

## 7. Output

- **Ruta:** `docs/spec/features/[feature-name]-spec.md`
- **Convención de nombres:** kebab-case, sufijo `-spec`
  - Correcto: `user-authentication-spec.md`, `payment-processing-spec.md`
  - Incorrecto: `UserAuth.md`, `feature1.md`, `auth spec.md`
- **Una feature = un archivo**, sin excepciones

Confirma el nombre y la ruta de cada archivo antes de escribirlo.
Al terminar todas las features, lista los archivos generados con sus rutas completas.
