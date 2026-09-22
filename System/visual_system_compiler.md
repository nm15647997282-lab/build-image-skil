# build-image-skill — Visual System Compiler

## 1. Purpose

本文件定义 `Phase 2 — Visual System Specification` 的通用编译方法。

Visual System Compiler 将已经通过 Phase 1B Gate 的 Reference Analysis 与 Traceability 结果转换为：

```text
Reference Analysis
+
Traceability
↓
Visual Rules
+
Prompt Rules
+
Quality Rules
```

三层共同构成目标 Image Skill 的可执行、可测试、可审计 Visual System。本 Compiler 只定义如何生成这三层，不为 `build-image-skill` 预设任何具体视觉风格，也不编译最终 `SKILL.md`。

## 2. Compiler Inputs

正式编译开始前必须具备：

- Target Skill Brief，用于确认 purpose 与 scope boundary；
- 已通过 Phase 1A Gate 的 Reference Set Audit；
- 已通过 Phase 1B Gate、Verdict 为 `READY FOR VISUAL SYSTEM SPECIFICATION` 的 Reference Analysis；
- active INV、VAR、ANTI 及其 OBS / REF Evidence；
- 当前 Build 已实例化的 Traceability；
- `System/build_protocol.md`、`phase_contracts.md`、`analysis_framework.md` 与 `traceability_spec.md`。

输入必须满足：

- 核心分析结论可回溯到有效 REF；
- 关键 INV / VAR / ANTI 没有阻断性 Evidence Gap；
- Brief 的视觉预设未覆盖 Reference Evidence；
- Phase 1B 仍保持有效，没有未处理的上游修订。

Required Input 缺失或 Phase 1B Gate 失效时，不得启动正式编译。

## 3. Compiler Outputs

Phase 2 正常完成后，目标 Image Skill 应产生：

```text
System/
├── visual_rules.md
├── prompt_rules.md
└── quality_rules.md
```

同时更新当前 Build 的 Traceability 实例，创建并连接 VR、PR、QR。

这三个文件属于目标 Image Skill，不是 `build-image-skill` 自身的固定视觉规则。具体章节应根据当前 Reference Analysis 自适应；本 Compiler 只规定三层职责和最低内容，不提供某一领域的成品规则。

## 4. Compiler Pipeline

Visual System Compiler 按以下顺序工作：

```text
1. Validate Phase 2 inputs
2. Select eligible active INV / VAR / ANTI
3. Create candidate rules
4. Run Rule Admission Test
5. Resolve conflicts and overlaps
6. Assign Rule Strength and Priority
7. Compile VR
8. Compile PR and QR from admitted VR
9. Deduplicate and align the three layers
10. Update Traceability links and locations
11. Run Visual System Readiness Gate
```

任何一步发现上游 Evidence、角色或 Confidence 无法支持规则时，应 `DEFER`、`REJECT` 或按 Phase Contracts 回退，而不是补写视觉内容。

## 5. Three-layer Visual System

### 5.1 Layer 1 — Visual Rules

`visual_rules.md` 回答：

> 最终图片在视觉上必须、应该、可以、应避免或不能具备什么？

Visual Rules 定义：

- visual behavior；
- visual constraints；
- visual priorities；
- allowed variation；
- style boundaries；
- anti-pattern protection。

VR 描述视觉结果和边界，不规定 Prompt 的具体措辞，也不定义测试步骤。

### 5.2 Layer 2 — Prompt Rules

`prompt_rules.md` 回答：

> 为实现 Visual Rules，生成 Prompt 应如何组织与表达？

Prompt Rules 可以定义：

- prompt construction logic；
- description priority and order；
- concrete visual wording；
- preferred / conditional / risky / avoid vocabulary；
- variation expression；
- guardrail language。

PR 是 VR 的实现层，不是新的视觉 Source of Truth。任何 PR 都必须连接至少一个 VR，且不得增加上游未定义的视觉要求。

### 5.3 Layer 3 — Quality Rules

`quality_rules.md` 回答：

> 如何判断生成结果是否符合 Visual System？

Quality Rules 定义：

- hard failure conditions；
- core quality checks；
- invariant compliance；
- variation validity；
- anti-pattern contamination；
- visual-family consistency；
- `PASS / REVISE / FAIL` logic。

QR 是 VR 的检测层。它只能检查已有 VR，不能独立增加审美标准或视觉要求。

### 5.4 Layer Alignment

每个 active VR 应至少具有：

- 一个能够实现它的 active PR；
- 一个能够检查它的 active QR。

如果一个正式 VR 无法被 Prompt 表达或无法被 Quality Rule 判断，它尚未达到可执行 Visual System 的标准，应被改写、拆分、合并或退回上游，而不是留作抽象口号。

### 5.5 Formal Traceability Requirement

每条正式 Rule 必须满足：

- VR 通过 `source_roles` 连接至少一个 active INV、VAR 或 ANTI；
- PR 通过 `source_visual_rules` 连接至少一个 active VR；
- QR 通过 `source_visual_rules` 连接至少一个 active VR；
- 所有关系同步写入上游 Entity 的 downstream；
- 每条链都能够继续回溯至 OBS 与 REF Evidence；
- 多对多关系合法，不要求一个上游只产生一个 Rule；
- 不存在 VR without source、PR without VR 或 QR without VR。

Traceability 不完整的候选 Rule 不能 ADMIT，也不能通过 Phase 2 Gate。

## 6. Formal Rule Strength

正式强度枚举固定为：

```text
MUST
SHOULD
MAY
AVOID
DO NOT
```

### 6.1 MUST

表示：如果该视觉条件明显缺失、反转或被替换，目标 Visual Family 会产生重大失真。

通常要求：

- 来源主要是 active、`core`、high-confidence INV；
- 得到高权重 References 的跨图支持；
- identity impact 明确；
- 与合法 VAR 不冲突；
- 重要反证已解决或被限定在不同 Context。

Single-instance、低 Confidence 或单纯高 Frequency 不能直接产生 MUST。

### 6.2 SHOULD

表示：默认应遵守，并对视觉稳定性有明显帮助，但在 Reference-supported Variation、Subtype 或明确 Context 中可以调整。

通常来自：

- active INV，但其适用范围存在合法例外；
- 重要且证据充分的稳定视觉机制；
- INV 与 VAR 共同定义的默认倾向。

SHOULD 必须说明何时可以偏离，不能把未写明例外的 SHOULD 当作隐性 MUST。

### 6.3 MAY

表示：References 明确支持的合法变化。

通常来自 active VAR，并必须说明：

- 什么可以变化；
- Evidence 支持的相对范围或类型；
- 变化时仍保持什么核心；
- 接近何种边界会产生漂移。

MAY 不得在 PR、QR 或后续 SK 编译中自动升级为 SHOULD 或 MUST。

### 6.4 AVOID

表示：某一方向容易导致 Style Drift、质量下降或越过合法 Variation 边界，应尽量避免，但不是所有出现都构成绝对失败。

通常来自：

- active ANTI 的 soft risk；
- context-dependent contamination；
- 有证据的 boundary risk；
- 尚未达到绝对排除强度的重复失败模式。

AVOID 应说明风险为何与视觉身份冲突，以及什么 Context 可能仍然合法。

### 6.5 DO NOT

表示：某一方向明确违反目标 Visual Family、Scope Boundary 或核心视觉系统。

通常要求：

- active、high-confidence、`core` 或 `important` ANTI；
- 明确的身份冲突、职责越界或重复 Critical Failure；
- 没有 Reference-supported VAR 允许该方向；
- 禁止范围可以清楚界定。

Scope Boundary 若需要形成 DO NOT，必须先在分析与 Traceability 中形成合法 ANTI 来源。不得绕过主链直接把 Brief 文本编译为视觉禁令。

## 7. Strength Assignment

Rule Strength 必须综合：

- Evidence Frequency；
- Importance；
- Confidence；
- Phase 1A Reference Weight；
- Visual Identity Impact；
- Variation Support；
- Anti-pattern Severity；
- Contradiction 与 Context。

Compiler 不使用机械分数或单一因子。Strength 决策至少回答：

1. 上游角色是 INV、VAR、ANTI，还是它们的组合？
2. Evidence 来自哪些 Core / Supporting References？
3. Confidence 和 Importance 是什么？
4. 缺失或违反该机制会产生什么身份后果？
5. 是否存在合法 Variation 或 Contextual Exception？
6. 该强度是否比上游 Evidence 更强？

如果最后一问为“是”且没有新增 Evidence，Strength 不得采用。

Strength 与 Priority 是不同概念：Strength 描述规则约束力；Priority 描述冲突、压缩和执行时的关注顺序。一个保护合法 Variation 的 MAY 可以具有很高 Priority，而不能因此变成 MUST。

## 8. Rule Priority

目标 Skill 可以根据当前视觉身份建立以下通用优先级语义：

- **Priority 1 — Identity / Scope Critical**：决定核心身份或防止明确职责越界；
- **Priority 2 — Stability Critical**：显著影响跨输入稳定性、关键边界或高风险漂移；
- **Priority 3 — Variation / Boundary Control**：保护合法变化并限制其边界；
- **Priority 4 — Supporting Detail**：提高完整性，但不决定核心身份。

Priority 必须来自 Invariant Importance、Evidence Confidence、Identity Impact、Generation Stability 与 Variation / Boundary 后果。

规则：

- 不按文件顺序自动分配 Priority；
- 不把所有 MUST 都机械设为同一 Priority；
- 不因 MAY 语气较弱而降低重要 Variation 的 Priority；
- Priority 4 仍必须通过 Rule Admission Test，否则不应成为正式 Rule。

## 9. Rule Admission Test

任何候选 VR、PR 或 QR 在进入正式 Visual System 前，必须回答：

1. **Legal source**：是否有合法 active 上游 Entity 与 Reference Evidence？
2. **Generation utility**：是否能帮助生成模型实现某个正式视觉要求？
3. **Evaluation utility**：是否能帮助判断生成结果？
4. **Executable meaning**：是否超越抽象形容词，具有可执行或可观察含义？
5. **Non-duplication**：是否只是已有 Rule 的同义重复？
6. **Role integrity**：是否把 Incidental Detail 或未晋升 Observation 错写成 Rule？
7. **Variation safety**：是否侵犯或消除 active Allowed Variation？
8. **No unsupported expansion**：是否增加 References 未支持的新风格、参数或边界？
9. **Scope fit**：是否属于当前 Phase 与目标 Skill 的职责？
10. **Traceability completeness**：能否建立完整 upstream、downstream、location 与 status？

Admission 结果只能是：

- **ADMIT**：独立、必要、可执行且可追踪；
- **MERGE**：机制有效，但应与现有 Rule 合并；
- **DEFER**：可能重要，但 Evidence、Context 或表达仍不足；
- **REJECT**：重复、无用、越界、unsupported 或 incidental；
- **RETURN UPSTREAM**：暴露了 Analysis / Traceability 的阻断性冲突，需要按 Phase Contracts 回退。

既不能帮助生成、也不能帮助判断的 Rule 不得 ADMIT。

## 10. Analysis Finding to Formal Rule

不是所有 Analysis Finding 都应成为 Rule。正式路径为：

```text
Analysis Finding
↓
Importance and Confidence Check
↓
Formal INV / VAR / ANTI role
↓
Traceability Check
↓
Rule Admission Test
↓
VR Candidate
```

普通解释文字、Incidental Detail、Single-instance 或未晋升 Observation 默认不进入规则系统。若后续出现新 Evidence，应先回到相应上游角色，而不是在 Phase 2 直接补 Rule。

## 11. Invariant Compilation — INV → VR

### 11.1 Eligibility

用于正式 VR 的 INV 必须：

- status 为 `active`；
- 有合法 OBS / REF Evidence；
- Confidence 与 Importance 足以支持其拟定强度；
- 与 active VAR / ANTI 的 Context 已协调；
- 没有阻断性 Evidence Gap。

### 11.2 Compilation

- identity-critical high-confidence INV 通常形成 MUST；
- 有合法例外、Context 或证据范围限制的 INV 通常形成 SHOULD；
- 多个 INV 描述同一不可分割机制时可以合并为一个 VR，并保留全部 `source_roles`；
- 一个复杂 INV 包含多个可独立执行、测试或修订的机制时应拆分为多个 VR；
- VR 必须说明视觉行为、适用范围与可观察后果，不能只改写成命令语气。

### 11.3 Coverage

每个 active core INV 必须至少映射一个 active VR。无法编译的重要 INV 会阻断 Phase 2 Gate，不能通过删除 Traceability link 隐藏。

## 12. Variation Compilation — VAR → VR

### 12.1 Eligibility

正式 VAR 必须有多个有效 Evidence 或可靠的变化结构，并明确变化范围、稳定核心与边界。

### 12.2 Compilation

VAR 可以形成：

- 独立 MAY Rule；
- 某个 MUST / SHOULD 的明确例外或 Context；
- Variation Boundary Rule；
- 用于防止模板锁定的选择结构。

### 12.3 Preservation

编译时必须保留：

- 可变化的 Dimension；
- Reference-supported options 或相对范围；
- 变化时仍保持的 Invariant；
- 越界条件；
- VAR → VR Traceability。

不得通过“默认值”无声消除其他合法选项，也不得把 MAY 写成所有输出必须选择同一表现。

## 13. Anti-pattern Compilation — ANTI → VR

### 13.1 Eligibility

ANTI 必须具有 active status、合法 OBS / REF Evidence、明确不兼容方向与可判断的 Context。

### 13.2 Strength

- **Soft Risk**：有漂移风险但不是任何 Context 下都失败，编译为 AVOID；
- **Strong Style Violation**：明确违背核心身份、Scope 或重复 Critical Failure，编译为 DO NOT。

### 13.3 Guardrail Form

Anti-pattern VR 应简洁说明：

- 要避免或禁止的视觉方向；
- 它与哪个核心身份或边界冲突；
- 适用 Context；
- 是否存在合法 Variation 例外。

不能只写没有视觉含义的 `Avoid X`，也不能把 weaker ANTI 过度升级为绝对禁令。

## 14. Visual Rule Architecture

目标 Skill 的 `visual_rules.md` 至少承担：

- **Visual Objective**：来自 Core Visual Identity 的简洁执行目标；
- **Rule Priority**：当前 Skill 的规则关注顺序；
- **Core Invariants**：最高身份保护；
- **Core Visual Rules**：由 Core Dimensions 产生的正式规则；
- **Adaptive Visual Rules**：只包含已晋升 Adaptive Dimensions 的规则；
- **Allowed Variation**：合法变化、稳定核心与边界；
- **Anti-pattern / Boundary Rules**：有证据的 AVOID / DO NOT；
- **Traceability Index**：VR ID、source roles、strength 与 location。

具体视觉模块由当前 Reference Analysis 决定。没有 Evidence 的 Dimension 不创建占位规则章节，也不强制每个 Skill 使用同一章节表。

每条正式 VR 至少应能识别：

- VR ID；
- statement；
- rule strength；
- priority；
- Context / condition；
- source INV / VAR / ANTI；
- 必要的 variation or boundary note。

## 15. Prompt Rule Architecture

目标 Skill 的 `prompt_rules.md` 至少承担：

- Prompt Construction Logic；
- Description Priority；
- Concrete Description Strategy；
- Preferred Vocabulary；
- Conditional / Risky / Avoid Vocabulary；
- Variation Expression；
- Guardrail Language；
- Anti-pattern Handling；
- Prompt Failure Risks；
- Traceability Index。

每条正式 PR 至少应能识别：

- PR ID；
- source VR IDs；
- expression objective；
- applicable Context；
- rule strength；
- wording strategy；
- known ambiguity or failure risk。

PR 不能用更强措辞改变 VR，也不能通过 Prompt 习惯引入新风格。

## 16. Prompt Construction Logic

Prompt Rules 应定义可调整的构建逻辑，而不是一个固定句子模板。

通用过程为：

1. 确认当前生成任务的 primary visual object 与职责边界；
2. 选择对当前任务适用的 active VR；
3. 依据 Priority、Strength 与 Context 组织必要信息；
4. 先表达具体对象、状态、关系与可见属性；
5. 加入当前 Skill 需要的空间、构图、光线、色调、材质、深度或 Adaptive Dimension 信息；
6. 明确 Allowed Variation 的当前选择，同时保留其稳定核心；
7. 只加入与当前任务相关的 AVOID / DO NOT Guardrails；
8. 删除重复、冲突和只提供抽象气氛的词；
9. 检查每段 Prompt Language 均能回溯到 PR → VR。

信息顺序可以按目标 Skill 调整。Compiler 不把某个历史 Skill 的 Prompt 顺序写成 Universal Rule。

## 17. Concrete Description First

> Style adjective cannot replace executable visual description.

Prompt Rules 应优先表达：

- 可见的视觉对象与状态；
- 可执行的构图和空间关系；
- 可观察的光线、色调、表面和深度特征；
- Reference-supported Adaptive Dimension；
- 明确的变化边界和 Guardrail。

抽象 Style Character 可以作为压缩总结，但不能成为唯一生成指令。一个形容词若不能说明模型应该呈现什么可见特征，应被具体化、限定或删除。

这不是全局禁止抽象词，而是禁止用抽象词替代 Visual Rules。

## 18. Prompt Vocabulary

每个目标 Skill 可以根据自身 VR 和已记录生成行为维护：

- **Preferred Vocabulary**：稳定、低歧义地表达目标 VR；
- **Conditional Vocabulary**：只在特定 Context 或 Subtype 下使用；
- **Risky Vocabulary**：可能触发错误解释，需要限定或替代表达；
- **Avoid Vocabulary**：反复导致 unsupported style、关键歧义或 ANTI contamination。

Vocabulary 规则：

- 不存在 Builder 预置的固定词表；
- 初始分类必须来自 Reference-derived visual intent 与已有可核验的生成行为；
- 没有生成证据时，对模型行为的判断保持 provisional；
- Risky 不等于绝对禁止；
- 同一词在不同 Skill 或 Context 中可以有不同分类；
- 每项 Vocabulary Guidance 必须连接实现的 VR 或防护的 ANTI；
- 后续 Test Evidence 可以触发有记录的重新分类。

## 19. Quality Rule Architecture

目标 Skill 的 `quality_rules.md` 至少承担：

- Evaluation Goal；
- Hard Fail Conditions；
- Core Quality Checks；
- Invariant Compliance；
- Variation Validity；
- Visual-family Consistency；
- Adaptive Dimension Checks；
- Anti-pattern Contamination；
- Physical / Structural / Generation Failure，若当前 Visual System 相关；
- `PASS / REVISE / FAIL` Logic；
- Revision Direction；
- Traceability Index。

每条正式 QR 至少应回答：

- QR ID；
- source VR IDs；
- what is checked；
- what counts as success；
- what counts as deviation；
- what counts as failure；
- applicable Context；
- rule strength or severity relationship。

禁止使用 `looks good`、`feels correct`、`professional` 或 `matches the vibe` 这类无法判断的标准替代可观察条件。

## 20. Quality Evaluation Architecture

### 20.1 Layer 1 — Hard Failure

只有当输出明显违反以下有 VR 支持的要求时，才可直接 FAIL：

- core MUST / Invariant；
- scope-critical DO NOT；
- critical ANTI Guardrail；
- 当前视觉系统明确要求避免的物理或结构不可能；
- 足以改变 Visual Family 的 major style drift。

Hard Fail 必须连接对应 QR → VR，不能由 QA 临时增加标准。

### 20.2 Layer 2 — Quality / Style Check

没有 Hard Fail 时，再检查：

- Core Visual Identity；
- Visual Rule compliance；
- Variation validity；
- Visual-family consistency；
- 适用的 Core / Adaptive Dimension；
- ANTI contamination；
- 其他由 active VR 定义的可观察质量。

### 20.3 Verdict Logic

- **PASS**：无 Hard Fail，核心规则成立，变化合法，未出现影响身份的偏差；
- **REVISE**：无 Hard Fail，但存在重要且可修正的规则偏差、边界风险或污染；
- **FAIL**：出现 Hard Fail，或多个偏差共同导致 Visual Family / Scope 失效。

Minor 现象只有在对应 QR 允许且不影响核心身份时，才可以随 PASS 记录；不得用平均分掩盖 Hard Fail。

## 21. Variation Preservation

编译器必须为每个 active core / important VAR 执行 Variation Preservation Check：

1. VAR 是否产生 VR 或进入相关 VR 的明确 exception / range？
2. VR 是否保留多个合法表现，而非只保留默认值？
3. PR 是否能表达变化选择，而非重复输出同一模板？
4. QR 是否能区分“合法变化”与“风格漂移”？
5. Anti-pattern Guardrail 是否误伤 VAR？
6. Strength 是否从 MAY 无依据升级？
7. Traceability 是否保留 VAR → VR → PR / QR 链？

以下做法属于 Variation Collapse：

- 把常见表现写成唯一允许表现；
- 用 MUST 固定 References 只显示为变化的属性；
- PR 永远选择同一选项；
- QR 把合法变化判为失败；
- 为消除一个风险而禁止整类 Variation。

发现 Variation Collapse 时，Phase 2 Gate 不得通过。

## 22. Rule Conflict Resolution

同一视觉维度出现冲突时，遵循：

```text
Evidence
→ Role
→ Strength
→ Context
→ Resolution
```

### 22.1 Resolution Process

1. 确认冲突是否发生在相同 Dimension、相同 Context 与相同 Scope；
2. 验证双方 source roles、status、Evidence、Confidence 与 Reference Weight；
3. 区分 Core Identity、合法 Variation、Boundary 与 Anti-pattern；
4. 比较身份影响、变化支持和 Anti-pattern Severity；
5. 优先保护 Core Visual Identity 与 Legitimate Variation；
6. 选择 contextualize、narrow、merge、split、defer 或 return upstream；
7. 更新 Traceability，并重新检查受影响的 PR / QR。

### 22.2 Common Conflict Forms

- **INV vs VAR**：把 INV 限定为稳定核心，把 VAR 表达为合法实现范围；不得让 MUST 消除 Variation；
- **VAR vs ANTI**：若同一表现、同一 Context 同时被允许与拒绝，属于上游角色冲突，必须拆分 Context 或回退分析；
- **INV vs INV**：若无法通过 Context、Subtype 或范围解释，不能编译两个互相矛盾的 MUST；
- **PR vs VR**：PR 比 VR 更窄或更强时，修正 PR，防止 Variation Collapse / Strength Distortion；
- **QR vs VR**：QR 比 VR 增加新要求或更严格时，修正或删除 QR，防止 Orphan Quality Rule。

禁止采用“更强的词自动覆盖较弱的词”。Strength 是 Evidence 结论，不是冲突解决捷径。

## 23. Rule Deduplication

多个 Finding 或 Role 如果表达同一视觉机制、相同 Scope、相同 Strength 与相同执行后果，应合并为一个 Rule，并通过多对一 Traceability 保留全部来源。

Deduplication 检查：

- statement 是否语义相同；
- Context 与 boundary 是否相同；
- Rule Strength 是否相同；
- PR / QR 实现与检测后果是否相同；
- 单独修改或测试是否有实际价值。

如果 Evidence、Context、Strength、Variation Boundary 或测试后果不同，应保留独立 Rule，不能为减少数量而合并失真。

禁止仅因措辞不同创建多个近义 VR，也禁止让 PR / QR 重复陈述完整 VR 而没有实现或检测职责。

## 24. Rule Granularity

合理 Rule 应：

- 表达一个清楚的视觉行为、变化边界或风险方向；
- 可以由 Prompt 实现；
- 可以由 Quality Rule 判断；
- 可以独立修改并评估影响；
- 具有完整 Traceability；
- 不与相邻 Rule 重复。

过大 Rule 的表现：

- 只要求整体“匹配 References”；
- 混合多个可独立失败的视觉机制；
- 无法判断是哪一部分失败。

过细 Rule 的表现：

- 同一机制被拆成大量微小同义句；
- 每条都依赖完全相同 Evidence、PR、QR 与修订动作；
- 单独测试没有意义。

如果多个属性在 References 中始终共同构成一个不可分割机制，可以保留为一个复合 Rule；必须在 statement 中保持可执行与可判断。

## 25. Traceability Update

编译器更新的是当前 Build 实例化后的 Traceability，不修改 `Templates/traceability.yaml` Schema。

### 25.1 Create VR / PR / QR

- 为 admitted Rule 分配稳定 ID；
- 写入简短 statement、`rule_strength`、status 与 location；
- VR 写入 `source_roles`；
- PR / QR 写入 `source_visual_rules`；
- 更新全部上游 Entity 的 downstream；
- 更新 VR 的 prompt_rules / quality_rules downstream；
- 对 merge 保留全部 upstream IDs；
- 对 reject / defer 保留必要的 Admission 决定或 Revision 记录；
- 不为普通解释文字创建 Entity。

### 25.2 Confidence Handling

Evidence Confidence 的 Source of Truth 保留在 OBS、INV、VAR、ANTI。VR / PR / QR 通过 upstream links 继承并暴露其 Confidence basis，不复制一个可能漂移的独立 Evidence Confidence。

Compiler 必须能够从 Rule 追溯并报告上游 Confidence；当多个来源 Confidence 不一致时，在 Rule rationale 或 Traceability `notes` 中记录 Strength 决策依据。除非未来 Traceability Specification 正式扩展 Schema，否则不得擅自增加第二套 confidence 字段。

### 25.3 Location

- VR 指向 `visual_rules.md` 的稳定 section / item；
- PR 指向 `prompt_rules.md`；
- QR 指向 `quality_rules.md`；
- 不要求行号；
- 章节调整只更新 location，不改变 ID。

### 25.4 Integrity Check

同步后至少检查：

- no Untraced Rule；
- no Broken / Asymmetric Link；
- no Orphan Quality Rule；
- no Invalid Active Dependency；
- core INV / important VAR / important ANTI coverage；
- Rule Strength Preservation。

## 26. Phase Boundary

本 Compiler 严格属于 Phase 2，可以：

- 创建或修改目标 Skill 的 Visual / Prompt / Quality Rules；
- 创建 VR / PR / QR Traceability；
- 解决三层内部冲突与重复；
- 判断 `READY FOR SKILL COMPILATION`。

本 Compiler 不得：

- 修改 Reference Set；
- 无证据修改 Reference Analysis；
- 创建目标 `SKILL.md` 或 SK Entity；
- 执行 Phase 3B Static Audit；
- 创建 TC 或运行真实生成测试；
- Freeze 目标 Skill；
- 修改历史 Reference Implementation；
- 重新设计 Traceability Schema。

发现上游问题时，按 `phase_contracts.md` 执行 Minimal Upstream Rollback。

## 27. Visual System Readiness Gate

Phase 2 最终 Verdict 只能是：

- `READY FOR SKILL COMPILATION`；或
- `NOT READY`。

### 27.1 READY Conditions

只有同时满足以下条件，才可以判定 READY：

- 三个目标 System Artifact 均已创建且职责分离；
- 所有 active core INV 均被至少一个 VR 覆盖；
- 所有 active core / important VAR 均被保留，且无 Variation Collapse；
- 所有 active core / important ANTI 均有强度合理的 Guardrail；
- 每个正式 VR 均通过 Rule Admission Test 并具有合法 source roles；
- 每个正式 PR / QR 均连接至少一个 VR；
- 每个正式 VR 均至少有一个可执行 PR 与一个可判断 QR；
- Rule Strength 有 Evidence、角色、Confidence、Importance 与 Context 支持；
- Rule Priority 已建立且没有被误当作 Strength；
- 没有 unsupported visual rule；
- 没有 Incidental Detail Overfitting；
- 没有明显 duplicate rule 或不可执行的 abstract-only rule；
- Visual / Prompt / Quality 三层语义一致；
- Prompt Vocabulary 没有成为新 Style Source；
- QR 没有增加 VR 未定义的要求；
- 冲突已解决、Contextualized，或被明确退回上游；
- Traceability upstream / downstream / location / status 已同步；
- 不存在阻断性的 Traceability Integrity Error；
- 未执行任何 Phase 2 Forbidden Mutation。

### 27.2 NOT READY Conditions

以下任一情况通常意味着 NOT READY：

- 关键 INV 没有 VR Coverage；
- 重要 VAR 被固定、丢失或无法表达；
- 重要 ANTI 没有 Guardrail；
- PR / QR 缺少 VR 来源；
- VR 无法被实现或判断；
- Strength 依赖主观偏好或比 Evidence 更强；
- 规则存在未解决冲突、重复或过度碎片化；
- Incidental Detail 被升级为正式规则；
- Vocabulary 引入上游未支持的视觉内容；
- Quality Rule 构成 Orphan Requirement；
- Traceability 存在阻断性错误；
- 需要回退 Phase 1B 才能解决的 Evidence / Role 问题。

NOT READY 时 Build 停留在 Phase 2，或按 Minimal Upstream Rollback 返回 Phase 1B。不得为了推进到 Skill Compilation 而降低 Admission 或 Traceability 要求。

## 28. Compiler Boundary

本文件不负责：

- 为任何历史或未来目标 Skill 编写真实视觉规则；
- 创建 `System/skill_compiler.md`；
- 创建 Audit Protocol 或 Test Protocol；
- 创建 SK / TC Entity；
- 编译最终 `SKILL.md`；
- 执行 Static Audit、真实生成、Regression 或 Freeze；
- 修改 Reference Analysis、Traceability Schema 或历史 Skill。

这些工作只能由后续明确授权的 Phase 完成。
