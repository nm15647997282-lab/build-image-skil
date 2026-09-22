# <target-skill> — Prompt Rules

> Copy this template into the target build and fill the copy as a Phase 2 artifact. PR implements active VR; it does not introduce a new visual source of truth or a fixed production prompt.

## 1. Prompt Objective

`<How prompts should realize the current Visual System and preserve scope.>`

## 2. Prompt Construction Logic

Record the target-specific construction sequence. Keep it adaptable to input and Context.

1. `<identify the primary visual object and scope>`
2. `<select applicable rules by Context, Priority, and Strength>`
3. `<describe concrete visible state and relationships>`
4. `<express the chosen legal Variation and stable core>`
5. `<add only relevant Guardrails>`
6. `<remove unsupported, conflicting, or duplicate language>`
7. `<run the target Skill's generation check>`

## 3. Description Priority

| Order / Priority | Information to Express | Source VR IDs | Context / Notes |
|---|---|---|---|
| `<value>` | `<concrete visual information>` | `<VR IDs>` | `<value>` |

Concrete physical or visual description should carry execution meaning; abstract style adjectives cannot replace it.

## 4. Vocabulary Guidance

Add only vocabulary supported by current VR or verified generation behavior. Do not prefill a domain word list.

### Preferred Vocabulary

| Term / Pattern | Purpose | Source VR IDs | Context |
|---|---|---|---|
| `<value>` | `<value>` | `<IDs>` | `<value>` |

### Conditional Vocabulary

| Term / Pattern | Allowed Context | Risk Outside Context | Source VR IDs |
|---|---|---|---|
| `<value>` | `<value>` | `<value>` | `<IDs>` |

### Risky Vocabulary

| Term / Pattern | Known Ambiguity / Risk | Safer Expression Strategy | Source VR / ANTI IDs |
|---|---|---|---|
| `<value>` | `<value>` | `<value>` | `<IDs>` |

### Avoid Vocabulary

| Term / Pattern | Evidence-supported Failure Risk | Replacement / Handling | Source VR / ANTI IDs |
|---|---|---|---|
| `<value>` | `<value>` | `<value>` | `<IDs>` |

## 5. Variation Expression

| PR ID | Source VR IDs | Related VAR IDs | Variation Choice | Prompt Expression Strategy | Stable Core | Boundary Guard |
|---|---|---|---|---|---|---|
| `PR-___` | `<VR IDs>` | `<VAR IDs>` | `<supported option / range>` | `<strategy>` | `<INV / VR IDs>` | `<concise>` |

## 6. Anti-pattern Guardrail Language

| PR ID | Source VR IDs | Related ANTI IDs | Risk Context | Guardrail Strategy | Legitimate Nearby VAR | Strength |
|---|---|---|---|---|---|---|
| `PR-___` | `<VR IDs>` | `<ANTI IDs>` | `<value>` | `<concrete wording strategy>` | `<VAR IDs / none>` | `<MUST / SHOULD / MAY / AVOID / DO NOT>` |

## 7. Formal Prompt Rules

| PR ID | Expression Objective / Rule | Source VR IDs | Strength | Context | Wording Strategy | Known Ambiguity / Failure Risk | Status |
|---|---|---|---|---|---|---|---|
| `PR-___` | `<rule>` | `<VR IDs>` | `<MUST / SHOULD / MAY / AVOID / DO NOT>` | `<value>` | `<concrete strategy>` | `<value / none>` | `<active / provisional / deprecated / rejected>` |

## 8. Traceability and Readiness

| Check | Result | IDs / Notes |
|---|---|---|
| Every active PR has active VR source | `<pass / issues>` | `<IDs>` |
| Every active VR has usable prompt expression | `<pass / issues>` | `<IDs>` |
| Strength and Context match source VR | `<pass / issues>` | `<IDs>` |
| Variation remains selectable | `<pass / issues>` | `<VAR / PR IDs>` |
| Vocabulary adds no unsupported visual content | `<pass / issues>` | `<concise>` |
| Traceability links and locations synced | `<pass / issues>` | `<concise>` |

**Artifact status:** `<IN PROGRESS / READY / NOT READY>`  
**Next required action:** `<value>`
