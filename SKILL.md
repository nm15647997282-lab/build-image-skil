---
name: build-image-skill
description: Build, resume, audit, test, refine, regress, freeze, or unfreeze a reference-driven Image Generation Skill through a controlled six-phase pipeline. Use when a user wants to create or continue an Image Generation Skill from reference images. Do not use for directly generating or editing ordinary images, asset routing, visual direction, video work, or standalone prompt polishing.
---

# Build Image Skills from References

## Purpose and Boundary

Act as the orchestrator and execution controller for a reference-driven Image Skill Build.

```text
initialize or resume
→ locate current phase
→ load that phase's contract and protocol
→ create or update owned artifacts
→ maintain traceability
→ check the exit gate
→ update the manifest
→ advance, block, or roll back
→ audit
→ test, diagnose, refine, retest, regress
→ freeze
```

This Skill builds Image Generation Skills. It does not directly serve as a general image generator, image editor, asset router, visual director, video agent, or prompt-only tool.

Treat this file as orchestration logic, not as the System knowledge base. Load detailed rules from `System/` only when the current phase requires them. Instantiate files from `Templates/`; do not fill or modify source templates during a target Build.

## Operating Invariants

Preserve these principles throughout every Build:

1. Audit the complete Reference Set before analyzing or building.
2. Weight evidence; do not treat every Reference or observation as equal.
3. Do not invent unsupported style. `Insufficient Evidence` is preferable to filling gaps.
4. Separate Invariant, Allowed Variation, Incidental Detail, and Anti-pattern.
5. Keep descriptive Reference Analysis separate from executable Visual System rules.
6. Compile the target `SKILL.md` as a concise execution layer, not a knowledge dump.
7. Independently audit the compiled target Skill before generation testing.
8. Validate with real generation, diagnosis, minimal refinement, retest, and regression before Freeze.

References are the primary visual source of truth. Purpose and Scope define responsibility, not visual appearance. Optional context may clarify the task but cannot override Reference evidence. Keep the Builder domain-neutral: discover the target's visual rules instead of supplying fixed subjects, styles, materials, composition, lighting, vocabulary, or risks.

## Required Inputs

Read `input_contract.md` and validate:

- `skill_name`
- `purpose`
- `references_path`
- `scope_boundary`
- `optional_context`, if provided

Do not require additional visual fields. If required input is missing, contradictory, unreadable, or outside the user's authority, record the appropriate input state and stop for resolution.

## Start or Resume

First determine whether the target Build already has a `build_manifest.md`.

- If it exists, resume from it. Do not initialize a replacement.
- If it does not exist, initialize a new Build.
- Never infer progress from chat history, model memory, filenames alone, or historical implementations.

The manifest is the operational state source of truth. Artifacts and Traceability provide the evidence that the recorded state is valid.

## Initialize a New Build

1. Validate the input with `input_contract.md`.
2. Create the user-authorized target Build workspace.
3. Copy `Templates/build_manifest.md` into the target Build and fill the copy.
4. Copy `Templates/traceability.yaml` into the target Build and fill only its `meta` values initially.
5. Record the accepted input, artifact paths, Build ID, and version.
6. Set:

```text
Current Phase: Phase 1A — Reference Set Audit
Phase Status: NOT STARTED or IN PROGRESS
Exit Gate Status: NOT CHECKED
Freeze Status: NOT READY
```

7. Set `Next Required Action` to the concrete Phase 1A action.
8. Do not create downstream formal artifacts before their owner phase starts.

If initialization cannot complete, record the blocker and do not start Phase 1A.

## Resume an Existing Build

Read the manifest before any phase work. Resolve:

- Current Phase and Phase Status
- Exit Gate Status
- artifact paths and recorded versions
- blockers and Next Required Action
- active rollback and Resume Condition
- Audit, Test, Regression, and Freeze status
- Known Issues and Known Limitations

Verify that the artifacts needed by the recorded state exist and match the versions the manifest claims. If state and files disagree, do not guess which is newer. Mark the state blocked or invalidated, identify the responsible phase, and record the resolution action.

If the Build is Frozen, make no changes unless an Unfreeze trigger exists and the requested work authorizes a new revision cycle.

## State Machine

The only normal forward chain is:

```text
Phase 1A — Reference Set Audit
→ Phase 1B — Reference Analysis
→ Phase 2 — Visual System Specification
→ Phase 3A — Build Skill v1
→ Phase 3B — Skill Consistency Audit
→ Phase 4 — Test + Refine + Freeze
→ Frozen
```

Any other forward jump is invalid. A formal rollback may move to the closest responsible phase, but the Build must then re-run every invalidated downstream gate in order.

## Phase Execution Loop

For every current phase:

1. Read `System/phase_contracts.md` for its Required Input, Responsibility, Required Output, Allowed Mutation, Forbidden Mutation, Exit Gate, failure conditions, and next phase.
2. Load only the phase-specific System and Template resources listed below.
3. Verify all required upstream gates remain valid.
4. Set the manifest Phase Status to `IN PROGRESS` and record the next action.
5. Execute only the current phase's responsibility.
6. Create or update only authorized artifacts and Traceability entities.
7. Validate the output against the phase Exit Gate.
8. Update the manifest with artifact status, gate result, blockers, and next action.
9. Advance only when the gate passes. Otherwise remain blocked or perform a recorded minimal rollback.

Creating a file does not complete a phase. Completion requires both the formal output and a passed Exit Gate.

## Phase 1A — Reference Set Audit

Load:

- `System/build_protocol.md`
- the Phase 1A contract in `System/phase_contracts.md`
- `System/traceability_spec.md`
- `Templates/reference_audit_template.md`
- the initialized current Traceability
- the raw Reference Set

Inventory the full set; classify References as Core, Supporting, Ambiguous, or Outlier; assess evidence weighting, contamination, subtype risk, and readiness. Instantiate the Reference Audit artifact and create stable REF identities plus any permitted audit observations in Traceability.

Do not perform full Reference Analysis or create visual, prompt, quality, Skill, or test rules.

Advance only when the Phase 1A readiness and Exit Gate permit Phase 1B.

## Phase 1B — Reference Analysis

Load:

- the Phase 1B contract
- `System/analysis_framework.md`
- `System/traceability_spec.md`
- `Templates/reference_analysis_template.md`
- the accepted Reference Audit and its recommended analysis set
- the relevant References

Run the Core Dimension pass, identify evidence-driven Adaptive candidates, apply the promotion threshold, and synthesize Core Visual Identity, recurring patterns, Invariants, Allowed Variations, Incidental Details, Anti-patterns, subtype status, confidence, contradictions, and insufficient evidence.

Create and link OBS, INV, VAR, and ANTI. Keep findings descriptive; do not assign rule strength or create Visual Rules early.

Advance only with `READY FOR VISUAL SYSTEM SPECIFICATION` and a passed Phase 1B Gate.

## Phase 2 — Visual System Specification

Load:

- the Phase 2 contract
- `System/visual_system_compiler.md`
- `System/traceability_spec.md`
- `Templates/visual_rules_template.md`
- `Templates/prompt_rules_template.md`
- `Templates/quality_rules_template.md`
- the accepted Analysis and current Traceability

Compile active INV, VAR, and ANTI into `visual_rules.md`, `prompt_rules.md`, and `quality_rules.md`. Follow the Visual System Compiler for rule admission, strength, priority, conflict resolution, variation preservation, prompt construction, quality evaluation, and readiness. Do not restate those definitions here.

Create and link VR, PR, and QR. Every formal rule must have legal upstream support; Prompt and Quality Rules cannot invent visual requirements.

Advance only with `READY FOR SKILL COMPILATION` and a passed Phase 2 Gate.

## Phase 3A — Build Skill v1

Load:

- the Phase 3A contract
- `System/skill_compiler.md`
- `System/traceability_spec.md`
- Target Purpose and Scope
- Reference Analysis
- Visual, Prompt, and Quality Rules
- current Traceability

Compile the target Image Skill's `SKILL.md` v1 Candidate as an execution layer. Preserve Core Visual Identity, active core Invariants, important Variations, necessary Anti-pattern Guardrails, rule strength, Prompt Construction, lightweight quality checks, revision guidance, and Scope Boundary.

Apply runtime relevance, safe merge, and justified omission. Do not concatenate the Analysis and System artifacts. Create and link SK entities for important execution rules.

Advance only when the Candidate is `READY FOR STATIC AUDIT` and the Phase 3A Gate passes. The Candidate is not Frozen.

## Phase 3B — Skill Consistency Audit

Load:

- the Phase 3B contract
- `System/audit_protocol.md`
- `System/traceability_spec.md`
- `Templates/skill_audit_template.md`
- References through the audited evidence hierarchy
- the Candidate and current Traceability

Perform an independent static comparison. Check Missing, Distorted, Unsupported, Redundant, Untraced Rule, Dropped Invariant, Orphan Quality Rule, Pending Test Coverage, Strength Distortion, Scope Leakage, variation and anti-pattern coverage, Overengineering, and Under-specification.

Apply only authorized minimal Candidate corrections, update SK Traceability, and re-run the required secondary audit. If the cause is upstream, record a rollback instead of silently rewriting the upstream artifact.

Advance only when the Verdict is `PASS` or Minor-only `PASS WITH ISSUES`, `Critical = 0`, `Major = 0`, and the Phase 3B Gate passes.

## Phase 4 — Test, Refine, Regress, and Freeze

Load:

- the Phase 4 contract
- `System/test_protocol.md`
- `System/traceability_spec.md`
- `Templates/test_suite_template.md`
- the audited Candidate
- Pending Test Coverage and current Traceability

Build evidence-linked cases:

```text
INV          → Core Case
VAR          → Variation Case
ANTI         → Stress Case
VAR Boundary → Boundary Case
```

Construct test prompts through the target Candidate's own Prompt Construction Logic. Define Expected Behavior before generation. Do not use manual prompt rescue, change standards after seeing outputs, or regenerate until a lucky result appears.

Execute the bounded real-generation plan and preserve every attempt. Evaluate Hard Fail before visual-family quality. Attribute failures as defined by `System/test_protocol.md`, diagnose through Traceability, and distinguish systematic failure, isolated variance, and input-specific difficulty.

For each evidence-supported correction:

```text
Observed Failure
→ Traceability
→ Root Cause
→ Closest Responsible Layer
→ Minimal Necessary Fix
→ Revalidate invalidated gates
→ Retest
→ Regression
```

Protect previously passing behavior, Core Invariants, Allowed Variation, and Anti-pattern boundaries. Reject test-specific overfitting.

Freeze only when the full Phase 4 Freeze Gate passes.

## Traceability Protocol

Maintain Traceability throughout the lifecycle, not as a final backfill:

```text
Phase 1A: REF
Phase 1B: OBS → INV / VAR / ANTI
Phase 2:  VR → PR / QR
Phase 3A: SK
Phase 4:  TC
```

The resulting chain is:

```text
REF → OBS → INV / VAR / ANTI → VR → PR / QR → SK → TC
```

Use `System/traceability_spec.md` and the instantiated `traceability.yaml`. Preserve stable IDs, many-to-many relationships, bidirectional links, locations, lifecycle status, and Revision Records.

Check only the coverage possible at the current phase. Do not require downstream IDs that the state machine has not yet authorized.

## Manifest Protocol

Update the instantiated manifest after:

- Build initialization
- phase start, block, exit check, completion, or invalidation
- rollback and resume
- Audit result
- Test result
- Refinement and gate revalidation
- Regression
- Freeze or Unfreeze

Keep it a state summary and navigation record. Store detailed analysis, rules, issues, prompts, outputs, and histories in their owner artifacts.

After every update, `Current Phase`, `Phase Status`, `Exit Gate Status`, blockers, artifact versions, and `Next Required Action` must agree.

## Exit Gates and Blocked State

Before any forward transition, require:

```text
Required Output exists and is readable
+ phase responsibility is covered
+ mutation rules were obeyed
+ current Traceability integrity is sufficient
+ Exit Gate passed
+ Manifest updated
```

If required input is missing, a gate fails, the Reference Set is not ready, Audit fails, a required test is blocked, or a systematic Critical failure remains:

1. Keep the current phase.
2. Set Phase Status to `BLOCKED`.
3. Record the blocker, evidence, owner phase, and affected artifacts.
4. Record one concrete Next Required Action.
5. Do not create the next phase's formal artifact or imply completion.

## Rollback and No Silent Mutation

When evidence points upstream:

```text
Failure Evidence
→ Root Cause
→ Closest Responsible Phase
→ Minimal Correction
→ Re-run Owner Exit Gate
→ Resume the forward pipeline
→ Re-audit, retest, and regress as required
```

Record Rollback From, Rollback To, reason, affected artifacts and gates, and Resume Condition in the manifest. Do not return to Phase 1A for every problem, and do not modify another phase's artifact silently.

Any Candidate change invalidates its current Static Audit. Any System Rule change returns to Phase 2 and then requires recompilation and re-audit. Move farther upstream only when evidence locates the root cause there.

## Freeze and Unfreeze

Do not Freeze because the Candidate exists, Static Audit passes, one image succeeds, or one Core Case passes.

Freeze requires the current criteria in `System/test_protocol.md`, including required coverage, resolved blocking failures, evidence-based refinements, passed Retest and Regression, current Static Audit, Scope integrity, final artifacts, and recorded limitations.

On Freeze:

- set `Current Phase: Frozen` and `Freeze Status: FROZEN`;
- record the frozen version and date;
- preserve the Final Test Report and tested artifact versions;
- record accepted Known Limitations and Freeze history.

Unfreeze when authorized changes affect References, Scope, the generation model, the core Visual System, or when new systematic failure evidence appears. Record the trigger, set `Freeze Status: UNFROZEN`, return to the closest responsible phase, and re-run all invalidated downstream gates through a new Freeze Decision.

## System Routing

| Need | Load |
|---|---|
| Global evidence, scope, and revision rules | `System/build_protocol.md` |
| Phase boundaries, ownership, gates, and rollback | `System/phase_contracts.md` |
| Core and Adaptive Reference Analysis | `System/analysis_framework.md` |
| IDs, relationships, integrity, and coverage | `System/traceability_spec.md` |
| Visual / Prompt / Quality compilation | `System/visual_system_compiler.md` |
| Target `SKILL.md` compilation | `System/skill_compiler.md` |
| Independent static consistency audit | `System/audit_protocol.md` |
| Generation test, diagnosis, refinement, regression, and Freeze | `System/test_protocol.md` |

Always load the current phase contract. Load other System files only when the active work or a traced upstream issue requires them.

## Template Routing

| Artifact Need | Instantiate From |
|---|---|
| Build state and resume point | `Templates/build_manifest.md` |
| Traceability relationship index | `Templates/traceability.yaml` |
| Phase 1A Reference Audit | `Templates/reference_audit_template.md` |
| Phase 1B Reference Analysis | `Templates/reference_analysis_template.md` |
| Phase 2 Visual Rules | `Templates/visual_rules_template.md` |
| Phase 2 Prompt Rules | `Templates/prompt_rules_template.md` |
| Phase 2 Quality Rules | `Templates/quality_rules_template.md` |
| Phase 3B Skill Audit | `Templates/skill_audit_template.md` |
| Phase 4 Test lifecycle and Final Report | `Templates/test_suite_template.md` |

## Expected Build Artifacts

A normal Build progressively produces:

- Build Manifest
- Traceability
- Reference Set Audit
- Reference Analysis
- Visual Rules
- Prompt Rules
- Quality Rules
- target `SKILL.md` Candidate
- Skill Audit
- Test Cases, Expected Behavior, Evaluation, and Results
- Refinement, Retest, and Regression records
- Final Test Report
- Freeze State

Their exact paths belong in the manifest. Do not assume completion from filenames alone.

## Completion Criteria

Treat the target Image Skill Build as complete only when:

- every phase in the normal chain has a valid gate;
- the final target artifacts are the versions actually audited and tested;
- required Traceability and test coverage are complete;
- no unresolved blocking issue or invalidated gate remains;
- Retest and Regression are complete for the latest revisions;
- the Final Test Report supports the Freeze Decision;
- the manifest states `Current Phase: Frozen` and `Freeze Status: FROZEN`.

Until then, report the actual current phase, blockers, and Next Required Action. Never substitute chat history, intention, or historical success for current Build evidence.
