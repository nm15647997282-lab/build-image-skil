# <target-skill> — Visual Rules

> Copy this template into the target build and fill the copy as a Phase 2 artifact. Compile only active INV / VAR / ANTI with legal evidence links. Detailed evidence remains in Reference Analysis and Traceability.

## 1. Visual Objective

`<Concise executable objective derived from Core Visual Identity and target scope.>`

## 2. Rule Priority

| Priority | Meaning in This Build | Rule IDs |
|---|---|---|
| 1 — Identity / Scope Critical | `<concise>` | `<VR IDs>` |
| 2 — Stability Critical | `<concise>` | `<VR IDs>` |
| 3 — Variation / Boundary Control | `<concise>` | `<VR IDs>` |
| 4 — Supporting Detail | `<concise>` | `<VR IDs>` |

Priority controls attention and conflict handling; it does not change Rule Strength.

## 3. Core Invariant Rules

| VR ID | Rule | Strength | Priority | Context / Condition | Source INV / VAR / ANTI IDs | Variation / Boundary Note | Status |
|---|---|---|---|---|---|---|---|
| `VR-___` | `<executable visual behavior>` | `<MUST / SHOULD / MAY / AVOID / DO NOT>` | `<1–4>` | `<value>` | `<IDs>` | `<concise / none>` | `<active / provisional / deprecated / rejected>` |

## 4. Core Visual Rules

Instantiate rules by the visual mechanisms present in this build; do not create empty domain sections.

| VR ID | Rule | Strength | Priority | Context / Condition | Source Role IDs | Notes |
|---|---|---|---|---|---|---|
| `VR-___` | `<rule>` | `<MUST / SHOULD / MAY / AVOID / DO NOT>` | `<1–4>` | `<value>` | `<INV / VAR / ANTI IDs>` | `<only if needed>` |

## 5. Adaptive Visual Rules

Include only rules from promoted Adaptive Dimensions.

| VR ID | Adaptive Dimension | Rule | Strength | Priority | Context | Source Role IDs | Notes |
|---|---|---|---|---|---|---|---|
| `VR-___` | `<promoted dimension>` | `<rule>` | `<MUST / SHOULD / MAY / AVOID / DO NOT>` | `<1–4>` | `<value>` | `<IDs>` | `<concise>` |

## 6. Allowed Variation

| VR ID | Source VAR ID | What May Vary | Supported Range / Options | What Remains Stable | Boundary / Drift Condition | Strength | Priority |
|---|---|---|---|---|---|---|---|
| `VR-___` | `VAR-___` | `<dimension>` | `<range>` | `<INV IDs / behavior>` | `<boundary>` | `<MAY or evidence-supported contextual strength>` | `<1–4>` |

## 7. Anti-pattern and Boundary Rules

| VR ID | Source ANTI / VAR ID | Direction to Avoid or Exclude | Conflict / Risk | Context / Legitimate Exception | Strength | Priority |
|---|---|---|---|---|---|---|
| `VR-___` | `<ANTI / VAR IDs>` | `<observable direction>` | `<identity / scope / boundary consequence>` | `<value / none>` | `<AVOID / DO NOT>` | `<1–4>` |

## 8. Conflict and Exception Notes

| Related Rule IDs | Context | Resolution | Variation Protected |
|---|---|---|---|
| `<VR IDs>` | `<value>` | `<contextualize / narrow / merge / split>` | `<VAR IDs / none>` |

## 9. Traceability and Readiness

| Check | Result | IDs / Notes |
|---|---|---|
| Every active VR has active source roles | `<pass / issues>` | `<IDs>` |
| All active core INV have VR coverage | `<pass / issues>` | `<IDs>` |
| All active core / important VAR are preserved | `<pass / issues>` | `<IDs>` |
| All active core / important ANTI have guardrails | `<pass / issues>` | `<IDs>` |
| Strength and Priority remain distinct | `<pass / issues>` | `<concise>` |
| Traceability locations and downstream links synced | `<pass / issues>` | `<concise>` |

**Artifact status:** `<IN PROGRESS / READY / NOT READY>`  
**Next required action:** `<value>`
