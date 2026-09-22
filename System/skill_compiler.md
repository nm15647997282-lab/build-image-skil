# build-image-skill — Skill Compiler

## 1. Purpose

本文件定义 `Phase 3A — Build Skill v1` 的通用编译方法。

Skill Compiler 将已经通过 Phase 2 Gate 的完整 Visual System 压缩为目标 Image Skill 的运行时执行层：

```text
Reference Analysis
+
Visual Rules
+
Prompt Rules
+
Quality Rules
+
Traceability
+
Target Skill Purpose / Scope
↓
Target SKILL.md v1 Candidate
```

本 Compiler 只定义如何构建目标 `SKILL.md`。它不为任何目标 Skill 预设视觉答案，不执行独立 Static Audit，不创建测试，也不 Freeze Skill。

## 2. Compilation Admission Gate

正式编译开始前必须同时满足：

- Target Skill Brief 中的 `skill_name`、`purpose` 与 `scope_boundary` 已被接受；
- Reference Analysis 已通过 Phase 1B Gate；
- `visual_rules.md`、`prompt_rules.md`、`quality_rules.md` 均存在并通过 Phase 2 Gate；
- Phase 2 Verdict 明确为 `READY FOR SKILL COMPILATION`；
- 当前 Build 的 Traceability 已实例化，active VR、PR、QR 的来源、强度、状态与位置可读取；
- Phase 2 之后没有未处理的上游实质修订；
- 不存在阻断性的三层冲突、Dropped INV、Variation Collapse、Orphan QR、Untraced Rule 或 Strength Distortion。

任何一项不满足时，不得通过猜测、补写或跳过链接来生成正式 Candidate。Build 必须停留在 Phase 2，或按 `phase_contracts.md` 回到最近的责任 Phase。

## 3. Compiler Inputs

Phase 3A 必须读取：

1. Target Skill Purpose / Scope；
2. 已通过 Gate 的 Reference Analysis；
3. Visual Rules；
4. Prompt Rules；
5. Quality Rules；
6. 当前 Build 的 Traceability。

必要时可以回查 Reference Set Audit 与原始 References，以确认关键结论是否被错误解释；但正常编译不得重新进行 Reference Analysis，也不得用编译者偏好推翻已通过 Gate 的上游含义。

当前 V2 System 与当前 Build 的正式 Artifacts 是主要 Source of Truth。历史实现只能帮助理解已验证的编译机制，不能替代当前证据链。

## 4. Compiler Output

正式输出是：

```text
Target Image Skill / SKILL.md
status: v1 candidate
```

同时更新当前 Build 的 Traceability，创建或更新 SK Entity 与双向链接。

Candidate 必须：

- 是可被运行时调用的执行协议；
- 保留完成目标生成任务所需的视觉、Prompt、检查与修订逻辑；
- 明显比完整 Analysis / System 更紧凑；
- 保持目标 Skill 的 purpose 与 scope boundary；
- 通过 Phase 3A 编译自检，达到“可审计”状态。

Candidate 不是 `Frozen`，也不能被描述为已经通过真实生成验证。只有后续 Phase 3B Static Audit 与 Phase 4 Test / Regression 全部通过后，才可能 Freeze。

## 5. SKILL.md as the Execution Layer

正式确立：

> `SKILL.md = compressed execution layer`

它不是以下文件的机械拼接：

```text
reference_analysis.md
+ visual_rules.md
+ prompt_rules.md
+ quality_rules.md
+ traceability data
```

`SKILL.md` 应保留模型在执行当前任务时必须知道的：

- 目标与职责边界；
- Core Visual Identity 的可执行表达；
- 核心 Invariants 与视觉优先级；
- 与当前 Visual System 相关的 subject / object construction、composition 或其他生成机制；
- 已被证据晋升且与运行有关的 Adaptive Dimensions；
- Allowed Variation 与其稳定核心、边界；
- Prompt Construction Logic 与必要的语言指导；
- 高风险 Anti-pattern Guardrails；
- 轻量 Generation Check、Quality Check 与 Revision Guidance；
- 最终执行原则。

这些是能力模块，不是强制章节清单。Compiler 必须根据目标 Visual System 合并、拆分、重命名或省略不适用模块；不得要求所有 Image Skill 使用完全相同的章节、顺序或视觉维度。

以下内容默认留在上游：

- 完整 Reference Audit 与 Reference Analysis；
- 大量 Evidence Explanation 与 Supporting Observation；
- 全量 Traceability Metadata；
- 完整 Quality Rubric；
- 历史分析、测试或修订记录；
- 低价值 Incidental Detail；
- 重复 Rule、长篇视觉理论与完整 Prompt Library。

只有当其中某项通过 Runtime Relevance Test，且压缩后仍是必要执行信息时，才可把其语义带入 Candidate；不得直接复制大段上游正文。

## 6. Runtime Relevance Test

每个候选内容进入 `SKILL.md` 前必须回答：

1. 运行时生成是否需要它？
2. 缺少它是否容易造成 Core Identity 丢失或 Style Drift？
3. 它是否帮助构建实际 Prompt？
4. 它是否帮助运行时自检或修复明显失败？
5. 它是否定义或保护合法 Variation？
6. 它是否保护关键 Scope Boundary？
7. 它是否只是背景解释、证据历史或重复元数据？

Admission 决策为：

- **KEEP**：有独立运行价值，保留为 Skill Rule 或关键执行内容；
- **MERGE**：与其他内容共同形成一个不失真的 Skill Rule；
- **REFERENCE INDIRECTLY**：运行时只需简洁结论，详细依据留在上游；
- **OMIT WITH REASON**：运行时不需要，且省略不会损害身份、变化、强度、边界或可执行性；
- **RETURN UPSTREAM**：候选内容暴露上游冲突或证据缺口，不能安全编译。

若第 7 项是主要性质，通常不进入 Candidate。若前六项中的任一项关系到 identity-critical 信息、重要 Variation、关键 Guardrail 或 Scope，则不能仅以“文件更短”为由省略。

## 7. Purpose and Scope Preservation

Compiler 必须把 Target Skill Brief 中的 `purpose` 与 `scope_boundary` 转换为简洁的运行时边界，同时保持 Reference-first：

- Purpose 说明目标 Skill 负责生成什么，不代替视觉规则；
- Scope Boundary 只限制已正式定义的职责，不被扩写成新的视觉风格；
- optional context 不得无证据升级为执行规则；
- Candidate 不得新增 routing、semantic trigger、video timing、animation、usage decision、外部系统行为或其他未获 Input Contract 授权的职责；
- 上游没有形成合法视觉链的 Brief 文字，不得绕过 Traceability 成为视觉禁令。

任何新增职责、媒介或输出行为都属于 Scope Leakage。无法在既有 purpose / scope 内表达的要求，应停止编译并要求回到相应上游，而不是在 Candidate 中静默扩展。

## 8. Core Visual Identity and Invariant Preservation

所有 active core INV 必须在 Candidate 中获得有效运行时覆盖。覆盖可以是一条独立 SK，也可以与其他不可分割机制安全合并，但必须：

- 保留 INV 的核心含义、适用 Context 与身份后果；
- 保留对应 VR 的实际 Rule Strength；
- 保留从 SK 回到 VR / PR / QR，再回到 INV / OBS / REF 的路径；
- 能被 Prompt Construction 实现，并能由轻量 Quality Check 识别明显偏离；
- 不被抽象口号或风格标签替代。

identity-critical、high-confidence 的 INV 是最高压缩保护对象。若其无法在不失真的情况下进入 Candidate，Phase 3A 不得通过。

以下均属于 Dropped Invariant：

- INV 完全未进入 Skill；
- 只保留了名称或形容词，没有执行含义；
- 强规则被弱化为可选建议；
- INV 被合并后适用范围或关键后果消失；
- Skill 中存在文字，但 Prompt / Check 无法实际使用它。

## 9. Allowed Variation Preservation

对每个 active core / important VAR，Compiler 必须保留：

- 可以变化的 Dimension、状态或相对范围；
- Reference-supported 的合法选择；
- 变化时必须保持的核心；
- 接近或越过边界时的漂移风险；
- VAR → VR → SK Traceability。

VAR 可以进入独立 SK，也可以成为某个 MUST / SHOULD 的明确例外、范围或选择结构。不能因为默认表现更常见，就删除其他合法表现。

以下属于 Variation Collapse / Distortion：

```text
MAY → MUST
A or B are supported → Always use A
Reference-supported range → one fixed value
contextual option → exception treated as failure
```

稳定 Skill 不等于固定模板。Candidate 的 Prompt Construction 必须能够按输入与 Context 选择合法变化，Quality Check 必须能区分合法 Variation 与真实 Style Drift。

## 10. Anti-pattern Guardrail Preservation

active core / important ANTI 应以简洁、上下文明确的 Guardrail 进入 Candidate。优先保留：

- 会破坏 Core Visual Identity 的方向；
- 会造成高风险或重复 Style Drift 的方向；
- 会越过 Scope Boundary 的方向；
- 会反复导致重要生成或质量失败的、已有证据的方向。

Guardrail 必须说明要避免的可见方向、冲突对象与适用 Context。不得：

- 把全部 ANTI 元数据复制成巨大禁止清单；
- 把 soft risk 自动升级为绝对禁令；
- 用过度禁止消除合法 VAR；
- 从历史领域案例或通用审美中新增 ANTI；
- 只写无可执行含义的 `avoid bad style` 类语句。

较低风险、重复或只对上游解释有用的 ANTI 可以不逐条展开，但重要保护能力不得消失。

## 11. Rule Strength and Priority Preservation

Candidate 必须保持正式强度：

```text
MUST / SHOULD / MAY / AVOID / DO NOT
```

禁止无新 Evidence 的转换：

```text
MAY → SHOULD or MUST
SHOULD → MUST
AVOID → DO NOT
MUST → optional guidance
DO NOT → soft suggestion
```

自然语言不必机械重复英文枚举，但其实际约束力必须等价且可审计。合并多个不同强度的 Rule 时，应保留各自条件与作用，不能用其中最强或最弱的措辞覆盖全部来源。

Strength 与 Priority 必须保持分离：

- Strength 表示约束性质；
- Priority 表示冲突、压缩和执行时的关注顺序。

高优先级 VAR 仍然是 MAY；低优先级细节也不能因位置靠后而被无声降级。

## 12. Traceability Preservation

Phase 3A 创建核心 Skill Rule 时，必须同步更新当前 Build 的 Traceability：

```text
VR / PR / QR
↓
SK
```

每个 active SK 至少需要：

- 稳定 `SK-*` ID；
- 简短 statement；
- 一个或多个 active `source_rules`；
- 实际 `rule_strength`；
- `status` 与 `location`；
- 上游 VR / PR / QR 的 `downstream.skill_rules` 反向链接。

每条 SK 必须能继续沿链回溯到 active INV / VAR / ANTI、OBS 与 REF。一个 SK 可连接多个上游；一个上游也可被多个 SK 使用。

Candidate 正文不必充满 ID。ID 可以只出现在稳定条目、轻量索引或 Traceability 中，只要 `location` 能明确指向对应 Skill Rule。

创建、合并、拆分、弃用或修改 SK 时，遵守 `traceability_spec.md`：稳定 ID 不重编号，deprecated / rejected ID 不复用，实质变化追加 Revision Record，所有双向链接保持一致。本阶段不得重设计 YAML Schema。

## 13. Safe Rule Merge

多个 VR / PR / QR 可以共同编译为一个 SK，前提是：

- 它们服务同一运行时动作或不可分割机制；
- Scope 与 Context 兼容；
- 没有语义冲突；
- 不丢失任何来源的 Rule Strength、例外或边界；
- 不消除合法 Variation；
- 合并后仍可构建 Prompt、进行自检并独立修订；
- `source_rules` 保留全部来源 ID。

不应合并的情况包括：

- Evidence、Context、Strength 或 Variation Boundary 不同；
- 规则具有不同的失败后果或修复方向；
- 合并后只能写成抽象口号；
- 合并会让某个 INV、VAR、ANTI 或 QR 失去可见覆盖。

Merge 的目标是减少运行时重复，不是减少 ID 数量。

## 14. Justified Rule Omission

并非每条 VR / PR / QR 都要逐字进入 Candidate。以下内容可以省略：

- 上游 Evidence Detail 与分析解释；
- 被另一 SK 完整覆盖的同义 Rule；
- 运行时不需要的 Supporting Detail；
- 低价值重复内容；
- 只属于完整 Rubric、但不影响运行时自检的细节。

省略必须同时满足：

1. 不涉及未覆盖的 core INV、important VAR 或 important ANTI；
2. 不改变 Rule Strength、Context、Scope 或 Quality-critical behavior；
3. 不造成 Prompt Rule 或 Quality Rule 的核心能力缺失；
4. 若由另一 SK 覆盖，该 SK 的 `source_rules` 包含被覆盖来源；
5. 若确实不进入任何 SK，在现有上游 Entity `notes` 或当前编译记录中保留简短、可审计理由，不增加新 Schema。

“为了更短”“看起来重复”“模型应该知道”都不是充分理由。Identity-critical 信息不得省略。

## 15. Prompt Construction Preservation

Candidate 必须说明如何从当前输入与适用规则构建实际生成描述，而不能只保留风格定义或一条固定 production prompt。

最小能力包括：

1. 确认当前任务的 primary visual object 与 scope；
2. 选择与当前 Context 相关的 active Skill Rules；
3. 按 Priority、Strength 与依赖关系组织描述；
4. 用具体可见的对象、状态、关系与视觉机制表达规则；
5. 明确本次合法 Variation 的选择及其稳定核心；
6. 只加入相关 Guardrails；
7. 删除冲突、重复和无法回溯的语言；
8. 在生成前运行轻量检查。

具体顺序、模块与词汇必须适应目标 Visual System。Compiler 不保存每个 subject 的完整 production prompt，不把历史 Skill 的措辞或结构设为 Universal Template，也不让抽象风格词取代具体视觉描述。

## 16. Generation and Quality Self-check

Candidate 应保留轻量、可执行的两段检查能力，而不是复制完整 Quality Rubric。

### 16.1 Generation Check

生成前至少确认：

- Purpose / Scope 与输入一致；
- Core INV 已表达；
- 当前 VAR 选择合法且未被写死；
- 适用的 Prompt Rules 已实现；
- 高风险 ANTI Guardrail 已加入；
- Prompt 内没有相互冲突、无来源或重复表达。

### 16.2 Quality Check

生成后至少确认：

- Core Visual Identity 与核心 INV 是否成立；
- 当前差异是否属于合法 VAR；
- 是否出现重要 ANTI contamination 或 scope violation；
- 是否触发上游定义的 Hard Failure；
- 偏差应 `PASS`、`REVISE` 还是 `FAIL`；
- 若需修订，最接近的可执行原因是什么。

Skill 中的检查只服务运行时明显判断。完整判据、细粒度 Rubric 与后续 Test 仍留在 `quality_rules.md` 和 Phase 4 Artifacts。

## 17. Revision Guidance

Candidate 可以保留少量高价值：

```text
Failure
→ Likely Cause
→ Fix Direction
```

只有同时满足以下条件才进入：

- Failure 高频、重要或会显著改变 Visual Family / Scope；
- Cause 能回溯到现有 SK / PR / QR，而不是猜测模型内部原因；
- Fix Direction 具体、局部且不引入 unsupported rule；
- 修复不会通过删除合法 Variation 获得表面稳定；
- 指导比重新读取完整 System 更适合运行时使用。

不得预写大量假设性 Failure，不得把 Phase 4 的 Test / Diagnosis / Regression 流程提前塞入 Skill，也不得宣称未经测试的修复已验证有效。

## 18. Overcompression Protection

以下 Candidate 属于 Under-specification：

```text
Follow the references.
Make it cinematic.
Keep it realistic.
Use good composition.
```

即使文件很短，只要缺少以下任一关键能力，就不能通过 Phase 3A：

- 可执行的 Core Visual Logic；
- 核心 INV 覆盖；
- Allowed Variation 与边界；
- Prompt Construction；
- 必要 Guardrails；
- Generation / Quality Check；
- 高价值失败修订方向，若上游表明其为运行时必要。

压缩是有损的，但损失只能发生在背景解释、重复与低运行价值细节，不能发生在决定执行正确性的语义上。

## 19. Overengineering Protection

Candidate 不得重新膨胀为：

- 视觉百科或研究报告；
- 规则数据库或 Traceability dump；
- 大量重复章节；
- 巨型 Vocabulary List；
- 完整评分系统；
- Evidence 引用集合；
- 全量测试、修订或历史记录；
- 对运行无帮助的 metadata 与抽象层。

每个模块必须通过 Runtime Relevance Test。若两个模块始终一起执行、一起检查且没有独立修订价值，应合并；若某段只能解释“为什么发现了规则”，而不能改变运行时决策，应留在上游。

目标是：

> concise but operationally complete

## 20. Compilation Procedure

Phase 3A 按以下顺序执行：

1. **Validate admission**：确认 Phase 2 为 `READY FOR SKILL COMPILATION`；
2. **Lock purpose and scope**：读取 Brief，建立不可静默扩展的运行边界；
3. **Build coverage inventory**：列出 active core / important INV、VAR、ANTI 与 VR / PR / QR；
4. **Apply Runtime Relevance Test**：对候选内容执行 KEEP / MERGE / REFERENCE INDIRECTLY / OMIT / RETURN UPSTREAM；
5. **Design adaptive execution modules**：按当前 Visual System 组织 Candidate，不套固定章节；
6. **Compile core behavior**：先保护 Core Identity、INV 与 Scope；
7. **Compile variation and guardrails**：保留 VAR 选择结构与关键 ANTI；
8. **Compile Prompt Construction**：保留从输入到实际描述的构建能力；
9. **Compile lightweight checks and guidance**：加入必要 Generation / Quality Check 与高价值 Revision Guidance；
10. **Create SK Traceability**：分配稳定 SK ID，连接 VR / PR / QR 并同步反向链接；
11. **Compress and deduplicate**：安全合并、记录合理省略，移除重复解释；
12. **Run Phase 3A self-check**：检查覆盖、强度、变化、边界、可执行性与紧凑性。

该流程产生编译者自检，不得输出 Phase 3B Verdict，也不能替代独立 Static Audit。

## 21. Phase 3A Self-check and Exit

Phase 3A 只有同时满足以下条件才可将 Candidate 交给 Static Audit：

- `SKILL.md` v1 Candidate 存在、可读取且可执行；
- Purpose 与 Scope Boundary 明确且没有新增职责；
- Core Visual Identity 与所有 active core INV 有有效 SK 覆盖；
- active core / important VAR 未消失、未被固定、未被 Guardrail 误伤；
- active core / important ANTI 有适度 Guardrail；
- Rule Strength 与 Context 未失真，Priority 未替代 Strength；
- Prompt Construction 是构建逻辑，而不是固定 Prompt 或抽象词列表；
- Generation Check、Quality Check 与必要 Revision Guidance 足以处理明显运行失败；
- 每个 active SK 有合法 VR / PR / QR 来源，并可回到 INV / VAR / ANTI 与 REF；
- merge 保留全部来源，omission 有合理依据；
- Candidate 没有大段复制 System，没有明显重复或无关复杂度；
- Candidate 没有 Under-specification、Unsupported Rule 或 Scope Leakage；
- Traceability 的 links、location、status 与必要 Revision Record 已同步；
- 未创建 Audit Verdict、TC、Test Artifact 或 Freeze 状态；
- 未执行任何 Phase 3A Forbidden Mutation。

Exit 只表示：

```text
READY FOR STATIC AUDIT
```

若核心规则无法在不失真的情况下压缩、Candidate 只能靠 unsupported 内容补全，或上游冲突阻止编译，则 Phase 3A 不通过，并按最近责任层执行 Minimal Rollback。

## 22. Compiler Boundary

本文件严格属于 Phase 3A。它可以：

- 创建或更新目标 `SKILL.md` v1 Candidate；
- 创建、更新或弃用 SK Entity；
- 安全合并上游规则并记录合理省略；
- 对 Candidate 进行编译自检。

它不得：

- 修改 Reference Set、Reference Audit 或 Reference Analysis；
- 无证据修改 Visual / Prompt / Quality Rules；
- 重新设计 Traceability Schema；
- 执行 Phase 3B 独立审计或签发 Audit Verdict；
- 创建 TC、Test Protocol、Test Results 或 Historical Backtest；
- 运行图片生成、Refinement、Regression；
- Freeze 目标 Skill；
- 修改历史 Reference Implementation。

