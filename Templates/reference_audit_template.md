# <target-skill> — Reference Set Audit

> Copy this template into the target build and fill the copy as the Phase 1A artifact. Record evidence reliability, weighting, contamination, and readiness only; do not create Analysis conclusions, Visual Rules, Skill Rules, or Tests here.

## 1. Audit Scope

| Field | Value |
|---|---|
| Build ID / Version | `<value>` |
| Target Skill | `<value>` |
| Purpose | `<value>` |
| Scope Boundary | `<value>` |
| References Path | `<value>` |
| Audit Date | `<value>` |

## 2. Reference Inventory

| REF ID | Source File | Accessible / Reviewable | Initial Notes |
|---|---|---|---|
| `REF-___` | `<path>` | `<yes / no>` | `<concise visible fact or issue>` |

## 3. Reference Classification

| REF ID | Role | Classification Reason | Use in Phase 1B | Status |
|---|---|---|---|---|
| `REF-___` | `<Core / Supporting / Ambiguous / Outlier>` | `<evidence-based reason>` | `<include / limited / boundary only / exclude>` | `<active / provisional / deprecated / rejected>` |

### Classification Summary

| Role | Count | REF IDs |
|---|---:|---|
| Core | `<n>` | `<IDs>` |
| Supporting | `<n>` | `<IDs>` |
| Ambiguous | `<n>` | `<IDs>` |
| Outlier | `<n>` | `<IDs>` |

## 4. Recurring Feature Frequency

Record only audit-level repetition signals that help weight evidence; detailed visual interpretation belongs to Phase 1B.

| OBS ID | Observed Feature / Relation | Supporting REF IDs | Frequency | Contradictions | Audit Note |
|---|---|---|---|---|---|
| `OBS-___` | `<visible feature>` | `<IDs>` | `<Dominant / Common / Occasional / Rare / Single-instance>` | `<IDs or none>` | `<concise>` |

## 5. Contamination Risk

| Risk ID | Affected REF IDs | Observable Concern | Possible Effect on Analysis | Handling |
|---|---|---|---|---|
| `<RA-ISSUE-___>` | `<IDs>` | `<concise>` | `<weighting / subtype / outlier risk>` | `<limit / exclude / review>` |

## 6. Subtype Check

| Candidate Group | REF IDs | Shared Evidence | Key Difference | Current Decision |
|---|---|---|---|---|
| `<name>` | `<IDs>` | `<concise>` | `<concise>` | `<same family / possible subtype / separate candidate / insufficient evidence>` |

## 7. Reference Set Issues

| Issue ID | Severity / Blocking | Evidence | Required Resolution | Status |
|---|---|---|---|---|
| `<RA-ISSUE-___>` | `<blocking / non-blocking>` | `<REF IDs>` | `<action>` | `<open / resolved / accepted>` |

## 8. Recommended Analysis Set

| Use | REF IDs | Conditions / Notes |
|---|---|---|
| Primary analysis | `<IDs>` | `<concise>` |
| Supporting comparison | `<IDs>` | `<concise>` |
| Boundary / contamination comparison | `<IDs>` | `<concise>` |
| Excluded from Phase 1B | `<IDs>` | `<reason>` |

## 9. Readiness Verdict

| Field | Value |
|---|---|
| Verdict | `<READY / READY WITH ISSUES / NOT READY>` |
| Blocking Reasons | `<issue IDs or none>` |
| Non-blocking Issues | `<issue IDs or none>` |
| Exit Gate Status | `<PASS / NOT PASSED>` |
| Next Required Action | `<Phase 1B action or Phase 1A resolution>` |
| Notes | `<concise>` |
