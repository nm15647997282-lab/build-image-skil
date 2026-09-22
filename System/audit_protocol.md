# build-image-skill — Static Audit Protocol

## 1. Purpose

本文件定义 `Phase 3B — Skill Consistency Audit` 的独立静态审计方法。

Audit 的唯一主要问题是：

> 当前 `SKILL.md` v1 Candidate 是否忠实、充分且紧凑地编译了已经成立的上游视觉系统？

Audit 验证编译正确性，不重新设计目标 Visual System，不运行图片生成，不创建正式 Test Case，也不 Freeze Skill。

## 2. Independence and Evidence Hierarchy

Audit 必须执行独立的 evidence-to-execution comparison，不能只接受 Compiler 的自检结论或沿用其省略理由。

证据层级固定为：

```text
References
↓
Reference Set Audit
↓
Reference Analysis
↓
Visual / Prompt / Quality Rules
↓
Traceability
↓
SKILL.md v1 Candidate
```

审计应先比较 Candidate 与其直接上游 System Rules，再在发现含义、证据或来源疑问时沿链向上核验。若 Candidate 与上游冲突，默认先按编译问题处理；只有明确证据证明上游 Artifact 自身错误时，才启动 Minimal Upstream Rollback。

“独立”要求使用新的覆盖清单与逐链核对，不要求复制 Reference Analysis，也不要求由另一套工具或人员执行。

## 3. Audit Admission and Scope

进入 Phase 3B 前必须具备：

- 已接受的 Target Skill Brief；
- 完整 Reference Set 与通过 Gate 的 Reference Set Audit；
- 通过 Gate 的 Reference Analysis；
- 通过 Phase 2 Gate 的 Visual、Prompt、Quality Rules；
- 当前 Build 的 Traceability；
- 已通过 Phase 3A Exit、状态为 `READY FOR STATIC AUDIT` 的 `SKILL.md` v1 Candidate。

任一 Required Input 缺失、上游 Gate 失效或 Candidate 仍在编译中时，不得签发 Verdict。

Audit 范围包括：

- Candidate 对 Purpose / Scope 的保真；
- Core Identity、INV、VAR、ANTI 的执行覆盖；
- VR / PR / QR 的运行能力是否进入 SK；
- Rule Strength 与 Context 是否保持；
- Prompt Construction、Quality Check 与 Revision Guidance 是否足够且有依据；
- Traceability 完整性；
- 压缩是否造成遗漏、失真、无依据新增或冗余；
- Phase 4 所需但尚未创建的 Test Coverage 声明。

## 4. Audit Method

Phase 3B 按以下顺序执行：

1. **Validate inputs and gates**：确认所有 Required Input 与状态有效；
2. **Lock audit baseline**：记录被审版本与对应上游 Artifact 版本；
3. **Build upstream coverage inventory**：列出 active core / important INV、VAR、ANTI、VR、PR、QR；
4. **Map SK coverage**：确认每项上游能力在 Candidate 中的实际位置、含义、强度与 Context；
5. **Audit candidate additions**：从每条核心 SK 反向检查是否有合法来源；
6. **Run issue-class audits**：Missing、Distorted、Unsupported、Redundant 及专项检查；
7. **Run traceability integrity audit**：检查链接、状态、位置、双向一致性与强度传递；
8. **Record Pending Test Coverage**：识别 Phase 4 必须覆盖的 INV、VAR、ANTI、SK，不创建 TC；
9. **Assign severity and corrections**：按执行后果定级，给出最小必要修正；
10. **Apply authorized corrections when needed**：只修正 Candidate 与相应 SK Traceability；
11. **Re-run quick static audit**：任何修正后复查全部受影响项及回归风险；
12. **Issue verdict and gate decision**：输出正式 Audit Artifact 与 Phase 4 准入结论。

Audit 必须检查实际语义与能力，不能以标题存在、关键词出现或 ID 数量替代覆盖证明。

## 5. Core Issue Classes

### 5.1 Missing

上游重要规则或执行能力存在，但 Candidate 中没有有效表达。

包括：

- Core INV 没有运行时覆盖；
- important VAR 或 ANTI 没有 Skill 支持；
- 核心 PR 没有进入 Prompt Construction；
- 核心 QR 没有进入 Quality / Generation Check；
- Scope Boundary 未表达，导致职责无法约束；
- 文字存在但不可执行、不可检查，形成实质缺失。

### 5.2 Distorted

Candidate 提到了上游规则，但改变了其意义、范围、Context、Strength 或角色。

包括：

- INV 被弱化；
- VAR 被写死或当成异常；
- ANTI 被无依据升级为绝对禁止；
- PR 改变 VR 的视觉目标；
- QR 被压缩成无法判断的口号；
- 安全 merge 抹去了来源之间的重要差异。

### 5.3 Unsupported

Candidate 新增了无法沿正式链回到 active VR / PR / QR 与 Reference Evidence 的执行规则、视觉要求、风格词义或职责。

Unsupported 不因“通常有用”“更美观”或来自历史 Skill 而合法。核心执行层中的 Unsupported Rule 至少是 Major；若改变目标身份、职责或主要行为，可以是 Critical。

### 5.4 Redundant

Candidate 中存在不会增加执行能力、判断能力或边界保护的重复内容。

包括：

- 同义规则多次出现；
- 长篇重复解释；
- 重复的 Prompt / Guardrail；
- 不必要 metadata、Evidence dump 或规则索引正文；
- 多个章节执行完全相同的动作。

Redundant 通常为 Minor；若大量冗余造成冲突、遮蔽优先级或使 Candidate 无法稳定执行，则升级为 Major。

## 6. Untraced Rule

任何 active SK 必须至少连接一个 active VR、PR 或 QR，并能继续回溯到 INV / VAR / ANTI、OBS 与 REF。

以下均标记 `Untraced Rule`：

- SK 的 `source_rules` 为空；
- source ID 不存在、Prefix 错误或状态不可用；
- 链在 VR / PR / QR 处中断；
- Skill 正文中的核心执行规则没有对应 SK；
- SK statement 与其 source rules 不相符；
- 通过 loose note 或 Brief 绕过正式主链。

核心 Untraced Rule 同时按 Unsupported 处理。普通非执行说明若无来源，应删除或明确保持为非规则背景，不能伪装成正式 SK。

## 7. Dropped Invariant

对每个 active INV 执行覆盖核对：

```text
INV → VR → SK → Candidate runtime behavior
```

若 core 或 identity-critical INV 没有进入 Candidate、只剩空泛标签、被无声弱化，或没有 Prompt / Check 能力支持，则标记 `Dropped Invariant`。

Dropped core INV 通常为 Critical；重要但非核心的 INV 缺失通常为 Major。不得以 Candidate 更短为理由降级。

## 8. Orphan Quality Rule

每个 active QR 必须连接至少一个 active VR，并只检查该 VR 已定义的视觉要求。

以下标记 `Orphan Quality Rule`：

- QR 没有 `source_visual_rules`；
- QR 检查上游未定义的视觉标准；
- Candidate 的 Quality Check 新增了独立审美门槛；
- QR 与其来源 VR 的 Context、范围或强度不相容。

如果 Orphan QR 已进入 Candidate，应同时检查 Unsupported 与 Strength Distortion。Audit 不通过删除对应合法 VR 来消除孤儿关系。

## 9. Untested Invariant and Pending Test Coverage

Phase 3B 尚未创建正式 TC。active INV 暂无 TC，不会仅因此判定 Audit 失败，而应记录为：

```text
Pending Test Coverage
```

Audit Artifact 的 Pending Test Coverage 至少列出：

- 待验证的 INV / VAR / ANTI / SK ID；
- 需要验证的行为或风险；
- 建议的未来 case family：`Core / Variation / Stress / Boundary`；
- 为什么仅靠 Static Audit 无法确认；
- Phase 4 需要保护的相关 Strength、Context 或 Variation Boundary。

本阶段不分配 `TC-*` ID，不编写生成 Prompt、次数、评分或结果。

如果一个核心 INV 被明确认定没有可行的观察或测试路径，或系统错误声称其已经由不存在的 TC 覆盖，则标记 `Untested Invariant Risk`。风险严重度根据其对身份与未来验证的影响判断；无法验证核心身份通常为 Major，并阻断进入 Phase 4，直至上游定义可评估行为或按 Minimal Rollback 修正。

## 10. Strength Distortion

逐链比较：

```text
INV / VAR / ANTI
→ VR
→ PR / QR
→ SK
→ Candidate wording and behavior
```

重点检查：

```text
MAY → SHOULD / MUST
SHOULD → MUST
AVOID → DO NOT
MUST → weak suggestion
DO NOT → optional guidance
```

还应检查不同 Strength 的规则在 merge 后是否被单一语气覆盖，以及 Priority 是否被误当作 Strength。

无新增正式 Evidence 支持的加强、削弱或角色改变，均标记 `Strength Distortion`。涉及 core identity、重要 Variation 或 scope-critical guardrail 时至少为 Major；造成身份或职责反转时为 Critical。

## 11. Scope Leakage

Audit 必须把 Candidate 的每项职责与 `purpose / scope_boundary` 对照。

Scope Leakage 包括：

- 新增未授权的输入或输出责任；
- 加入 routing、semantic decision、video behavior、animation、usage decision 或外部系统行为；
- 把 optional context 当作视觉 Source of Truth；
- 把目标 Skill 扩展到未定义的媒介、对象或流程；
- 通过 Guardrail 偷偷重写 Purpose。

具体 leakage 由当前目标 Scope 决定，Builder 不预置一种固定 Scope。会改变目标 Skill 职责的 leakage 通常为 Critical；局部越界但尚未改变主要职责的为 Major。

## 12. Variation Preservation Audit

对每个 active core / important VAR 检查：

1. Candidate 是否保留该变化能力；
2. 合法 options / range 是否仍存在；
3. 变化时保持的 INV 是否明确；
4. Prompt Construction 是否能选择不同合法表现；
5. Quality Check 是否把合法变化与漂移区分；
6. Guardrail 是否误伤 VAR；
7. `VAR → VR → SK` 是否完整；
8. MAY 是否被无依据加强。

VAR 消失、被固定、被降级为异常、被 ANTI 错误覆盖或只保留默认值，均标记 `Variation Preservation Failure` / `Variation Collapse`，通常为 Major。若变化本身是目标身份的重要组成且被整体删除，可以升级为 Critical。

## 13. Anti-pattern Coverage Audit

对每个 active core / important ANTI 检查：

- 是否存在合法 VR Guardrail；
- 必要的 PR Guardrail 是否进入 Prompt Construction；
- Candidate 中是否有清楚、上下文正确的保护；
- AVOID / DO NOT 的强度是否保持；
- Guardrail 是否足以防止已知高风险漂移；
- 是否因反漂移而形成过度禁止或伤害 VAR。

重要 ANTI 没有 Guardrail，标记 `Anti-pattern Coverage Gap`，通常为 Major；导致核心身份或 Scope 失守时可为 Critical。过度 Guardrail 同时按 Distorted、Strength Distortion 或 Variation Failure 记录。

## 14. Prompt Rule Coverage Audit

Audit 不要求每条 PR 逐字复制进 Candidate，而要验证其执行能力：

- 核心 VR 是否有可用 Prompt expression；
- Candidate 是否说明如何选择、排序和组织适用规则；
- 具体可见描述是否替代纯抽象风格词；
- VAR 是否能在 Prompt 中被合法表达；
- 相关 Guardrails 是否能按 Context 使用；
- Prompt language 是否引入 unsupported visual content；
- Candidate 是否退化为固定 production prompt 或无结构词表。

缺少决定核心生成行为的 PR 能力，通常为 Major；Prompt Construction 整体缺失或无法执行时为 Critical。

## 15. Quality Rule Coverage Audit

Audit 检查核心 QR 是否在以下运行时模块中得到足够支持：

```text
Generation Check
Quality Check
Revision Guidance
```

至少确认：

- Core INV 有可观察检查；
- VAR validity 可区分；
- ANTI contamination 与 Scope violation 可识别；
- 上游 Hard Failure 没有被弱化；
- `PASS / REVISE / FAIL` 的运行时判断没有新增标准；
- 高频重要偏差拥有可执行的修订方向，若上游表明其为必要能力。

Candidate 不需复制完整 Rubric。若压缩后无法判断重要失败，标记 `Quality Rule Coverage Gap`，通常为 Major；若只缺少非关键细节，可为 Minor。

## 16. Traceability Integrity Audit

Traceability 定义以 `traceability_spec.md` 为准。本 Protocol 不创建第二套 Schema。

Phase 3B 至少检查：

- `Untraced Rule`；
- `Dropped Invariant`；
- `Variation Coverage Gap / Variation Collapse`；
- `Anti-pattern Coverage Gap`；
- `Orphan Quality Rule`；
- `Strength Distortion`；
- `Evidence Gap`；
- `Broken Link`；
- `Asymmetric Link`；
- `Invalid Active Dependency`；
- SK `location` 是否指向实际 Candidate 内容；
- merge 是否保留全部 `source_rules`；
- deprecated / rejected ID 是否被错误复用；
- Candidate 修订是否有必要的 Revision Record。

TC 尚未创建造成的空覆盖按 Pending Test Coverage 处理；除此之外，不得用“Phase 4 会解决”掩盖当前 SK 链路错误。

## 17. Overengineering Audit

以下内容标记 `Overengineering`：

- 章节数量明显超过当前 Visual System 所需；
- 同一规则、Guardrail 或检查反复出现；
- 长篇视觉理论、Evidence Explanation 或 Reference 报告；
- 巨型 Vocabulary List；
- 完整评分系统、Traceability dump 或不必要 metadata；
- 把 Phase 4 的 Test / Regression 流程塞入 Candidate；
- 对运行时没有帮助的抽象层与配置。

局部冗余通常为 Minor。若复杂度制造冲突、遮蔽关键强度、降低可执行性或让模型无法识别主路径，则为 Major。

## 18. Under-specification Audit

以下内容标记 `Under-specification`：

- 只要求“follow references”“keep coherent”或其他空泛目标；
- 缺少 Core Visual Logic；
- Core INV 只剩标签；
- Allowed Variation、Guardrail 或 Scope 不可操作；
- Prompt Construction 缺失；
- Generation / Quality Check 无法判断重要偏差；
- 合并过度，多个可独立失败的机制被压成一句；
- Skill 依赖执行时重新阅读全部 System 才能工作。

影响主要生成路径时通常为 Major；Candidate 整体无法稳定执行时为 Critical。

## 19. Issue Record

每个 Audit Issue 至少记录：

- `issue_id`；
- issue class；
- severity；
- Candidate location / SK ID；
- affected upstream IDs；
- observed mismatch；
- execution or identity impact；
- required minimal correction；
- owner layer；
- status：open / corrected / accepted minor；
- recheck result。

Issue ID 属于 Audit Artifact，不改变 `traceability.yaml` Schema。相同根因造成多个表象时可以合并为一项，但必须列出全部受影响规则；不同 Strength、Context 或修复动作的问题不得为减少数量而合并。

## 20. Severity

Severity 按问题对执行、身份、Scope、Variation 与证据链的后果判断，不按文字长度或问题数量机械分配。

### 20.1 Critical

会导致以下任一后果：

- 目标 Skill 主要职责错误或严重 Scope Drift；
- Core Visual Identity 丢失或反转；
- core / identity-critical INV 被丢弃；
- 大量或核心 Unsupported Rule 改写 Visual System；
- Prompt Construction 整体无法稳定执行；
- 主要 Traceability 失效，无法证明 Candidate 来源；
- Candidate 整体 Under-specified，或已不再是同一目标 Skill。

Critical 必须修复；未解决时 Verdict 为 `FAIL`。

### 20.2 Major

会导致以下任一后果：

- Visual Stability 明显下降；
- important VAR 被写死、删除或误判；
- 核心 Prompt Construction 不完整；
- Rule Strength 发生实质失真；
- Quality Check 无法判断重要问题；
- important ANTI 无 Guardrail；
- 单项 Unsupported execution rule 影响正式行为；
- Traceability 的重要链路断裂；
- Candidate 过度复杂或过度压缩到影响执行。

Major 必须修复；未解决时 Verdict 为 `FAIL`。

### 20.3 Minor

不改变核心行为、身份、Scope、Strength 或 Variation，例如：

- 局部重复；
- wording 不够清楚但含义仍可执行；
- 次序或定位不理想；
- 非关键说明冗余；
- 不影响执行的小型链接或格式问题。

Minor 可以修正，也可以在不影响 Gate 的前提下明确保留为 issue。不能把多个共同造成执行失效的 Minor 分散记录以规避 Major。

## 21. Verdict

正式 Verdict 只有：

```text
PASS
PASS WITH ISSUES
FAIL
```

### PASS

- `Critical = 0`；
- `Major = 0`；
- 没有值得修正的实质 Minor；
- 所有必需修正已经完成并通过复核。

### PASS WITH ISSUES

- `Critical = 0`；
- `Major = 0`；
- 只剩少量、已记录且不影响运行与后续测试的 Minor；
- 所有必需修正已经完成并通过复核。

在 Phase 3B Exit Gate 中，这个状态等价于：

```text
PASS WITH MINOR ISSUES
```

它不是允许保留 Major 的条件性通过。

### FAIL

存在任意未解决：

```text
Critical
或
Major
```

Required Input / Gate 无效、无法证明主要规则来源、无法在当前责任层完成必要修正，或修正后仍重复出现阻断性失真，也必须 `FAIL` 或保持 Phase 3B blocked。

## 22. Correction Authority

Phase 3B 默认可以：

- 对 Target `SKILL.md` Candidate 做 Minimal Necessary Correction；
- 同步更新受影响 SK 的 statement、source links、strength、location、status 与 Revision Record；
- 删除 Candidate 中无依据或重复的执行内容；
- 恢复被遗漏、弱化或写死的上游含义；
- 对修正后的 Candidate 重新审计。

修正必须由现有上游证据支持，并限制在解决已记录 Issue 的最小范围。

Phase 3B 默认不得：

- 修改 Reference Set；
- 静默重写 Reference Audit、Reference Analysis、Visual Rules、Prompt Rules 或 Quality Rules；
- 新增 Visual Style、Evidence、Vocabulary 或职责；
- 通过删除合法 VAR 让 Candidate 更容易通过；
- 大规模重新设计 Visual System；
- 创建 TC、运行生成测试或 Freeze Skill。

## 23. Upstream Issue and Minimal Rollback

若 Audit 发现根因不在 Candidate，而在上游，应记录 `Upstream Issue`，至少包含：

- 触发 Evidence；
- Root Cause 判断；
- 最近的 Owner Phase；
- 计划的最小修订；
- 受影响的下游 Gates；
- 恢复后需要重新执行的编译与审计。

然后按 `phase_contracts.md` 执行：

```text
Failure Evidence
↓
Closest Responsible Phase
↓
Minimal Correction
↓
Re-run Owner Exit Gate
↓
Recompile Candidate
↓
Re-run Phase 3B
```

Audit 不得为了给 Candidate 签发通过而在 Phase 3B 静默改写上游。Root Cause 不清时保持当前 Phase 继续诊断，不猜测式回退。

## 24. Secondary Validation After Correction

只要 Candidate 或 SK Traceability 被修改，就必须执行快速 Static Re-audit。至少复查：

- 原 Issue 是否真正关闭；
- `Critical = 0`、`Major = 0`；
- 没有新增 Unsupported Rule；
- 没有新的 Missing / Distorted / Redundant；
- Strength 与 Priority 仍保持；
- VAR 没有因修复被删除、写死或被 Guardrail 误伤；
- Scope 没有扩大；
- INV / ANTI / Prompt / Quality Coverage 仍成立；
- Traceability links、location、status 与 Revision Record 一致；
- 修正没有造成新的 Under-specification 或 Overengineering。

如果修正影响多个模块，快速复核必须扩大到全部受影响模块，不能只检查改动句子。复核结果写入同一 Audit Artifact。

## 25. Audit Artifact Requirements

正式 Skill Audit Artifact 至少包含：

1. Audit scope 与被审版本；
2. 使用的 Evidence / Artifact 版本；
3. 上游 Coverage Inventory 与 SK Mapping；
4. Issue Register；
5. Traceability Integrity 结果；
6. INV / VAR / ANTI Coverage 结果；
7. Prompt Rule 与 Quality Rule Coverage 结果；
8. Scope、Strength、Overengineering、Under-specification 结果；
9. Required Corrections 与实际修订；
10. Secondary Validation 结果；
11. Pending Test Coverage；
12. `Critical / Major / Minor` 计数；
13. Verdict；
14. 是否允许进入 Phase 4 的明确结论；
15. Upstream Issue / Rollback，若有。

本 Protocol 不规定文件名、表格样式或固定章节数量，只规定审计信息必须可核验。

## 26. Phase 3B Exit Gate

只有同时满足以下条件，才允许进入 `Phase 4 — Test + Refine + Freeze`：

- Skill Audit Artifact 已完成；
- Verdict 为 `PASS`，或为只含 Minor 的 `PASS WITH ISSUES`（即 `PASS WITH MINOR ISSUES`）；
- `Critical = 0`；
- `Major = 0`；
- 所有 Required Corrections 已完成；
- 任何 Candidate 修订已通过 Secondary Validation；
- 不存在已知 Unsupported Rule、Dropped core INV、Variation Collapse、重要 Anti-pattern Gap、Scope Leakage 或阻断性 Traceability Error；
- Candidate 仍是紧凑、可执行的 execution layer；
- Pending Test Coverage 已记录，但本阶段没有伪造 TC 或测试结果；
- 未执行任何 Phase 3B Forbidden Mutation。

若 Verdict 为 `FAIL`、存在未解决 Critical / Major、上游 Gate 失效，或 Audit 无法在不扩大 Scope / 发明规则的情况下通过，则 Build 停留在 Phase 3B 或执行 Minimal Upstream Rollback。

Phase 3A 自检、人工口头确认、历史 Skill 成功或“看起来合理”均不能替代本 Gate。

## 27. Interface with Phase 4

Phase 3B 只向未来 Test Protocol 交付：

- 已通过静态审计的 `SKILL.md` Candidate；
- Skill Audit Artifact 与 Verdict；
- Pending Test Coverage；
- 已知 Minor Issues；
- 需要在真实生成中验证的 INV、VAR、ANTI、SK 与边界风险。

Phase 4 再负责创建 `TC-*`、Core / Variation / Stress / Boundary Cases、真实生成结果、Diagnosis、Refinement、Retest、Regression 与 Freeze Decision。

Static PASS 只证明“编译在文档与追溯层面成立”，不证明真实生成表现已经稳定。

## 28. Audit Boundary

本文件严格属于 Phase 3B。它不负责：

- 再做一次 Reference Analysis；
- 重新设计 Visual / Prompt / Quality System；
- 创建 `System/test_protocol.md` 或 `Templates/build_manifest.md`；
- 创建正式 TC 或 Test Artifact；
- 执行图片生成、Historical Backtest、Refinement 或 Regression；
- 修改历史成功 Skill；
- Freeze 任何 Skill；
- 重新设计 Traceability Schema。

