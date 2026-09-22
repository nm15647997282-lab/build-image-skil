# <target-skill> — Reference Analysis

> Copy this template into the target build and fill the copy as the Phase 1B artifact. Use the current Core Dimensions from `System/analysis_framework.md`, promote only evidence-qualified Adaptive Dimensions, and keep all findings descriptive rather than command-like.

## 1. Analysis Scope

| Field | Value |
|---|---|
| Build ID / Version | `<value>` |
| Target Skill | `<value>` |
| Phase 1A Verdict | `<value>` |
| Core References | `<REF IDs>` |
| Supporting References | `<REF IDs>` |
| Limited / Boundary References | `<REF IDs>` |
| Excluded References | `<REF IDs and reason>` |

## 2. Core Dimension Findings

Instantiate or combine rows as the evidence requires. All current Framework Core Dimensions must be checked, but they need not become identical fixed sections.

| Core Dimension(s) | OBS IDs | Evidence REF IDs | Descriptive Finding | Contradictions / Limits | Confidence |
|---|---|---|---|---|---|
| `<framework dimension or justified grouping>` | `<OBS IDs>` | `<REF IDs>` | `<what is observed>` | `<IDs / uncertainty>` | `<high / medium / low / insufficient>` |

## 3. Adaptive Dimension Decisions

### Candidate and Promotion Record

| Candidate | Parent Core Dimension | Promotion Evidence | Contradictions | Decision | Confidence |
|---|---|---|---|---|---|
| `<evidence-derived name>` | `<dimension>` | `<signals and REF / OBS IDs>` | `<concise>` | `<PROMOTE / RETAIN AS OBSERVED DETAIL / INCIDENTAL DETAIL / INSUFFICIENT EVIDENCE>` | `<value>` |

### Promoted Adaptive Dimensions

Repeat only for `PROMOTE` decisions.

#### <adaptive-dimension-name>

| Field | Finding |
|---|---|
| Parent Core Dimension | `<value>` |
| What was inspected | `<concise>` |
| Why separate analysis is needed | `<concise>` |
| Evidence Scope | `<REF / OBS IDs>` |
| Descriptive Finding | `<finding>` |
| Known Contradictions | `<value / none>` |
| Confidence | `<high / medium / low>` |

## 4. Recurring Patterns

| OBS ID | Pattern | Core / Adaptive Dimension | REF IDs | Frequency | Importance | Confidence | Contradiction | Potential Role |
|---|---|---|---|---|---|---|---|---|
| `OBS-___` | `<descriptive>` | `<value>` | `<IDs>` | `<Dominant / Common / Occasional / Rare / Single-instance>` | `<core / important / supporting / incidental>` | `<value>` | `<IDs / none>` | `<INV / VAR / ANTI candidate / incidental>` |

## 5. Core Visual Identity

`<Evidence-based synthesis of the visual mechanisms, scope, major variation, and differentiating boundaries. Avoid adjective-only summaries.>`

| Field | Value |
|---|---|
| Evidence Scope | `<REF / OBS IDs>` |
| Overall Confidence | `<high / medium / low>` |
| Major Qualifications | `<concise / none>` |

## 6. Invariants

| INV ID | Descriptive Statement | Supporting OBS / REF IDs | Contradictions | Importance | Confidence | Status |
|---|---|---|---|---|---|---|
| `INV-___` | `<statement>` | `<IDs>` | `<IDs / none>` | `<core / important / supporting>` | `<value>` | `<active / provisional / deprecated / rejected>` |

## 7. Allowed Variations

| VAR ID | Variable Dimension | Supported Range / Options | Stable Core | Boundary | OBS / REF IDs | Importance | Confidence | Status |
|---|---|---|---|---|---|---|---|---|
| `VAR-___` | `<dimension>` | `<descriptive range>` | `<related INV IDs / meaning>` | `<drift boundary>` | `<IDs>` | `<value>` | `<value>` | `<active / provisional / deprecated / rejected>` |

## 8. Incidental / Observed Details

| Detail | REF / OBS IDs | Frequency | Why It Is Not Core | Current Handling |
|---|---|---|---|---|
| `<detail>` | `<IDs>` | `<value>` | `<reason>` | `<retain / incidental / insufficient evidence>` |

## 9. Anti-patterns

| ANTI ID | Incompatible Direction | Comparison / Evidence | Conflict with Identity / Scope | Context / Exceptions | Importance | Confidence | Status |
|---|---|---|---|---|---|---|---|
| `ANTI-___` | `<descriptive>` | `<OBS / REF IDs>` | `<concise>` | `<value>` | `<value>` | `<value>` | `<active / provisional / deprecated / rejected>` |

## 10. Subtype Analysis

| Candidate | REF IDs | Shared Invariants | Distinguishing Dimensions | Decision | Confidence |
|---|---|---|---|---|---|
| `<name>` | `<IDs>` | `<INV candidates / summary>` | `<concise>` | `<Allowed Variation / Meaningful Subtype / Separate Skill Candidate / Insufficient Evidence>` | `<value>` |

## 11. Open Questions and Insufficient Evidence

| ID | Question / Gap | Affected Conclusion | Evidence Needed | Blocking Phase 2? |
|---|---|---|---|---|
| `<AN-ISSUE-___>` | `<concise>` | `<IDs / section>` | `<value>` | `<yes / no>` |

## 12. Evidence Confidence Summary

| Result Group | High | Medium | Low | Insufficient | Notes |
|---|---:|---:|---:|---:|---|
| OBS / Patterns | `<n>` | `<n>` | `<n>` | `<n>` | `<concise>` |
| INV | `<n>` | `<n>` | `<n>` | `<n>` | `<concise>` |
| VAR | `<n>` | `<n>` | `<n>` | `<n>` | `<concise>` |
| ANTI | `<n>` | `<n>` | `<n>` | `<n>` | `<concise>` |

## 13. Readiness for Visual System Specification

| Field | Value |
|---|---|
| Verdict | `<READY FOR VISUAL SYSTEM SPECIFICATION / NOT READY>` |
| Blocking Issues | `<IDs or none>` |
| Non-blocking Limitations | `<IDs or none>` |
| Traceability Sync | `<complete / issues found>` |
| Next Required Action | `<Phase 2 action or upstream resolution>` |
