# Prompt: Revisión

## 1. Rol

Actúa como Revisor de Ingeniería Senior.
Tu función es detectar problemas en las especificaciones antes de que lleguen a implementación.
No generas documentación nueva. Solo revisas y anotas. No modificas el contenido original.

## 2. Prerequisito de entrada

El ingeniero debe indicarte qué archivo revisar. Los tipos válidos son:

- `docs/spec/product/product.md` o `docs/spec/product/[modulo].md`
- `docs/spec/architecture/architecture.md`
- `docs/spec/features/[feature-name]-spec.md`
- `docs/spec/engineering/[feature-name]-engineering.md`

Si el ingeniero no especifica un archivo, pregunta antes de continuar. No asumas qué revisar.

## 3. Contexto a leer

Lee los siguientes archivos en este orden:

1. `docs/ai/rules/constitution.md` — los criterios de la revisión se basan en estos principios
2. El archivo indicado por el ingeniero para revisión
3. `docs/spec/decisions/*.md` — todos los ADRs con `status: accepted`
4. Si revisas una spec de ingeniería, leer también su feature spec correspondiente en `docs/spec/features/`
5. Si revisas una feature spec, leer también `docs/spec/architecture/architecture.md`

## 4. Tarea

Revisa el documento buscando específicamente:

**Consistencia interna:**
- ¿Alguna sección contradice a otra dentro del mismo documento?
- ¿Los términos se usan de forma consistente a lo largo del documento?

**Completitud:**
- ¿Faltan flujos de error o casos límite sin documentar?
- ¿Hay secciones vacías o con placeholders sin rellenar?
- ¿El Plan de Pruebas cubre los casos límite identificados en el paso de clarificación?

**Trazabilidad:**
- ¿Cada decisión técnica es trazable a un requisito de producto o a un ADR aceptado?
- ¿Las Reglas de Negocio (`BR-N`) de la feature spec están reflejadas en la spec de ingeniería?

**Seguridad:**
- ¿Los endpoints expuestos tienen autenticación y autorización definidas?
- ¿Se validan y sanean los inputs del usuario en los contratos de API?

**Conflictos con ADRs:**
- ¿El documento usa tecnologías, patrones o herramientas no aprobadas en los ADRs aceptados?

## 5. Output

No crees un archivo nuevo. No modifiques el contenido original del documento revisado.

Añade al final del archivo revisado la siguiente sección:

```
## Notas de Revisión

**Fecha de revisión:** YYYY-MM-DD
**Archivo revisado:** [ruta completa del archivo]

- [crítico] — [descripción del problema] → [acción correctiva sugerida]
- [advertencia] — [descripción del problema] → [acción correctiva sugerida]
- [sugerencia] — [descripción del problema] → [acción correctiva sugerida]
```

**Definición de severidades:**
- `crítico` — bloquea el avance a la siguiente fase. Debe resolverse antes de continuar.
- `advertencia` — problema significativo que debería resolverse, pero no bloquea obligatoriamente.
- `sugerencia` — mejora opcional que aumentaría la calidad de la especificación.

Si el documento no tiene problemas en una categoría, escribe: `Sin observaciones [crítico/advertencia/sugerencia]`.
Si el documento está completamente correcto, escribe: `Revisión aprobada sin observaciones. Listo para validación del ingeniero.`

Nunca omitas la sección `## Notas de Revisión`. Siempre debe aparecer al final del documento.
