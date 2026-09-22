# <target-skill> — Test Suite, Refinement, and Freeze Record

> Copy this template into the target build and fill the copy as the Phase 4 artifact structure. Instantiate from active Traceability after Phase 3B passes. If split into multiple files, preserve every responsibility recorded here.

## 1. Test Suite Overview

| Field | Value |
|---|---|
| Build ID / Version | `<value>` |
| Target Skill | `<value>` |
| Candidate Version | `<value>` |
| Static Audit Verdict / Version | `<value>` |
| Test Scope | `<concise>` |
| Suite Status | `<NOT STARTED / IN PROGRESS / PASS / PASS WITH ISSUES / FAIL / BLOCKED>` |
| Last Updated | `<timestamp>` |

### Test Environment

| Field | Value |
|---|---|
| Generation Model / Service | `<value or unavailable>` |
| Model / Service Version | `<value or unavailable>` |
| Relevant Settings | `<value or unavailable>` |
| Execution Dates | `<value>` |
| Uncontrolled Factors | `<value / none known>` |

## 2. Case Plan by Type

### Core Cases — `INV → Core`

| TC ID | Verifies | Purpose | Attempt Plan | Status |
|---|---|---|---|---|
| `TC-___` | `<INV / SK IDs>` | `<value>` | `<predeclared bounded plan>` | `<status>` |

### Variation Cases — `VAR → Variation`

| TC ID | Verifies | Purpose | Attempt Plan | Status |
|---|---|---|---|---|
| `TC-___` | `<VAR / SK IDs>` | `<value>` | `<predeclared bounded plan>` | `<status>` |

### Stress Cases — `ANTI → Stress`

| TC ID | Verifies | Purpose | Attempt Plan | Status |
|---|---|---|---|---|
| `TC-___` | `<ANTI / SK IDs>` | `<value>` | `<predeclared bounded plan>` | `<status>` |

### Boundary Cases — `VAR Boundary → Boundary`

| TC ID | Verifies | Purpose | Attempt Plan | Status |
|---|---|---|---|---|
| `TC-___` | `<VAR / SK IDs>` | `<value>` | `<predeclared bounded plan>` | `<status>` |

## 3. Test Case Record

Repeat for each TC. Case Type must be `Core / Variation / Stress / Boundary`.

### TC-___ — <title>

| Field | Value |
|---|---|
| Case Type | `<Core / Variation / Stress / Boundary>` |
| Verifies (`traceability.yaml`) | `<active INV / VAR / ANTI / SK IDs>` |
| Supporting Rule Path | `<SK → VR / PR / QR → source roles>` |
| Purpose | `<why this case exists>` |
| Input Scenario | `<legal test input>` |
| Primary Challenge / Risk | `<value>` |
| Prompt Construction Source | `<Candidate section / SK / PR IDs>` |
| Planned Attempts | `<bounded count and reason>` |
| Traceability Location | `<file / section / item>` |

#### Expected Behavior — lock before generation

| Must Hold | Allowed Variation | Borderline | Hard Fail / Outside | Possible Non-systematic Variance |
|---|---|---|---|---|
| `<INV / behavior>` | `<VAR / range>` | `<condition>` | `<QR-supported condition>` | `<condition>` |

#### Evaluation Criteria

| Layer | QR / VR IDs | Observable Check | PASS | Deviation | FAIL |
|---|---|---|---|---|---|
| `<Hard Fail / Visual-family Quality>` | `<IDs>` | `<check>` | `<condition>` | `<condition>` | `<condition>` |

#### Generation and Results

| Attempt | Raw Input | Actual Prompt | Output Reference | Hard Fail | Evaluation | Result | Main Issue | Attribution / Confidence |
|---|---|---|---|---|---|---|---|---|
| `<n>` | `<value>` | `<Candidate-generated prompt>` | `<path / ID>` | `<yes / no; QR ID>` | `<summary>` | `<PASS / PASS WITH VARIANCE / FAIL / BLOCKED>` | `<value / none>` | `<type; confidence>` |

#### Case Conclusion

| Field | Value |
|---|---|
| Aggregate Result | `<PASS / PASS WITH VARIANCE / FAIL / BLOCKED>` |
| Systematic / Isolated | `<systematic / isolated / unresolved / not applicable>` |
| Evidence | `<attempt and rule IDs>` |
| Required Action | `<none / diagnosis / unblock>` |
| Notes | `<concise>` |

## 4. Failure Attribution and Root Cause

Attribution values: `Prompt Construction Failure / SKILL.md Failure / System Rule Failure / Model Variance / Subject-specific Difficulty / Mixed / Unresolved`.

| Failure ID | TC / Attempts | Observed Failure | Attribution | Relevant SK / PR / QR / VR | Relevant INV / VAR / ANTI | Systematic Evidence | Root Cause | Confidence | Next Action |
|---|---|---|---|---|---|---|---|---|---|
| `<FAIL-___>` | `<IDs>` | `<observable>` | `<allowed value>` | `<IDs>` | `<IDs>` | `<value>` | `<closest responsible cause>` | `<high / medium / low>` | `<action>` |

## 5. Refinement Log

### REV-___

| Field | Value |
|---|---|
| Triggering Failure / TC | `<IDs>` |
| Evidence | `<attempt / output / rule IDs>` |
| Failure Attribution | `<allowed value>` |
| Root Cause | `<value>` |
| Owner Phase | `<phase>` |
| Files Changed | `<paths>` |
| Rules / Entity IDs Changed | `<IDs>` |
| Before | `<concise>` |
| After | `<concise>` |
| Why Minimal | `<reason>` |
| Expected Effect | `<value>` |
| Regression Risk | `<value>` |
| Invalidated Gates | `<value / none>` |
| Revalidated Gates | `<value / pending>` |
| Retest Cases | `<TC IDs>` |
| Regression Cases | `<TC IDs>` |
| Outcome / Rollback Path | `<value>` |

## 6. Retest

| Revision ID | Affected TC | Related Risk Case | Related Core Case | Related Variation / Boundary Case | Conditions Comparable | Result | Issue Closed |
|---|---|---|---|---|---|---|---|
| `<REV-___>` | `<TC ID>` | `<TC ID>` | `<TC ID>` | `<TC ID / not applicable>` | `<yes / no>` | `<status>` | `<yes / no>` |

## 7. Regression

| Revision ID | Change Scope | Affected Case | Related Core Case | Related Variation Case | Related Stress / Boundary Case | Regression Result | New Issues |
|---|---|---|---|---|---|---|---|
| `<REV-___>` | `<local / broad; traceability impact>` | `<TC IDs>` | `<TC IDs>` | `<TC IDs>` | `<TC IDs>` | `<PASS / FAIL / PENDING>` | `<IDs / none>` |

### Variation / Anti-pattern Protection

| Revision ID | Guardrail / Strength Change | Nearby Legitimate VAR | Template Lock Check | Over-prohibition Check | Result |
|---|---|---|---|---|---|
| `<REV-___>` | `<IDs>` | `<VAR / TC IDs>` | `<pass / fail>` | `<pass / fail>` | `<value>` |

## 8. Coverage Matrix

| Entity ID | Type | Importance | Required Case Type | TC IDs | Result | Gap / Limitation |
|---|---|---|---|---|---|---|
| `<ID>` | `<INV / VAR / ANTI / SK>` | `<core / important / supporting>` | `<Core / Variation / Stress / Boundary>` | `<IDs>` | `<covered / gap / currently untestable>` | `<value / none>` |

### Capability Coverage

| Capability | TC IDs | Status | Notes |
|---|---|---|---|
| Prompt Construction | `<IDs>` | `<covered / gap>` | `<concise>` |
| Quality Evaluation / Calibration | `<IDs>` | `<covered / gap>` | `<concise>` |
| Scope Boundary | `<IDs>` | `<covered / gap>` | `<concise>` |
| Known Risks | `<IDs>` | `<covered / gap>` | `<concise>` |

## 9. Known Limitations

| Limitation ID | Evidence / TC IDs | Impact and Scope | Why Non-blocking or Blocking | Accepted | Future Unfreeze Trigger |
|---|---|---|---|---|---|
| `<LIM-___>` | `<IDs>` | `<value>` | `<value>` | `<yes / no / pending>` | `<condition>` |

## 10. Final Test Report

| Field | Value |
|---|---|
| Test Scope / Environment | `<summary or section links>` |
| Core Results | `<summary>` |
| Variation Results | `<summary>` |
| Stress Results | `<summary>` |
| Boundary Results | `<summary>` |
| Failure Taxonomy | `<actual failure IDs / groups>` |
| Refinements Performed | `<REV IDs>` |
| Retest Status | `<complete / incomplete; summary>` |
| Regression Status | `<PASS / FAIL / PENDING>` |
| Traceability Coverage | `<complete / gaps>` |
| Remaining Known Limitations | `<LIM IDs / none>` |
| Suite Verdict | `<PASS / PASS WITH ISSUES / FAIL>` |

## 11. Freeze Decision

| Criterion | Result | Evidence |
|---|---|---|
| Core Stability | `<pass / fail>` | `<TC IDs>` |
| Variation Stability / No Template Lock | `<pass / fail>` | `<TC IDs>` |
| Stress Stability | `<pass / fail>` | `<TC IDs>` |
| Boundary Control | `<pass / fail>` | `<TC IDs>` |
| Traceability Coverage | `<pass / fail>` | `<coverage section>` |
| Latest Regression | `<pass / fail / pending>` | `<REV / TC IDs>` |
| Scope Integrity | `<pass / fail>` | `<evidence>` |
| Known Limitations Accepted | `<yes / no / not applicable>` | `<LIM IDs>` |
| Required Cases Unblocked | `<yes / no>` | `<TC IDs / none>` |

| Field | Value |
|---|---|
| Freeze Candidate | `<yes / no>` |
| Final Decision | `<FREEZE V1 / FREEZE V1 WITH KNOWN LIMITATIONS / NOT READY>` |
| Freeze Rationale | `<evidence-based rationale>` |
| Frozen Version / Date | `<value or none>` |
| Recommended Future Tests | `<directions only; no invented results>` |
