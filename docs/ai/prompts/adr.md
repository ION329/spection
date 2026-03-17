# Prompt: Registro de Decisión de Arquitectura

## 1. Rol

Carga y aplica las instrucciones definidas en `docs/ai/agents/software-architect.md`.
En este contexto específico, tu función es documentar decisiones técnicas ya tomadas o en evaluación.
Léelo antes de continuar.

## 2. Prerequisito de entrada

El ingeniero debe describir la decisión técnica a registrar antes de que comiences.
Si el ingeniero no ha descrito la decisión, pregunta:

- ¿Qué decisión técnica se debe registrar?
- ¿Ya fue tomada o está en evaluación?
- ¿Qué alternativas fueron consideradas?

No generes el ADR hasta tener esta información.

## 3. Contexto a leer

Lee los siguientes archivos en este orden:

1. `docs/ai/rules/constitution.md` — sección VI define las reglas de los ADRs
2. `docs/ai/agents/software-architect.md` — tu rol en este proceso
3. `docs/spec/decisions/` — lee todos los ADRs existentes para:
   - Asignar el ID correcto (siguiente número en la secuencia)
   - Verificar que la nueva decisión no contradice un ADR ya aceptado
   - Verificar que no existe ya un ADR para la misma decisión

Si la nueva decisión contradice un ADR aceptado, no generes el nuevo ADR todavía.
Informa al ingeniero del conflicto y espera instrucciones.

## 4. Tarea

Documenta la decisión técnica con objetividad. Sigue estas reglas:

- El campo `rule` del YAML debe ser una instrucción ejecutable en una sola oración que cualquier
  IA pueda seguir en el futuro sin contexto adicional. Ejemplo: `"Siempre usar PostgreSQL. Nunca usar MongoDB."`
- La sección Opciones Consideradas debe tener mínimo 2 alternativas genuinamente evaluadas.
  No incluyas opciones descartadas trivialmente.
- La sección Consecuencias debe documentar los trade-offs negativos con honestidad.
  Un ADR sin consecuencias negativas no es creíble.
- Si esta decisión reemplaza a una anterior, identifica el ADR que reemplaza y actualiza
  ese ADR anterior cambiando su campo `status` a `superseded`.

## 5. Plantilla obligatoria

Usa exactamente la estructura de `docs/ai/templates/adr-template.md`.
La cabecera YAML es obligatoria. No elimines ni renombres ningún campo del YAML.
Lee los comentarios `<!-- Instrucción: ... -->` de la plantilla y síguelos al pie de la letra.

## 6. Output

- **Ruta:** `docs/spec/decisions/ADR-[NNN]-[titulo-en-kebab-case].md`
- **Convención de IDs:** números secuenciales con ceros a la izquierda, tres dígitos
  - Correcto: `ADR-001`, `ADR-002`, `ADR-013`
  - Incorrecto: `ADR-1`, `ADR-01`, `ADR1`
- **Convención de nombres:** kebab-case descriptivo del tema de la decisión
  - Correcto: `ADR-001-use-postgresql.md`, `ADR-002-use-react-query.md`
  - Incorrecto: `ADR-001-decision.md`, `ADR-001-database.md`

Antes de escribir, confirma el ID asignado al ingeniero para evitar colisiones.
Si actualizas un ADR existente a `status: superseded`, confirma la ruta del archivo modificado.

Al finalizar, lista todos los archivos creados o modificados con sus rutas completas.
