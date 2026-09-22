# build-image-skill — Phase Contracts

## 1. Purpose

本文件把 `build-image-skill` 的构建流程定义为正式 Six-Phase State Machine。

每个 Phase 都是一个具有明确进入条件、单一主要职责、正式输出、写权限与 Exit Gate 的 Build State，而不是普通文档章节。只有当前 Phase 的 Exit Gate 通过后，Build 才能进入唯一正常下一阶段。

本文件受以下上游合同约束：

- `project_brief.md`：定义 Builder 目标与六阶段架构；
- `input_contract.md`：定义 Build 开始前的最低输入；
- `System/build_protocol.md`：定义 Reference-first、证据层级、阶段隔离与最小修订原则。

本文件只定义 Workflow State、Phase Boundary 与 Phase Gate。它不定义具体分析维度、Traceability Schema、规则 Schema、Audit Rubric、Test Suite 或 Artifact 模板。

## 2. State Machine Overview

正式状态链为：

```text
Build Initialization
↓
Phase 1A — Reference Set Audit
↓
Phase 1B — Reference Analysis
↓
Phase 2 — Visual System Specification
↓
Phase 3A — Build Skill v1
↓
Phase 3B — Skill Consistency Audit
↓
Phase 4 — Test + Refine + Freeze
↓
Frozen
```

六个正式主 Phase 固定为：

1. Phase 1A — Reference Set Audit；
2. Phase 1B — Reference Analysis；
3. Phase 2 — Visual System Specification；
4. Phase 3A — Build Skill v1；
5. Phase 3B — Skill Consistency Audit；
6. Phase 4 — Test + Refine + Freeze。

`Build Initialization` 是进入状态机前的输入确认状态，`Frozen` 是终止状态；二者不增加新的主 Phase。`Blocked` 或 `Failure` 表示当前 Phase 未通过 Gate，也不构成额外主 Phase。

## 3. Contract Terms

### 3.1 Accepted Build Input

满足 `input_contract.md` 并得到 `ACCEPTED` 结论的本次 Build 输入实例。它至少包含：

- `skill_name`；
- `purpose`；
- `references_path`；
- `scope_boundary`；
- 可选的 `optional_context`。

### 3.2 Target Skill Brief

Accepted Build Input 中描述目标 Skill 职责、范围与辅助背景的内容。它是本次 Build 的任务边界，不是视觉来源，也不要求成为独立文件。

### 3.3 Reference Set

`references_path` 指向的候选 Reference Images。它是受保护的上游视觉证据，不是任一 Phase 可以随意修改的 Build Artifact。

### 3.4 Build Artifact

某个 Owner Phase 正式创建、供下游消费的构建产物。本文件只定义 Artifact 类型与职责，不预设全部文件名、目录结构或 Schema。

### 3.5 Build State Record

用于记录当前 Phase、Gate 结果、Block 原因、Rollback 原因与 Freeze 状态的概念性状态记录。具体 Manifest 或 Schema 由后续工作定义；本阶段不创建它。

## 4. Global Transition Rules

### 4.1 Normal Forward Order

唯一正常前进顺序为：

```text
1A → 1B → 2 → 3A → 3B → 4 → Frozen
```

任何 Phase 只能在自身 Exit Gate 通过后进入 `Next Phase`。已有下游草稿、历史文件或人工判断不能替代当前 Gate。

### 4.2 Required Input Rule

进入 Phase 前，全部 Required Input 必须：

- 存在且可读取；
- 属于当前 Build；
- 已通过其 Owner Phase 的 Exit Gate；
- 未被未记录的下游修改污染。

Required Input 缺失、无效或来源不明时，当前 Phase 不得开始。

### 4.3 Phase Isolation Rule

当前 Phase 只能执行其 `Responsibility`，并只能进行 `Allowed Mutation`。任何未明确授权的写入默认禁止。

尚未到达的下游 Artifact 不得提前创建；已通过 Gate 的上游 Artifact 不得为方便当前工作而被静默改写。

### 4.4 Gate Invalidation Rule

如果已通过 Gate 的 Artifact 后续被正式修订：

1. 该 Artifact 原 Gate 结果失效；
2. 从其 Owner Phase 开始重新验证；
3. 所有依赖该 Artifact 的下游 Gate 均视为待重新通过；
4. Build 按正常顺序重新前进，直到回到原进度；
5. Phase 4 中发生的修订必须完成相应 Regression 后才能 Freeze。

### 4.5 No Silent Advancement

Gate 未明确记录为通过时，默认状态是仍停留在当前 Phase。`READY WITH ISSUES`、`PASS WITH ISSUES` 等条件性结果只有在本合同明确允许且阻断项为零时，才可推进。

## 5. Phase 1A — Reference Set Audit

### Phase Name

`Phase 1A — Reference Set Audit`

### Purpose

判断当前 Reference Set 是否可靠，以及哪些 References 应成为后续视觉分析的主要证据。

### Required Input

- `input_contract.md` 所定义的 Build Input Contract；
- 状态为 `ACCEPTED` 的 Build Input；
- Target Skill Brief；
- 可读取的完整 Reference Set。

本 Phase 不需要 Reference Analysis、Visual System、`SKILL.md` 或 Test Artifact。

### Responsibility

本 Phase 唯一主要负责回答：

> 哪些 Evidence 值得信，当前证据是否足以进入正式分析？

职责包括：

- 检查全部可用 References，而不是抽样；
- 判断 Reference Set 的整体一致性；
- 分类 `Core / Supporting / Ambiguous / Outlier`；
- 建立必要的证据频率与权重判断；
- 检查污染、明显子类型与证据覆盖；
- 判断进入 Reference Analysis 的准备度；
- 明确推荐分析集合与边界对照集合。

本 Phase 不负责解释完整视觉语言，也不负责生成执行规则。

### Required Output

正式 **Reference Set Audit Artifact**，至少能够表达：

- Reference classification；
- evidence weighting；
- contamination risk；
- subtype status；
- missing coverage；
- readiness verdict；
- recommended analysis set。

Readiness Verdict 使用：

- `READY`；
- `READY WITH ISSUES`；
- `NOT READY`。

### Allowed Mutation

- 创建或更新本次 Build 的 Reference Set Audit Artifact；
- 更新 Build State Record 中仅与 Phase 1A 相关的状态、Verdict 与 Block 原因。

### Forbidden Mutation

- 修改、删除、移动或重命名原 Reference Images；
- 未经用户授权补充或替换 Reference Set；
- 创建正式 Reference Analysis；
- 创建 Visual Rules、Prompt Rules 或 Quality Rules；
- 创建目标 `SKILL.md`；
- 创建 Skill Audit 或 Test Artifact；
- 生成测试图片。

### Exit Gate

只有同时满足以下条件，Gate 才通过：

- 全部可用 References 已被检查；
- Reference classification 已完成；
- evidence weighting 已建立，单例与高频证据未被混同；
- contamination、subtype 与 missing coverage 已检查；
- recommended analysis set 已明确；
- Verdict 为 `READY`，或为不存在阻断性问题的 `READY WITH ISSUES`；
- 未执行任何 Forbidden Mutation。

### Blocked / Failure Condition

以下任一情况出现时，Build 必须停留在 Phase 1A：

- Required Input 缺失或 Reference Set 不可读取；
- Reference 数量或覆盖不足以支持视觉家族判断；
- 多个冲突视觉方向无法可靠分组或定权；
- 关键污染无法隔离；
- Verdict 为 `NOT READY`；
- Target Skill Brief 与 Reference Set 的职责发生实质冲突且未解决。

Blocked 时只能补充、澄清或重新审核证据；不得通过降低标准强行进入下一 Phase。

### Next Phase

`Phase 1B — Reference Analysis`

## 6. Phase 1B — Reference Analysis

### Phase Name

`Phase 1B — Reference Analysis`

### Purpose

解释经审核 References 共享的视觉语言，并区分视觉核心、合法变化、偶发细节与边界。

### Required Input

- Target Skill Brief；
- 完整 Reference Set；
- 已通过 Phase 1A Exit Gate 的 Reference Set Audit Artifact。

Reference Set Audit 决定不同 References 在本 Phase 的分析权重；Outlier 只可作为边界对照，不得用于定义 Core Visual Identity。

### Responsibility

本 Phase 唯一主要负责回答：

> 可信 References 共同构成了怎样的视觉家族？

职责包括：

- 提炼 Core Visual Identity；
- 分析后续框架要求的通用视觉维度；
- 识别由当前证据支持的 Adaptive Dimensions；
- 汇总 recurring patterns；
- 区分 Invariant、Allowed Variation、Incidental Detail 与 Anti-pattern；
- 解释关键视觉机制，而不只堆叠形容词；
- 标记 Evidence Confidence 与 `Insufficient Evidence`。

本合同不在此固定具体 Core 或 Adaptive Dimensions；它们由后续 Analysis Framework 定义。

### Required Output

正式 **Reference Analysis Artifact**，能够表达：

- analysis scope 与证据权重；
- Core Visual Identity；
- evidence-supported dimensions 与 recurring patterns；
- Invariants；
- Allowed Variations；
- Incidental Details；
- Anti-patterns；
- subtype analysis；
- Evidence Confidence 与证据不足项；
- non-executable 的 Final Visual Definition。

### Allowed Mutation

- 创建或更新本次 Build 的 Reference Analysis Artifact；
- 更新 Build State Record 中仅与 Phase 1B 相关的状态与 Block 原因。

### Forbidden Mutation

- 修改 Reference Set；
- 静默修改 Phase 1A 的分类、权重或 readiness 结论；
- 把描述性分析直接写成 `MUST / SHOULD / MAY / AVOID / DO NOT` 等执行规则；
- 创建或修改 Visual Rules、Prompt Rules、Quality Rules；
- 创建目标 `SKILL.md`、Skill Audit 或 Test Artifact；
- 使用外部风格常识替代 Reference Evidence；
- 为证据不足项自动补写风格。

### Exit Gate

只有同时满足以下条件，Gate 才通过：

- 所有 Phase 1A 推荐的有效 References 已按权重完成分析；
- Core Visual Identity 已明确且有 Reference Evidence 支持；
- Invariant、Allowed Variation、Incidental Detail 与 Anti-pattern 已区分；
- 关键视觉机制已得到解释；
- Evidence Confidence 已表达；
- Adaptive Dimensions 已按证据识别，或明确记录无充分证据；
- 证据不足项已标记，而非被外部知识补齐；
- 输出仍是描述层，没有提前创建执行规格；
- 未执行任何 Forbidden Mutation。

### Blocked / Failure Condition

以下任一情况出现时，Build 必须停留在 Phase 1B 或按 Rollback Principle 返回 Phase 1A：

- Required Input 缺失或 Phase 1A Gate 无效；
- Core Visual Identity 无法从有效证据中成立；
- 关键结论主要依赖 Ambiguous / Outlier Evidence；
- 核心与变化仍无法区分；
- 发现 Reference Audit 存在影响分析的事实错误；
- Target Skill Brief 的视觉预设正在覆盖 References；
- 关键证据缺口使下一阶段无法形成可靠规则。

### Next Phase

`Phase 2 — Visual System Specification`

## 7. Phase 2 — Visual System Specification

### Phase Name

`Phase 2 — Visual System Specification`

### Purpose

把描述性的 Reference Analysis 转换为可执行、可表达、可评估的视觉系统。

### Required Input

- Target Skill Brief；
- 完整 Reference Set；
- 已通过 Phase 1A Exit Gate 的 Reference Set Audit Artifact；
- 已通过 Phase 1B Exit Gate 的 Reference Analysis Artifact；
- 如果未来已存在正式 Traceability Artifact，则将其作为条件性 Required Input；本合同不定义其 Schema。

### Responsibility

本 Phase 唯一主要负责回答：

> 未来生成时应如何稳定复现并判断已经分析出的视觉语言？

职责是把 descriptive findings 编译为三层系统：

- **Visual Rules**：视觉目标、规则强度、不变量、变化范围与边界；
- **Prompt Rules**：如何把视觉规则表达为稳定的生成指令；
- **Quality Rules**：如何判断输出是否仍属于目标 Visual Family。

转换必须保持 evidence support、rule strength、variation boundaries 与 anti-pattern protection。三层规则应可相互对应，但本阶段不建立正式 Traceability ID。

### Required Output

正式 Visual System Artifacts：

- **Visual Rules Artifact**；
- **Prompt Rules Artifact**；
- **Quality Rules Artifact**。

具体结构与 Schema 由后续 Visual System Compiler 定义。

### Allowed Mutation

- 创建或更新本 Phase 所拥有的三个 Visual System Artifacts；
- 为消除三层内部冲突，对本 Phase 产物进行受控修订；
- 更新 Build State Record 中仅与 Phase 2 相关的状态与 Block 原因。

### Forbidden Mutation

- 修改 Reference Set 或 Reference Set Audit；
- 无证据改写 Reference Analysis；
- 添加 Reference Analysis 未支持的视觉规则、参数或词汇；
- 创建目标 `SKILL.md`；
- 创建 Skill Audit 或 Test Artifact；
- 执行真实生成测试；
- 把分析层的不确定性伪装成强执行规则。

### Exit Gate

只有同时满足以下条件，Gate 才通过：

- Reference Analysis 的核心结论已被转换为可执行规则；
- Visual、Prompt、Quality 三层职责清楚且没有相互替代；
- Invariant、Allowed Variation 与 Anti-pattern 已按原证据强度表达；
- Prompt Rules 能表达核心 Visual Rules；
- Quality Rules 能检查核心 Visual Rules 与主要漂移风险；
- 关键规则不是不可执行的抽象形容词；
- 不存在明显 unsupported rule 或 rule-strength distortion；
- 三层之间不存在阻断性冲突；
- 未执行任何 Forbidden Mutation。

### Blocked / Failure Condition

以下任一情况出现时，Build 必须停留在 Phase 2 或回退到 Phase 1B：

- Required Input 缺失或上游 Gate 已失效；
- 关键分析结论无法转成可执行或可评估规则；
- 三层规则对同一核心结论给出冲突表达；
- Rule Strength 无法从 Evidence Confidence 与视觉角色中确定；
- 规则依赖 Reference Analysis 未提供的视觉事实；
- 发现影响规则系统的上游分析错误。

### Next Phase

`Phase 3A — Build Skill v1`

## 8. Phase 3A — Build Skill v1

### Phase Name

`Phase 3A — Build Skill v1`

### Purpose

把完整 Visual System 压缩编译成目标 Image Skill 的可执行 v1 Candidate。

### Required Input

- Target Skill Brief；
- 已通过 Phase 1B Exit Gate 的 Reference Analysis Artifact；
- 已通过 Phase 2 Exit Gate 的 Visual Rules Artifact；
- 已通过 Phase 2 Exit Gate 的 Prompt Rules Artifact；
- 已通过 Phase 2 Exit Gate 的 Quality Rules Artifact；
- 如果未来已存在正式 Traceability Artifact，则将其作为条件性 Required Input。

### Responsibility

本 Phase 唯一主要负责回答：

> 如何把上游完整系统压缩成运行时可执行的 `SKILL.md`？

职责包括：

- 保留核心视觉身份与 Invariants；
- 保留必要的 Allowed Variation 与 Anti-pattern Guardrails；
- 编译 Prompt Construction Logic；
- 编译最小但可执行的 Quality / Self-check Logic；
- 删除分析过程、证据说明和重复知识；
- 保持目标职责边界。

本 Phase 的检查是编译者自检，不产生独立 Audit Verdict，也不能替代 Phase 3B。

### Required Output

正式 **Target `SKILL.md` v1 Candidate**。

该 Candidate 是待审计执行层，不是 Frozen Skill。

### Allowed Mutation

- 创建或更新当前目标 Skill 的 `SKILL.md` v1 Candidate；
- 在本 Phase 内为满足编译自检而压缩、重排或修正 Candidate；
- 更新 Build State Record 中仅与 Phase 3A 相关的状态与 Block 原因。

### Forbidden Mutation

- 修改 References、Reference Audit 或 Reference Analysis；
- 无证据修改 Visual System Artifacts；
- 为缩短文件而删除关键 Invariant；
- 把 Allowed Variation 锁成固定模板；
- 把 System 文件机械拼接为 `SKILL.md`；
- 添加 Usage Contract、路由或其他 Scope Leakage；
- 创建正式 Skill Audit Verdict；
- 开始真实生成测试或 Freeze。

### Exit Gate

只有同时满足以下条件，Gate 才通过：

- `SKILL.md` v1 Candidate 已存在且可执行；
- Core Visual Identity 与核心 Invariants 均有运行时表达；
- Allowed Variation 未被明显写死；
- Prompt Construction Logic 存在且不是纯风格形容词；
- Quality / Self-check Logic 存在；
- 主要 Anti-pattern Guardrails 存在；
- Candidate 明显比完整 System 更紧凑，没有大段复制上游；
- 不存在明显 Scope Leakage；
- 未执行任何 Forbidden Mutation。

本 Gate 只确认 Candidate 已达到“可审计”状态，不确认其编译正确性。

### Blocked / Failure Condition

以下任一情况出现时，Build 必须停留在 Phase 3A 或回退到 Phase 2：

- Required Input 缺失或 Phase 2 Gate 已失效；
- 核心规则无法在不失真的情况下压缩；
- Candidate 缺少必要执行逻辑；
- Candidate 只能通过新增 unsupported rule 才能显得完整；
- 上游三层规则存在阻止编译的冲突；
- Candidate 出现明显职责漂移或固定模板化。

### Next Phase

`Phase 3B — Skill Consistency Audit`

## 9. Phase 3B — Skill Consistency Audit

### Phase Name

`Phase 3B — Skill Consistency Audit`

### Purpose

独立检查当前 `SKILL.md` 是否忠实、充分且紧凑地编译了上游视觉系统。

### Required Input

- Target Skill Brief；
- 完整 Reference Set；
- 已通过 Phase 1A Exit Gate 的 Reference Set Audit Artifact；
- 已通过 Phase 1B Exit Gate 的 Reference Analysis Artifact；
- 已通过 Phase 2 Exit Gate 的 Visual Rules Artifact；
- 已通过 Phase 2 Exit Gate 的 Prompt Rules Artifact；
- 已通过 Phase 2 Exit Gate 的 Quality Rules Artifact；
- 已通过 Phase 3A Exit Gate 的 Target `SKILL.md` v1 Candidate；
- 如果未来已存在正式 Traceability Artifact，则必须纳入 Audit。

### Responsibility

本 Phase 唯一主要负责回答：

> `SKILL.md` 的编译是否发生了失真？

独立审计至少检查：

- `Missing`；
- `Distorted`；
- `Unsupported`；
- `Redundant`。

并识别 Dropped Invariant、Strength Distortion、Scope Leakage、Overengineering 与 Under-specification。Traceability 建立后，Audit 还应检查 Untraced Rule，但本阶段不定义 ID 或完整 Rubric。

### Required Output

正式 **Skill Audit Artifact**，至少包含：

- Audit scope；
- issue classification 与 severity；
- Required Corrections；
- 修订后的复核结果；
- Verdict：`PASS / PASS WITH ISSUES / FAIL`；
- 是否允许进入 Phase 4 的明确结论。

### Allowed Mutation

- 创建或更新 Skill Audit Artifact；
- 对 Target `SKILL.md` Candidate 进行有上游证据支持的最小修正；
- 对修正后的 Candidate 重新执行一致性检查；
- 更新 Build State Record 中仅与 Phase 3B 相关的状态、Verdict 与 Block 原因。

Phase 3B 对 `SKILL.md` 的修正是经合同明确授予的纠错权限，不改变 Phase 3A 对 Candidate 的主要 Ownership。

### Forbidden Mutation

- 修改 Reference Set；
- 为使 Candidate 通过而随意修改 Reference Audit、Reference Analysis 或 Visual System；
- 重新设计目标视觉身份；
- 添加无上游支持的新规则；
- 用删除合法 Variation 的方式消除 Audit Issue；
- 在 Audit Gate 通过前开始正式生成测试；
- Freeze Skill。

发现明确上游问题时，应记录证据并按 Rollback Principle 回到其 Owner Phase，不得在 Phase 3B 内静默修复上游 Artifact。

### Exit Gate

只有同时满足以下条件，Gate 才通过：

- Skill Audit Artifact 已完成；
- Verdict 为 `PASS`，或为仅含 Minor 问题的 `PASS WITH ISSUES`；
- `Critical = 0`；
- `Major = 0`；
- 所有必需修正已经完成并重新审计；
- Candidate 不存在已知 unsupported rule、关键遗漏或 Scope Leakage；
- Candidate 仍是紧凑、可执行的 execution layer；
- 未执行任何 Forbidden Mutation。

该 Gate 是进入真实生成测试的强制正式 Gate，不得由 Phase 3A 自检或人工口头确认替代。

### Blocked / Failure Condition

以下任一情况出现时，Build 必须停留在 Phase 3B 或回退到最近责任 Phase：

- Required Input 缺失或任一上游 Gate 已失效；
- Verdict 为 `FAIL`；
- 存在未解决 Critical 或 Major Issue；
- 必需修正后仍出现同一编译失真；
- Issue 根因位于 Reference Analysis 或 Visual System，而非 Candidate；
- Audit 无法在不扩大范围或发明规则的情况下通过。

### Next Phase

`Phase 4 — Test + Refine + Freeze`

## 10. Phase 4 — Test + Refine + Freeze

### Phase Name

`Phase 4 — Test + Refine + Freeze`

### Purpose

通过真实生成证据验证目标 Skill 是否能在核心输入与合法变化下稳定保持同一 Visual Family，并在受控修订与回归后决定是否 Freeze。

### Required Input

- 完整 Reference Set；
- 已通过 Gate 的 Reference Set Audit Artifact；
- 已通过 Gate 的 Reference Analysis Artifact，包括 Reference-derived Invariants、Allowed Variations 与 Anti-patterns；
- 已通过 Gate 的 Visual Rules Artifact；
- 已通过 Gate 的 Prompt Rules Artifact；
- 已通过 Gate 的 Quality Rules Artifact；
- 已通过 Phase 3B Exit Gate 的 Audited `SKILL.md` Candidate；
- Skill Audit Artifact 及其 `PASS` 或合格的 `PASS WITH ISSUES` Verdict；
- 如果未来已存在正式 Traceability Artifact，则 Test Cases 必须连接相关上游规则。

### Responsibility

本 Phase 唯一主要负责回答：

> 当前 Skill 在真实生成环境中是否稳定成立，是否满足 Freeze 条件？

职责是完整执行：

```text
Test
→ Diagnose
→ Minimal Fix
→ Retest
→ Regression
→ Freeze Decision
```

测试必须覆盖 `Core / Variation / Stress / Boundary` 四类行为，并区分 Prompt Failure、Skill Failure、System Rule Failure、Model Variance 与输入特定难度。测试评价 Visual Family 一致性，不要求逐图复制，也不以“是否漂亮”为通过标准。

### Required Output

正式 Phase 4 Artifacts，至少表达：

- Test Cases；
- Expected Behavior；
- Test Results；
- Failure Diagnosis；
- Refinement History；
- Retest Results；
- Regression Results；
- Remaining Known Limitations；
- Final Test Report；
- Freeze Status：`FREEZE / FREEZE WITH KNOWN LIMITATIONS / NOT READY`，或后续 Test Protocol 定义的等价状态。

本合同不规定这些 Artifact 的具体文件拆分或 Schema。

### Allowed Mutation

- 创建或更新 Phase 4 所拥有的 Test、Diagnosis、Refinement、Regression 与 Freeze Artifacts；
- 基于真实 Test Evidence 对当前 `SKILL.md` Candidate 做最小、受控且有记录的修订；
- 更新 Build State Record 中与 Phase 4、Retest、Regression 和 Freeze 相关的状态；
- 当证据证明根因位于上游时，发起 Minimal Upstream Rollback。

任何 Phase 4 对 `SKILL.md` 的修订都会使原 Phase 3B Gate 失效，必须回到 Phase 3B 重新审计后才能恢复正式 Test。若修改超出局部执行措辞或涉及编译结构，应先回到 Phase 3A。Prompt、Visual 或 Quality Rules 的修订必须回到 Phase 2，由 Owner Phase 执行，不能在 Phase 4 中静默改写。

### Forbidden Mutation

- 修改、替换或重排 Reference Set 以提高通过率；
- 无证据修改 Core Visual Identity 或其他上游结论；
- 用手工超强 Prompt 绕过 `SKILL.md`；
- 无限生成直到偶然成功；
- 把单次 Model Variance 直接视为系统性失败；
- 把系统性失败归咎于随机性；
- 为消除失败而禁止全部合法 Variation；
- 降低 Expected Behavior、Rubric 或测试难度以制造通过；
- 在相关修订未重新审计、Retest 或 Regression 前 Freeze；
- Freeze 仍存在重复 Critical Failure 或未记录限制的 Skill。

### Exit Gate

Phase 4 Exit Gate 同时是 Freeze Gate。只有同时满足以下条件，才允许进入 `Frozen`：

- Core Cases 稳定通过，或只有不影响核心身份的 Minor Issue；
- Variation Cases 未显示明显 Template Lock 或系统性 Style Drift；
- Stress Cases 没有重复 Critical Failure Pattern；
- Boundary Cases 的失败可控且未证明核心系统失效；
- 失败已按根因分类，系统性问题未被当作随机性忽略；
- 每项正式 Refinement 都有 Test Evidence、Root Cause 与最小修订记录；
- 相关修订已完成 Retest；
- 所有受影响的核心与合法 Variation 已完成 Regression；
- 任何被修订的上游 Gate 与 Static Audit Gate 均已重新通过；
- Remaining Known Limitations 已明确记录；
- Final Test Report 与 Freeze Status 已完成；
- 未执行任何 Forbidden Mutation。

### Blocked / Failure Condition

以下任一情况出现时，Build 必须停留在 Phase 4、继续受控修订，或回退到最近责任 Phase：

- Required Input 缺失或 Phase 3B Gate 无效；
- 无法执行真实生成或无法保存足够测试证据；
- 出现重复 Critical Failure Pattern；
- 核心 Cases 不稳定；
- 修复一个问题持续破坏合法 Variation；
- Root Cause 位于上游但尚未完成 Rollback；
- Retest 或 Regression 未通过；
- Remaining Limitation 会破坏核心职责；
- Freeze Status 为 `NOT READY`。

Build 不得通过无限迭代追求 100% 单次成功率；当失败主要属于可记录的模型随机性且不构成系统性模式时，可以依后续 Test Protocol 判断是否 `FREEZE WITH KNOWN LIMITATIONS`。

### Next Phase

`Frozen`

## 11. Phase Ownership

Owner Phase 负责首次创建其 Artifact，并对其 Gate 正确性负责。其他 Phase 只能在本合同明确授权时修改；否则必须回到 Owner Phase。

| Artifact | Owner | Other-phase mutation rule |
|---|---|---|
| Accepted Build Input / Target Skill Brief | Build Initialization | 后续只读；实质变更视为新输入并使相关下游 Gate 失效 |
| Reference Set | External input / protected evidence | Builder Phase 不得修改；补充或替换需外部授权并回到 Phase 1A |
| Reference Set Audit Artifact | Phase 1A | 发现事实错误时回到 Phase 1A |
| Reference Analysis Artifact | Phase 1B | 发现事实错误或关键缺口时回到 Phase 1B |
| Visual Rules Artifact | Phase 2 | 测试或审计发现根因后回到 Phase 2 |
| Prompt Rules Artifact | Phase 2 | 测试或审计发现根因后回到 Phase 2 |
| Quality Rules Artifact | Phase 2 | 测试或审计发现根因后回到 Phase 2 |
| Target `SKILL.md` v1 Candidate | Phase 3A | Phase 3B 可做审计修正；Phase 4 可做测试证据支持的局部修正，随后必须重过 Audit Gate |
| Skill Audit Artifact | Phase 3B | 任何 Candidate 修订后由 Phase 3B 更新或重建 |
| Test / Diagnosis / Refinement / Regression Artifacts | Phase 4 | 仅 Phase 4 在当前 Build 中维护 |
| Final Test Report / Freeze Status | Phase 4 | Freeze 后不得静默修改 |

Ownership 不是禁止纠错，而是确保纠错发生在正确责任层，并使受影响的下游 Gate 可被重新验证。

## 12. Exit Gate Rules

每个 Phase 的 Exit Gate 除本 Phase 专属条件外，还必须满足四项全局条件：

1. **Artifact existence**：Required Output 已存在且可读取；
2. **Responsibility coverage**：本 Phase 的核心问题已被回答，关键不确定性已解决或明确记录；
3. **Mutation compliance**：没有未撤销的 Forbidden Mutation 或 Phase Leakage；
4. **State validity**：Gate 结果、Block 原因与 Next Phase 已被记录。

Gate 结果只有两种推进意义：

- **Pass**：允许进入唯一正常 Next Phase；
- **Not Passed**：保持当前 Phase，或按证据执行最小回退。

状态标签可以在后续协议中细化，但不得改变这一推进语义。

特别规定：

- Phase 1A 的 `NOT READY` 不能进入 Phase 1B；
- Phase 3B 的 `FAIL` 或任何未解决 Critical / Major Issue 不能进入 Phase 4；
- Phase 4 的 Retest 或 Regression 未完成不能进入 Frozen。

## 13. Rollback Principle

State Machine 允许基于证据纠错，但不允许任意回滚：

```text
Failure Evidence
↓
Root Cause
↓
Closest Responsible Phase
↓
Minimal Correction
↓
Re-run Owner Exit Gate
↓
Resume Forward Pipeline
↓
Retest / Regression where applicable
```

### 13.1 Minimal Upstream Rollback

- Candidate 编译问题：回到 Phase 3A，再经 Phase 3B；
- Static Audit 可在不改变上游的情况下修正 Candidate：停留 Phase 3B，修正并重审；
- Visual、Prompt 或 Quality Rule 问题：回到 Phase 2，再经 3A、3B、4；
- 描述性视觉结论问题：回到 Phase 1B，再经所有下游 Gate；
- Reference 分类、权重或准备度问题：回到 Phase 1A，再经所有下游 Gate；
- Reference Set 本身不足：停留或回到 Phase 1A，等待受授权的证据补充。

不得因 Phase 4 的 Prompt Rule 问题直接回到 Phase 1A，也不得因单次生成失败启动任何上游回退。

### 13.2 Rollback Evidence Requirement

每次回退必须记录：

- 触发 Evidence；
- Root Cause 判断；
- 目标 Owner Phase；
- 计划的最小修订；
- 受影响的下游 Gates；
- 恢复前进后需要执行的 Retest / Regression。

如果 Root Cause 尚不明确，应停留当前 Phase 继续诊断，而不是猜测式回滚。

## 14. Invalid State Transitions

以下转换一律非法：

```text
1A → 2
1A → 3A
1B → 3A
1B → 3B
2 → 3B
2 → 4
3A → 4 without Phase 3B Gate
3B FAIL → 4
3B with Critical or Major issues → 4
4 with failed Retest → Frozen
4 without Regression → Frozen
Any Phase → Frozen except a passed Phase 4 Freeze Gate
```

下列行为同样构成非法状态转换或 Phase Leakage：

- Required Input 不完整时启动 Phase；
- Exit Gate 未明确通过就创建下一 Phase 的正式 Artifact；
- 使用历史产物假定当前 Build 已通过某个 Gate；
- 在当前 Phase 静默修改另一个 Owner Phase 的 Artifact；
- 以条件性 Verdict 掩盖阻断性 Issue；
- Freeze 后继续无证据修改正式 Skill 或 System Artifacts。

Rollback 不属于非法跳跃，但必须满足第 13 节的 Evidence、Root Cause、Closest Responsible Phase 与 Gate Revalidation 要求。

## 15. Final State — Frozen

`Frozen` 表示目标 Image Skill 已完成当前版本的证据分析、规则规格、编译、独立审计、真实测试与回归验证。

进入 Frozen 必须具备：

- Phase 1A–3B 的有效 Gate 链；
- Phase 4 已通过 Freeze Gate；
- 最终 `SKILL.md` 与其依赖的 System Artifacts 是实际经过测试的版本；
- Remaining Known Limitations 已记录；
- Freeze Status 与 Final Test Report 一致。

Frozen 是当前版本的受控基线，不代表永远不可改。新 Evidence、已证实 Regression 或明确需求变更可以触发新修订，但必须：

1. 记录解冻原因；
2. 定位最近责任 Phase；
3. 从该 Phase 重新通过全部受影响的下游 Gates；
4. 重新完成必要的 Audit、Retest 与 Regression；
5. 形成新的 Freeze 决定。

禁止对 Frozen Skill 进行未记录、未测试的审美重写。

## 16. Contract Boundary

本 Phase Contract 不负责：

- 定义完整 Adaptive Reference Analysis Framework；
- 创建 `REF / OBS / INV / VAR / ANTI` 等 Traceability ID；
- 定义 Visual Rule、Prompt Rule 或 Quality Rule Schema；
- 定义完整 Audit Rubric；
- 定义具体 Test Cases、评分系统或生成次数；
- 设计 Build Manifest、YAML Schema 或全部文件模板；
- 创建目标 `SKILL.md`；
- 执行真实测试或 Historical Backtest；
- 修改任何历史 Reference Implementation。

这些工作只能由后续明确授权的阶段完成。
