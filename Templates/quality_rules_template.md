# <target-skill> — Quality Rules

> Copy this template into the target build and fill the copy as a Phase 2 artifact. QR evaluates active VR; it cannot add an independent visual standard.

## 1. Quality Objective

`<What successful membership in the current Visual Family means and how scope is protected.>`

## 2. Evaluation Architecture

### Layer 1 — Hard Fail Conditions

| QR ID | What Is Checked | Failure Condition | Source VR IDs | Context | Strength / Severity Relation | Status |
|---|---|---|---|---|---|---|
| `QR-___` | `<observable requirement>` | `<hard failure>` | `<VR IDs>` | `<value>` | `<source strength and consequence>` | `<active / provisional / deprecated / rejected>` |

### Layer 2 — Visual-family Quality

| QR ID | Category | What Is Checked | Acceptable | Deviation | Failure | Source VR IDs | Context | Strength / Severity Relation | Status |
|---|---|---|---|---|---|---|---|---|---|
| `QR-___` | `<core / adaptive / variation / anti-pattern / scope>` | `<observable check>` | `<condition>` | `<condition>` | `<condition>` | `<VR IDs>` | `<value>` | `<source strength and consequence>` | `<active / provisional / deprecated / rejected>` |

The Layer 1 and Layer 2 tables are the canonical formal QR definitions. Every QR referenced below must appear in one of them. A QR's formal source is always one or more VR IDs; related INV / VAR / ANTI IDs are coverage context, not a substitute source link.

## 3. Invariant Compliance

| QR ID | Source VR IDs | Related INV IDs | Observable Check | Acceptable | Failure |
|---|---|---|---|---|---|
| `QR-___` | `<VR IDs>` | `<INV IDs>` | `<check>` | `<condition>` | `<condition>` |

## 4. Allowed Variation Validity

| QR ID | Source VR IDs | Related VAR IDs | Valid Range / Options | Borderline | Outside Visual Family | Stable Core Checked |
|---|---|---|---|---|---|---|
| `QR-___` | `<VR IDs>` | `<VAR IDs>` | `<condition>` | `<condition>` | `<condition>` | `<INV / VR IDs>` |

## 5. Anti-pattern Contamination

| QR ID | Source VR IDs | Related ANTI IDs | Contamination Signal | Acceptable Context / Exception | Revision Threshold | Failure Threshold |
|---|---|---|---|---|---|---|
| `QR-___` | `<VR IDs>` | `<ANTI IDs>` | `<observable signal>` | `<value / none>` | `<condition>` | `<condition>` |

## 6. Adaptive Dimension Checks

Include only promoted Adaptive Dimensions with active VR.

| QR ID | Adaptive Dimension | Source VR IDs | What Is Checked | Acceptable | Deviation | Failure |
|---|---|---|---|---|---|---|
| `QR-___` | `<dimension>` | `<IDs>` | `<check>` | `<condition>` | `<condition>` | `<condition>` |

## 7. Verdict Logic

| Verdict | Required Condition |
|---|---|
| PASS | `<no Hard Fail; core rules hold; Variation is valid; no identity-changing deviation>` |
| REVISE | `<no Hard Fail; important but correctable deviation or boundary risk>` |
| FAIL | `<Hard Fail or combined deviations invalidate Visual Family / Scope>` |

Auxiliary scoring may support comparison but cannot offset a Hard Fail.

## 8. Revision Direction

| QR IDs | Observed Failure | Likely Responsible Rule Path | Minimal Revision Direction |
|---|---|---|---|
| `<IDs>` | `<observable failure>` | `<QR → VR → source roles>` | `<concise; no new standard>` |

## 9. Traceability and Readiness

| Check | Result | IDs / Notes |
|---|---|---|
| Every active QR has active VR source | `<pass / issues>` | `<IDs>` |
| Every active VR has a usable QR | `<pass / issues>` | `<IDs>` |
| No QR adds an upstream-undefined requirement | `<pass / issues>` | `<IDs>` |
| VAR can be distinguished from Style Drift | `<pass / issues>` | `<IDs>` |
| Hard Fail conditions have formal VR support | `<pass / issues>` | `<IDs>` |
| Traceability links and locations synced | `<pass / issues>` | `<concise>` |

**Artifact status:** `<IN PROGRESS / READY / NOT READY>`  
**Next required action:** `<value>`
