# <target-skill> — Skill Consistency Audit

> Copy this template into the target build and fill the copy as the Phase 3B artifact. Audit the compiled `SKILL.md` against the evidence hierarchy; do not redesign the Visual System or run generation tests here.

## 1. Audit Scope

| Field | Value |
|---|---|
| Build ID / Version | `<value>` |
| Candidate Path / Version | `<value>` |
| Audit Date | `<value>` |
| Auditor / Pass | `<value>` |

## 2. Evidence Sources

| Layer | Artifact / Version | Status |
|---|---|---|
| References | `<path / version>` | `<valid / issue>` |
| Reference Audit | `<path / version>` | `<valid / issue>` |
| Reference Analysis | `<path / version>` | `<valid / issue>` |
| Visual Rules | `<path / version>` | `<valid / issue>` |
| Prompt Rules | `<path / version>` | `<valid / issue>` |
| Quality Rules | `<path / version>` | `<valid / issue>` |
| Traceability | `<path / version>` | `<valid / issue>` |

## 3. Coverage Summary

| Coverage Area | Upstream IDs | SK IDs / Candidate Location | Result | Notes |
|---|---|---|---|---|
| Core Invariants | `<IDs>` | `<IDs / location>` | `<complete / gap>` | `<concise>` |
| Allowed Variations | `<IDs>` | `<IDs / location>` | `<preserved / collapsed / gap>` | `<concise>` |
| Anti-pattern Guardrails | `<IDs>` | `<IDs / location>` | `<complete / gap / excessive>` | `<concise>` |
| Prompt Rule Capability | `<IDs>` | `<IDs / location>` | `<complete / gap>` | `<concise>` |
| Quality Rule Capability | `<IDs>` | `<IDs / location>` | `<complete / gap>` | `<concise>` |
| Purpose / Scope | `<brief location>` | `<candidate location>` | `<preserved / leakage>` | `<concise>` |

## 4. Issue Register

Allowed Category values:

`Missing / Distorted / Unsupported / Redundant / Untraced Rule / Dropped Invariant / Orphan Quality Rule / Untested Invariant / Pending Test Coverage / Strength Distortion / Scope Leakage / Variation Preservation Failure / Anti-pattern Coverage Gap / Prompt Rule Coverage Gap / Quality Rule Coverage Gap / Traceability Integrity / Overengineering / Under-specification`

| Issue ID | Category | Severity | Affected Rule / Section | Upstream IDs | Evidence | Problem | Required Minimal Fix | Owner | Status | Recheck Result |
|---|---|---|---|---|---|---|---|---|---|---|
| `<AUD-___>` | `<category>` | `<Critical / Major / Minor>` | `<SK ID / location>` | `<IDs>` | `<artifact / IDs>` | `<concise>` | `<action>` | `<phase>` | `<open / corrected / accepted minor>` | `<pending / pass / fail>` |

## 5. Traceability Integrity

| Check | Result | Affected IDs / Notes |
|---|---|---|
| Untraced Rule | `<pass / issues>` | `<value>` |
| Dropped Invariant | `<pass / issues>` | `<value>` |
| Orphan Quality Rule | `<pass / issues>` | `<value>` |
| Variation Coverage / Collapse | `<pass / issues>` | `<value>` |
| Anti-pattern Coverage | `<pass / issues>` | `<value>` |
| Strength Distortion | `<pass / issues>` | `<value>` |
| Broken / Asymmetric Links | `<pass / issues>` | `<value>` |
| Invalid Active Dependency | `<pass / issues>` | `<value>` |
| SK locations and Revision Records | `<pass / issues>` | `<value>` |

## 6. Pending Test Coverage

Do not create TC IDs in Phase 3B.

| Target IDs | Behavior / Risk to Validate | Future Case Family | Why Static Audit Is Insufficient | Strength / Context / Boundary to Protect |
|---|---|---|---|---|
| `<INV / VAR / ANTI / SK IDs>` | `<value>` | `<Core / Variation / Stress / Boundary>` | `<value>` | `<value>` |

## 7. Corrections

| Correction ID | Issue IDs | Candidate / SK Change | Traceability Update | Upstream Change Required | Result |
|---|---|---|---|---|---|
| `<COR-___>` | `<IDs>` | `<minimal change>` | `<links / location / revision>` | `<no or rollback target>` | `<pending / complete>` |

## 8. Secondary Validation

| Check | Result | Notes |
|---|---|---|
| Original issues closed | `<pass / fail>` | `<IDs>` |
| Critical = 0 | `<yes / no>` | `<value>` |
| Major = 0 | `<yes / no>` | `<value>` |
| No new Unsupported / Distorted rule | `<pass / fail>` | `<value>` |
| Variation remains preserved | `<pass / fail>` | `<value>` |
| Scope and Strength remain valid | `<pass / fail>` | `<value>` |
| Traceability remains consistent | `<pass / fail>` | `<value>` |
| No new Overengineering / Under-specification | `<pass / fail>` | `<value>` |

## 9. Verdict and Exit Gate

| Field | Value |
|---|---|
| Critical Count | `<n>` |
| Major Count | `<n>` |
| Minor Count | `<n>` |
| Verdict | `<PASS / PASS WITH ISSUES / FAIL>` |
| Exit Gate | `<PASS / NOT PASSED>` |
| Phase 4 Allowed | `<yes / no>` |
| Upstream Rollback | `<none or owner phase / reason>` |
| Next Required Action | `<value>` |

`PASS WITH ISSUES` may contain Minor issues only; any unresolved Critical or Major requires `FAIL`.
