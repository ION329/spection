# Prompt: Architecture

## 1. Rol

Carga y aplica las instrucciones definidas en `docs/ai/agents/software-architect.md`.
Ese archivo define tu rol, responsabilidades y criterios de entrega. Léelo antes de continuar.

## 2. Prerequisito de entrada

Antes de leer cualquier otro archivo, verifica que `docs/spec/product/product.md` contiene
la línea `**Status: Validated**` al inicio del documento.

Si no está validado: detente y comunica al ingeniero que el product doc debe estar validado
antes de continuar con la arquitectura. No generes nada.

## 3. Contexto a leer

Lee los siguientes archivos en este orden:

1. `docs/ai/rules/constitution.md` — principios rectores, en especial la sección de AI Behavior Rules
2. `docs/ai/agents/software-architect.md` — tu rol y protocolo de entrega
3. `docs/spec/product/product.md` — fuente primaria de requisitos
4. `docs/spec/product/*.md` — cualquier módulo adicional de producto
5. `docs/spec/decisions/*.md` — cargar todos los ADRs con `status: accepted` como restricciones vinculantes

Si no existen ADRs previos, continúa. Toma nota de que este puede ser el primer ADR del proyecto.

## 4. Tarea

Diseña la arquitectura del sistema basándote exclusivamente en lo que está documentado en el product doc.
Sigue estas reglas sin excepción:

- No inventes tecnologías que no estén justificadas por un requisito de producto o un ADR aceptado
- Si un requisito de producto no tiene suficiente detalle para tomar una decisión técnica, pregunta al ingeniero antes de asumir
- Cada tecnología del stack debe tener su justificación explícita en la sección Technology Stack
- Cada decisión significativa debe generar un ADR separado en `docs/spec/decisions/`

Una decisión es significativa si: afecta el stack tecnológico, define el modelo de datos,
establece la estrategia de seguridad, o introduce una dependencia externa relevante.

## 5. Template obligatorio

Usa exactamente la estructura de `docs/ai/templates/architecture-template.md`.
Lee los comentarios `<!-- Instrucción: ... -->` del template y sígelos al pie de la letra.
No omitas ninguna sección. Si una sección no aplica, escríbela con "N/A" y justificación.

Para cada ADR generado, usa exactamente la estructura de `docs/ai/templates/adr-template.md`.

## 6. Output

**Arquitectura del sistema:**
- **Ruta:** `docs/spec/architecture/architecture.md`
- **Convención:** un solo archivo por proyecto. Si el sistema tiene dominios muy separados, consultar al ingeniero antes de dividir.

**ADRs (uno por decisión significativa):**
- **Ruta:** `docs/spec/decisions/ADR-[NNN]-[titulo-en-kebab-case].md`
- **Convención de IDs:** ceros a la izquierda, tres dígitos: `ADR-001`, `ADR-002`
- **Convención de nombres:** `ADR-001-use-postgresql.md`, `ADR-002-use-react.md`

Confirma cada ruta de guardado antes de escribir. Genera primero la arquitectura, luego los ADRs.
