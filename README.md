# Spection

Spec-Driven Development. The specification is the source of truth.
Code is a direct consequence of documentation.

## Structure

```
docs/
├── ai/                              ← methodology engine (framework rules, do not modify per-project)
│   ├── ai-engineering-methodology.md   ← canonical methodology document
│   ├── agents/                      ← AI role definitions
│   ├── prompts/                     ← executable prompts with input/output contracts
│   ├── templates/                   ← document templates
│   ├── workflows/                   ← step-by-step process guides
│   └── rules/                       ← governance and constitutional rules
│       └── constitution.md          ← non-negotiable engineering principles
│
├── spec/                            ← project specs (AI-generated, engineer-validated)
│   ├── product/                     ← product definition and problem space
│   ├── architecture/                ← system architecture and tech stack
│   ├── features/                    ← individual feature specifications
│   ├── engineering/                 ← implementation-ready engineering specs
│   ├── tasks/                       ← task breakdowns per feature
│   └── decisions/                   ← architecture decision records (ADRs)
│
├── public/                          ← simplified documentation for stakeholders
└── lab/                             ← experiments, research, and implementation history
    └── history/                     ← archived specs of implemented features
```

## How it works

Spection runs a pipeline of specialized AI agents. Each phase produces a validated document
before the next one begins. No phase can be skipped.

```
Discovery → Architecture → Feature Spec → Engineering Spec + Tasks → Implementation → Archive
```

| Agent | Prompt | Output |
|---|---|---|
| Product Strategist | `prompts/discovery.md` | `docs/spec/product/product.md` |
| Software Architect | `prompts/architecture.md` | `docs/spec/architecture/architecture.md` + ADRs |
| Systems Engineer | `prompts/feature-spec.md` | `docs/spec/features/[feature]-spec.md` |
| Lead Engineer | `prompts/engineering.md` | `docs/spec/engineering/[feature]-engineering.md` + `tasks.md` |
| Technical Writer | `prompts/review.md` | `docs/public/` |

Every phase transition requires explicit engineer approval (`**Status: Validated**`).

## Start here

**New project:**
1. Read the methodology: `docs/ai/ai-engineering-methodology.md`
2. Read the project rules: `docs/ai/rules/constitution.md`
3. Run the full workflow: `docs/ai/workflows/init-project.md`

**Adding a feature to an existing project:**
- `docs/ai/workflows/create-feature.md`

**Before writing any code:**
- `docs/ai/workflows/implementation-hygiene.md`

**After a feature is implemented and merged:**
- `docs/ai/workflows/archive-feature.md`
