# <target-skill> — Build Manifest

> Copy this template into a new target build. This file is the Build State Record and resume point; detailed evidence, rules, issues, and test results remain in their owner artifacts.

## 1. Build Identity

| Field | Value |
|---|---|
| Target Skill (`skill_name`) | `<required>` |
| Build ID | `<required>` |
| Build Version | `<required>` |
| Purpose | `<required>` |
| Scope Boundary | `<required; list or concise statement>` |
| References Path | `<required>` |
| Optional Context | `<optional or none>` |
| Last Updated | `<timestamp>` |

## 2. Current State

| Field | Value |
|---|---|
| Current Phase | `<Phase 1A — Reference Set Audit / Phase 1B — Reference Analysis / Phase 2 — Visual System Specification / Phase 3A — Build Skill v1 / Phase 3B — Skill Consistency Audit / Phase 4 — Test + Refine + Freeze / Frozen>` |
| Phase Status | `<NOT STARTED / IN PROGRESS / BLOCKED / READY FOR EXIT CHECK / COMPLETE>` |
| Exit Gate Status | `<NOT CHECKED / PASS / NOT PASSED / INVALIDATED>` |
| Last Completed Phase | `<phase or none>` |
| Blockers | `<IDs or concise summary / none>` |
| Next Required Action | `<one concrete next action>` |

## 3. Artifact Index

| Artifact | Path | Owner Phase | Status | Version / Updated |
|---|---|---|---|---|
| Accepted Build Input / Target Skill Brief | `<path>` | Initialization | `<status>` | `<value>` |
| Reference Set Audit | `<path>` | Phase 1A | `<status>` | `<value>` |
| Reference Analysis | `<path>` | Phase 1B | `<status>` | `<value>` |
| Visual Rules | `<path>` | Phase 2 | `<status>` | `<value>` |
| Prompt Rules | `<path>` | Phase 2 | `<status>` | `<value>` |
| Quality Rules | `<path>` | Phase 2 | `<status>` | `<value>` |
| Traceability | `<path>` | Cross-phase | `<status>` | `<value>` |
| Target `SKILL.md` Candidate | `<path>` | Phase 3A | `<status>` | `<value>` |
| Skill Audit | `<path>` | Phase 3B | `<status>` | `<value>` |
| Test Suite / Results | `<path>` | Phase 4 | `<status>` | `<value>` |
| Final Test Report | `<path>` | Phase 4 | `<status>` | `<value>` |

## 4. Reference State — Phase 1A

| Field | Value |
|---|---|
| Reference Readiness | `<NOT CHECKED / READY / READY WITH ISSUES / NOT READY>` |
| Core References | `<count; REF IDs>` |
| Supporting References | `<count; REF IDs>` |
| Ambiguous References | `<count; REF IDs>` |
| Outliers | `<count; REF IDs>` |
| Reference Set Issues | `<issue IDs or concise summary / none>` |
| Recommended Analysis Set | `<REF IDs or artifact location>` |

## 5. Analysis State — Phase 1B

| Field | Value |
|---|---|
| Analysis Verdict | `<NOT STARTED / READY FOR VISUAL SYSTEM SPECIFICATION / NOT READY / INVALIDATED>` |
| Confirmed Adaptive Dimensions | `<names or none>` |
| Active Invariants | `<count; INV IDs>` |
| Active Variations | `<count; VAR IDs>` |
| Active Anti-patterns | `<count; ANTI IDs>` |
| Open Evidence Issues | `<IDs or concise summary / none>` |

## 6. Visual System and Traceability — Phase 2+

| Field | Value |
|---|---|
| Visual System Status | `<NOT STARTED / IN PROGRESS / READY FOR SKILL COMPILATION / NOT READY / INVALIDATED>` |
| Traceability Status | `<NOT INITIALIZED / IN PROGRESS / COMPLETE / ISSUES FOUND>` |
| Untraced Rules | `<count; IDs>` |
| Dropped Invariants | `<count; IDs>` |
| Broken / Asymmetric Links | `<count; IDs or summary>` |
| Coverage Gaps | `<count; IDs or summary>` |

## 7. Skill Compilation and Static Audit — Phase 3

| Field | Value |
|---|---|
| Skill Compilation Status | `<NOT STARTED / IN PROGRESS / READY FOR STATIC AUDIT / BLOCKED / INVALIDATED>` |
| Candidate Version | `<version or none>` |
| Audit Status | `<NOT STARTED / PASS / PASS WITH ISSUES / FAIL / INVALIDATED>` |
| Critical Issues | `<count; IDs>` |
| Major Issues | `<count; IDs>` |
| Minor Issues | `<count; IDs>` |
| Pending Test Coverage | `<IDs or artifact location / none>` |

## 8. Test, Regression, and Freeze — Phase 4

| Field | Value |
|---|---|
| Test Status | `<NOT STARTED / IN PROGRESS / PASS / PASS WITH ISSUES / FAIL / BLOCKED / INVALIDATED>` |
| Core Coverage | `<covered / required; gaps>` |
| Variation Coverage | `<covered / required; gaps>` |
| Stress Coverage | `<covered / required; gaps>` |
| Boundary Coverage | `<covered / required; gaps>` |
| Regression Status | `<NOT REQUIRED / PENDING / PASS / FAIL / INVALIDATED>` |
| Freeze Status | `<NOT READY / CANDIDATE / FROZEN / UNFROZEN>` |
| Final Freeze Decision | `<FREEZE V1 / FREEZE V1 WITH KNOWN LIMITATIONS / NOT READY / not issued>` |
| Frozen Version | `<version or none>` |
| Freeze Date | `<date or none>` |

## 9. Known Issues and Limitations

### Open Issues

| ID | Severity | Owner Phase | Summary | Required Resolution |
|---|---|---|---|---|
| `<ID>` | `<Critical / Major / Minor>` | `<phase>` | `<concise>` | `<action>` |

### Known Limitations

| ID | Evidence | Impact / Scope | Accepted For Freeze | Future Trigger |
|---|---|---|---|---|
| `<ID>` | `<artifact / TC IDs>` | `<concise>` | `<yes / no / pending>` | `<condition>` |

## 10. Active Rollback

| Field | Value |
|---|---|
| Rollback Active | `<yes / no>` |
| Rollback From | `<phase or none>` |
| Rollback To | `<closest responsible phase or none>` |
| Reason / Evidence | `<issue and evidence IDs>` |
| Affected Artifacts / Gates | `<concise list>` |
| Resume Condition | `<required gate and action>` |

## 11. Freeze History

Append one row for each completed Freeze or Unfreeze event; do not replace earlier rows.

| Version | Event | Date | Final Report | Known Limitations | Reason / Trigger |
|---|---|---|---|---|---|
| `<version>` | `<FROZEN / UNFROZEN>` | `<date>` | `<path>` | `<IDs or none>` | `<concise>` |

## 12. Last State Change

| Field | Value |
|---|---|
| Event | `<START / EXIT / BLOCK / ROLLBACK / REFINEMENT / FREEZE / UNFREEZE>` |
| From → To | `<state transition>` |
| Evidence / Artifact | `<IDs or paths>` |
| Result | `<concise>` |
| Updated By / At | `<actor; timestamp>` |

