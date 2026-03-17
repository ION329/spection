# Spection Constitution

These are the non-negotiable principles that govern all engineering decisions in this project.
Every engineer and every AI session must respect these rules without exception.
When in doubt, refer to this document before proceeding.

---

## I. Specification Integrity

**The spec is the source of truth.**
If the code contradicts the spec, the code is wrong — not the spec.
If the spec needs to change, update the spec first, then update the code.

**No feature is implemented without a validated spec.**
A feature request, a verbal agreement, or a chat message is not a spec.
The feature does not exist until `docs/spec/features/[feature]-spec.md` exists and is validated.

**No phase may be skipped.**
The sequence is: Discovery → Architecture → Feature Spec → Engineering Spec → Tasks → Implementation.
Skipping a phase to move faster always produces rework. It is not permitted.

---

## II. AI Behavior Rules

**The AI must never hallucinate technologies.**
The AI may only recommend or use technologies explicitly present in:
- `docs/spec/architecture/architecture.md`
- An ADR with `status: accepted` in `docs/spec/decisions/`

If the AI is uncertain about the approved stack, it must ask before generating.

**The AI must follow templates exactly.**
All generated documents must use the templates in `docs/ai/templates/`.
No section may be omitted without explicit engineer approval.

**The AI must save output to the specified path.**
Every prompt defines an output path. The AI must use that path.
It must not invent alternative paths or file names.

**The AI must ask before specifying.**
In the feature specification phase, the AI is required to ask clarifying questions
before generating a spec. This step is mandatory and cannot be bypassed.

**The AI must not modify validated documents without instruction.**
Once the engineer has validated a document, the AI must not alter it
unless the engineer explicitly requests a revision.

---

## III. Code Quality Standards

**Every function must do one thing.**
Functions with multiple responsibilities must be split before merging.

**No magic values in code.**
All constants must be named and documented. No hardcoded strings, numbers, or URLs in business logic.

**No implementation without a corresponding test plan.**
Every engineering spec must include a section describing how the feature will be tested.
The tasks file must include at least one test task.

**Security is not optional.**
Authentication, authorization, input validation, and data sanitization are not features.
They are requirements on every endpoint and every user-facing input.
They must appear in the engineering spec, not be added as afterthoughts.

---

## IV. Validation Gates

**The engineer is the only one who can approve a phase transition.**
The AI generates. The engineer validates. Validation is not automatic.

**A document is not validated until the engineer explicitly marks it so.**
The engineer signals validation by either:
- Appending `**Status: Validated**` at the top of the document, or
- Moving the workflow forward via explicit instruction

**Review notes must be resolved before advancing.**
If a `## Review Notes` section exists in a spec with unresolved `critical` items,
that spec cannot advance to the next phase.

---

## V. Context Hygiene

**Every implementation session starts with a clean context.**
Before coding, close all active AI chats. Open a new session.
Load only:
1. `docs/spec/engineering/[feature]-engineering.md`
2. `docs/spec/tasks/[feature]-tasks.md`
3. ADRs with `status: accepted` relevant to the feature

**Do not load product docs, architecture overviews, or unrelated specs into an implementation session.**
High-level context contaminates implementation-level reasoning and degrades output quality.

---

## VI. Architecture Decision Records

**Every significant technical decision must be recorded as an ADR.**
A decision is significant if it:
- affects the technology stack
- changes a data model
- introduces a new external dependency
- contradicts or supersedes a previous decision

**ADRs are immutable once accepted.**
An accepted ADR is never edited. If a decision changes, a new ADR is created
with `supersedes: ADR-[previous-id]` and the old one is updated to `status: superseded`.

**The AI must load accepted ADRs at the start of every architecture or engineering session.**
Rules defined in ADRs are binding constraints, not suggestions.
