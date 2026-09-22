# build-image-skill — Traceability Specification

## 1. Purpose

本文件定义 `build-image-skill` 的正式 Traceability 机制，使重要视觉结论、执行规则、Skill Rule 与 Test Case 能够回溯到具体 Reference Evidence。

Traceability 的目标是：

```text
Explain origin
Preserve meaning
Detect loss
Support audit
Support testing
Support refinement
```

Traceability 是轻量的 index / relationship layer，不是第二套知识库。详细分析、规则正文与测试结果仍保存在各自 Artifact 中。

## 2. Core Traceability Chain

正式主链为：

```text
REF
↓
OBS
↓
INV / VAR / ANTI
↓
VR
↓
PR / QR
↓
SK
↓
TC
```

| Prefix | Entity |
|---|---|
| `REF` | Reference |
| `OBS` | Observation |
| `INV` | Invariant |
| `VAR` | Allowed Variation |
| `ANTI` | Anti-pattern |
| `VR` | Visual Rule |
| `PR` | Prompt Rule |
| `QR` | Quality Rule |
| `SK` | Skill Rule |
| `TC` | Test Case |

这是一条逻辑主链，不是一对一流水线。一个节点可以有多个上游与多个下游；重要结论可以合并多条 Evidence，规则也可以被多个 Skill Rule 或 Test Case 消费。

## 3. Common Entity Contract

所有 Traceability Entity 均应支持以下基础信息：

| Field | Purpose |
|---|---|
| `id` | 当前 Build 内唯一、稳定的人类可读 ID |
| `statement` 或 `title` | 简短表达该 Entity 的意义，不复制完整正文 |
| `location` | 指向正式 Artifact 的 file / section / item |
| `status` | 当前生命周期状态 |
| `notes` | 必要补充，默认保持简短 |

Evidence Entity 还需要记录 Evidence 与 Confidence；Rule Entity 还需要预留 Rule Strength；所有 Entity 必须能够通过类型专属关系字段形成上游与下游链接。

`location` 用于定位正文，Traceability YAML 中的短 statement 只充当索引。没有独立正文文件的 REF 可以把 `location.source_file` 直接指向 Reference Source。

## 4. Entity Types

### 4.1 REF — Reference

REF 表示一张具体 Reference Image 或一个明确 Reference Source，是视觉证据链的原始来源。

要求：

- 每个可引用 Reference 有唯一 REF ID；
- ID 创建后保持稳定，不随分类、排序或文件展示顺序变化；
- Core、Supporting、Ambiguous 与 Outlier 均可以拥有 REF ID；
- `role` 继承 Phase 1A 的 Reference classification；
- Outlier 是证据角色，不等于 `rejected` status；
- REF 本身只表示原始证据，不自动证明任何视觉结论。

最小字段：

- `id`；
- `location`；
- `role`；
- `status`；
- `downstream.observations`；
- `notes`。

### 4.2 OBS — Observation

OBS 表示从一个或多个有效 References 中观察到的视觉事实、重复模式或可比较差异。

OBS 必须：

- descriptive；
- evidence-based；
- non-prescriptive；
- 至少连接一个 REF；
- 区分支持 Evidence 与矛盾 Evidence；
- 不使用 `MUST / SHOULD / MAY / AVOID / DO NOT`。

Analysis Dimension 只作为 OBS 的分类上下文，不需要 Traceability ID。

最小字段：

- `id`；
- `statement`；
- `analysis_dimensions`；
- `evidence.source_refs`；
- `evidence.contradicting_refs`；
- `confidence`；
- `importance`；
- `status`；
- `location`；
- `downstream.invariants / variations / anti_patterns`；
- `notes`。

### 4.3 INV — Invariant

INV 表示明显缺失、反转或替换后会显著改变目标 Visual Family 身份的核心视觉属性。

INV 必须：

- 至少连接一个 OBS；
- 能沿 OBS 回溯到 Reference Evidence；
- 记录直接支持的 REF 集合作为便于审计的 Evidence 索引；
- 具有足以支持核心身份判断的 Confidence；
- 不由 Single-instance 单独支持；
- 在后续 Visual System、Skill 与 Test 中获得覆盖。

最小字段：

- `id`；
- `statement`；
- `evidence.source_refs`；
- `evidence.supporting_observations`；
- `evidence.contradicting_refs`；
- `confidence`；
- `importance`；
- `status`；
- `location`；
- `downstream.visual_rules / skill_rules / test_cases`；
- `notes`。

### 4.4 VAR — Allowed Variation

VAR 表示可以变化、但仍属于同一 Visual Family 的视觉维度、状态或相对范围。

VAR 的作用是防止稳定性退化为固定模板。它必须说明变化的对象、Evidence 支持的范围，以及变化时仍保持的视觉核心。

最小字段与 INV 相同，但其下游覆盖应特别支持：

- Visual Rule 中的变化表达；
- Skill 中的变化能力；
- Variation Test Coverage。

### 4.5 ANTI — Anti-pattern

ANTI 表示与目标 Visual Family 不兼容、容易造成稳定 Style Drift 的视觉方向。

ANTI 必须来自：

- Reference comparison；
- Outlier 或 contamination evidence；
- Core Identity 的明确反方向；
- 已有并可核验的稳定失败证据。

它不能由 Builder 的固定风格清单产生。最小字段与 INV 相同，但其下游覆盖应特别支持 Visual Guardrail、必要的 Prompt Guardrail、Skill Guardrail 与 Stress Test。

### 4.6 VR — Visual Rule

VR 表示从一个或多个 INV / VAR / ANTI 编译出的视觉执行规则。

VR 必须：

- 通过 `source_roles` 连接至少一个 INV、VAR 或 ANTI；
- 不独立发明视觉内容；
- 预留 `rule_strength`；
- 保持上游角色的意义与适用范围；
- 能被 PR、QR 或 SK 消费。

最小字段：

- `id`；
- `statement`；
- `source_roles`；
- `rule_strength`；
- `status`；
- `location`；
- `downstream.prompt_rules / quality_rules / skill_rules`；
- `notes`。

### 4.7 PR — Prompt Rule

PR 表示为了让生成模型稳定实现某个 Visual Rule，Prompt 应如何表达。

PR 必须：

- 连接一个或多个 VR；
- 不成为新的 Style Source of Truth；
- 不加入 VR 上游未支持的视觉内容；
- 预留并保持必要的 Rule Strength；
- 能映射到使用它的 Skill Rule。

最小字段：

- `id`；
- `statement`；
- `source_visual_rules`；
- `rule_strength`；
- `status`；
- `location`；
- `downstream.skill_rules`；
- `notes`。

### 4.8 QR — Quality Rule

QR 表示如何判断生成结果是否满足一个或多个 Visual Rules。

QR 必须：

- 连接一个或多个 VR；
- 检查上游已经定义的视觉要求；
- 能支持后续 PASS / REVISE / FAIL 判断；
- 不增加新的视觉标准；
- 能映射到使用它的 Skill Quality / Self-check Rule。

最小字段与 PR 相同，使用 `source_visual_rules` 和 `downstream.skill_rules`。

### 4.9 SK — Skill Rule

SK 表示最终进入目标 `SKILL.md` 的执行规则或关键执行模块。

SK 必须：

- 通过 `source_rules` 连接正式 VR、PR 或 QR；
- 保持上游 Rule Strength 与职责范围；
- 保留核心 Invariant；
- 保留合法 Variation；
- 保留必要 Anti-pattern Guardrail；
- 不成为新的上游视觉来源。

一个 SK 可以压缩合并多个上游 Rule，但必须保留所有来源链接。

最小字段：

- `id`；
- `statement`；
- `source_rules`；
- `rule_strength`；
- `status`；
- `location`；
- `downstream.test_cases`；
- `notes`。

### 4.10 TC — Test Case

TC 表示用于验证一个或多个 Skill Rule、Invariant、Allowed Variation 或 Anti-pattern 的正式测试案例。

TC 必须：

- 通过 `verifies` 明确声明验证对象；
- 记录 `case_type`，供后续 Test Protocol 区分 Core、Variation、Stress 与 Boundary；
- 不只记录测试名称；
- 连接实际被验证的 INV、VAR、ANTI 或 SK；
- 把详细 Prompt、Expected Behavior 与 Result 留在正式 Test Artifact，而非复制进 Traceability YAML。

最小字段：

- `id`；
- `title`；
- `case_type`；
- `verifies`；
- `status`；
- `location`；
- `notes`。

## 5. ID Convention

### 5.1 Format

ID 使用：

```text
REF-001
OBS-001
INV-001
VAR-001
ANTI-001
VR-001
PR-001
QR-001
SK-001
TC-001
```

规则：

- Prefix 必须与 Entity Type 一致；
- 数字部分在当前 Build 的同类 Entity 中唯一；
- 三位数字是起始可读格式，超过容量时可自然扩展；
- 完整跨 Build 引用使用 `build_id + entity_id`；
- 不使用 UUID，除非未来出现本规范无法满足的明确需求。

### 5.2 Stability

- ID 在 Entity 正式创建时分配；
- 不因排序、章节移动、文件重命名或内容轻微修订而重编号；
- 废弃或拒绝的 ID 保留，不得复用；
- 编号空缺是合法状态；
- 错误合并、拆分或角色重分类时，保留旧 ID 与状态，通过 Revision Record 指向新 Entity；
- 不允许无声删除后用同一 ID 表示不同含义。

## 6. Relationship Model

### 6.1 Many-to-many

Schema 必须支持：

- 多个 REF 支持一个或多个 OBS；
- 多个 OBS 支持一个 INV / VAR / ANTI；
- 一个 OBS 支持多个结果角色；
- 一个 INV / VAR / ANTI 产生多个 VR；
- 一个 VR 产生多个 PR / QR；
- 多个 VR / PR / QR 被压缩为一个 SK；
- 一个规则被多个 SK 使用；
- 一个 TC 验证多个 INV / VAR / ANTI / SK；
- 一个 INV / VAR / ANTI / SK 被多个 TC 覆盖。

不得假设任何阶段严格一对一。

### 6.2 Allowed Primary Links

| From | To | Meaning |
|---|---|---|
| REF | OBS | Reference supports or contradicts an observation |
| OBS | INV / VAR / ANTI | Observation supports an analysis result role |
| INV / VAR / ANTI | VR | Analysis result is compiled into a visual rule |
| VR | PR / QR | Visual rule gains prompt expression or quality evaluation |
| VR / PR / QR | SK | Formal system rule is compiled into the Skill execution layer |
| INV / VAR / ANTI / SK | TC | Test case declares what it validates |

Direct `source_refs` on INV / VAR / ANTI are Evidence indexes for easier auditing；它们不能替代必须存在的 OBS link。

### 6.3 Upstream and Downstream

上游字段是 Entity 来源的正式记录：

- OBS：`evidence.source_refs`；
- INV / VAR / ANTI：`evidence.supporting_observations` 与 `evidence.source_refs`；
- VR：`source_roles`；
- PR / QR：`source_visual_rules`；
- SK：`source_rules`；
- TC：`verifies`。

`downstream` 是反向索引，便于回答“这个 Entity 后来被哪里使用”。每条正式关系必须双向一致：上游 Entity 的 downstream 包含下游 ID，下游 Entity 的 source / verifies 字段也包含上游 ID。

若两侧不一致，以原始 Evidence 和 Owner Phase Artifact 为依据修复关系，不得凭 YAML 的较新时间戳判断哪一侧正确。

## 7. Evidence Support

### 7.1 OBS Evidence

每个 active 或 provisional OBS 至少需要：

- 一个存在且可用的 REF ID；
- 与 statement 一致的可见事实；
- Phase 1A role 可识别；
- Confidence；
- 已知矛盾 Reference，若存在。

### 7.2 INV / VAR / ANTI Evidence

每个 active 或 provisional INV / VAR / ANTI 至少需要：

- 一个存在且状态允许使用的 OBS ID；
- 可沿 OBS 回溯的 REF Evidence；
- `source_refs` 便捷索引；
- `supporting_observations`；
- `confidence`；
- `importance`；
- 已知 contradicting refs；
- 必要说明。

`source_refs` 与 OBS 路径出现差异时，视为需审计的不一致，不得用直接 REF link 绕过 OBS。

### 7.3 Evidence Sufficiency

- Single-instance 不得单独支持 active INV；
- 低权重或 Ambiguous Evidence 不得单独支撑核心结论；
- Outlier 可支持边界比较和 ANTI，但不能定义 Core Visual Identity；
- Brief 或外部知识不能作为 REF 或 OBS；
- `Insufficient Evidence` 的结论不得被伪装成 active high-confidence Rule 来源。

## 8. Confidence

适用于 OBS、INV、VAR、ANTI：

- `high`：多个高权重 References 一致支持，覆盖充分，重要矛盾很少或已解释；
- `medium`：多个有效 References 支持，但覆盖有限或存在可解释矛盾；
- `low`：支持有限、权重较低、范围不清或存在明显矛盾；
- `insufficient`：无法从当前 Evidence 形成可靠结论。

规则：

- Confidence 不是概率，不使用伪精确数值；
- Confidence 不等于 Frequency、Importance 或 Rule Strength；
- 下游不能把 `low / insufficient` 静默提升为强规则；
- Confidence 改变必须有 Evidence 与 Revision Reason。

## 9. Importance

OBS、INV、VAR 与 ANTI 支持：

- `core`：影响核心身份或强制覆盖要求；
- `important`：影响稳定性、变化、边界或质量，但不是核心身份本身；
- `supporting`：有分析价值，但不触发全部核心覆盖要求。

Importance 用于决定覆盖优先级，不能代替 Confidence。高重要性但低 Confidence 的条目必须先补证据或保持 provisional，不能直接编译为正式强规则。

## 10. Status

所有 Entity 使用：

- `active`：当前 Build 中正式有效；
- `provisional`：已记录但仍等待证据、Gate 或正式确认；
- `deprecated`：曾有效但已被修订或替代，保留历史；
- `rejected`：经评估不进入正式链，保留拒绝原因。

规则：

- Outlier REF 可以是 `active`，其证据角色由 `role` 表达；
- active 下游不得依赖 rejected Entity；
- 依赖 deprecated Entity 时必须转向其 successor，或明确记录临时原因；
- deprecated / rejected ID 不得删除或复用；
- 状态变化必须追加 Revision Record。

## 11. Rule Strength Preservation

VR、PR、QR 与 SK 预留 `rule_strength` 字段。正式枚举与编译规则由 Visual System Compiler 定义，本规范不提前固定 `MUST / SHOULD / MAY / AVOID / DO NOT` 的语义。

Traceability 必须支持检查：

```text
INV / VAR / ANTI
→ VR
→ PR / QR
→ SK
```

在传递中是否发生未经证据支持的加强、削弱或角色改变。

原则：

- 每个 Rule Entity 记录自身实际 strength；
- strength 变化必须能回溯到上游 Entity 或 Revision Evidence；
- VAR 不得在无依据时被压缩成固定硬规则；
- ANTI 不得因措辞方便被自动升级为绝对禁止；
- 核心 INV 不得在 SK 编译中被无声弱化或丢失；
- `rule_strength: null` 只允许出现在尚未进入正式规则编译的 provisional 条目中。

## 12. Coverage Requirements

### Requirement 1 — No Untraced Rule

任何 active VR、PR、QR、SK 必须存在合法上游来源。

### Requirement 2 — Invariant Coverage

每个 active INV 最终必须至少连接到：

- 一个 active VR；
- 一个 active SK；
- 一个 active TC。

### Requirement 3 — Variation Coverage

每个 `core` 或 `important` active VAR 最终必须具有：

- Visual System 中的支持；
- Skill 中的支持；
- `variation` TC Coverage。

### Requirement 4 — Anti-pattern Coverage

每个 `core` 或 `important` active ANTI 最终应具有：

- 对应 VR Guardrail；
- 必要时的 PR Guardrail；
- SK Guardrail；
- `stress` TC Coverage。

如果某一层确实不适用，必须记录理由；不能仅留空。

### Requirement 5 — Quality Rule Origin

每个 active QR 必须连接至少一个 active VR。QR 不得检查上游未定义的视觉要求。

### Requirement 6 — Skill Compilation Coverage

每个 active SK 必须连接至少一个 active VR、PR 或 QR，并能沿链回溯到 INV / VAR / ANTI 与 REF Evidence。

### Requirement 7 — Test Declaration

每个 active TC 必须通过 `verifies` 声明至少一个 active INV、VAR、ANTI 或 SK。Case Type 必须与主要验证目的相容。

## 13. Traceability Integrity Errors

### 13.1 Untraced Rule

active VR、PR、QR 或 SK 没有合法上游来源，或无法沿链回到 Reference Evidence。

### 13.2 Dropped Invariant

active INV 没有进入 Visual System 或最终 Skill。

### 13.3 Untested Invariant

active INV 已进入 Skill，但没有 active TC Coverage。

### 13.4 Orphan Quality Rule

active QR 没有对应 VR，或检查了上游未定义的视觉要求。

### 13.5 Unsupported Skill Rule

active SK 无法回溯到正式 VR / PR / QR，或其内容超出上游支持范围。

### 13.6 Variation Collapse

active VAR 在 VR 或 SK 中消失、被写死，或没有 Variation TC Coverage。

### 13.7 Anti-pattern Coverage Gap

`core` 或 `important` active ANTI 缺少必要 Guardrail 或 Stress TC。

### 13.8 Strength Distortion

Rule Strength 沿 INV / VAR / ANTI → VR → PR / QR → SK 传递时，被无证据加强、削弱或改变角色。

### 13.9 Evidence Gap

OBS 缺少 REF，或 INV / VAR / ANTI 缺少 OBS、可回溯 REF、Confidence 或必要 Evidence。

### 13.10 Broken Link

关系字段引用不存在、错误 Prefix、错误 Build 或已无法使用的 ID。

### 13.11 Asymmetric Link

上游记录了 downstream，但下游未记录对应 source / verifies；或反之。

### 13.12 Invalid Active Dependency

active Entity 依赖 rejected Entity，或在没有迁移说明时依赖 deprecated Entity。

这些错误类型供后续 Audit Protocol 使用；本阶段不定义 severity、自动修复或完整 Rubric。

## 14. Phase Ownership

| Entity | Primary owner phase | Creation responsibility |
|---|---|---|
| REF | Phase 1A | 为可引用 References 分配稳定身份并记录 role |
| OBS | Phase 1A / Phase 1B | 1A 可记录审计观察；1B 创建正式分析 Observation |
| INV / VAR / ANTI | Phase 1B | 从正式 OBS 与 Reference Evidence 形成结果角色 |
| VR / PR / QR | Phase 2 | 把分析结果编译为 Visual System |
| SK | Phase 3A | 把正式 System Rules 编译进 `SKILL.md` |
| TC | Phase 4 | 声明测试对 INV / VAR / ANTI / SK 的覆盖 |

后续 Phase 可以依据 Audit 或 Test Evidence 修改状态、关系或正文定位，但必须：

- 遵守 `phase_contracts.md` 的 Mutation / Rollback 规则；
- 保留稳定 ID；
- 追加 Revision Record；
- 重新验证受影响的下游 Gate；
- 不静默重写历史。

## 15. Phase Gate Expectations

本规范不修改 `phase_contracts.md`，但 Traceability 在未来应支持以下 Gate 检查：

### Phase 1A Exit

- 所有被审核或后续需要引用的 References 已有稳定 REF Identity；
- REF role 与 Reference Set Audit 一致；
- 已记录的审计 OBS 能回溯到 REF。

### Phase 1B Exit

- 关键 OBS 已连接 Evidence；
- active INV / VAR / ANTI 已连接 OBS 与 REF；
- Confidence、Importance、Status 与定位已记录；
- 核心结论没有 Evidence Gap。

### Phase 2 Exit

- active 核心 INV / VAR / ANTI 已映射到 VR；
- active PR / QR 均有 VR 来源；
- 关键 Rule Strength 可比较；
- 不存在阻断性的 Untraced Rule、Orphan Quality Rule 或 Strength Distortion。

### Phase 3A Exit

- 核心 Visual System Rules 已映射到 SK；
- 压缩合并没有丢失来源；
- INV、VAR 与 ANTI 的语义和强度仍可追踪。

### Phase 3B Audit

- 检查全部 Integrity Errors；
- 确认 Critical / Major Traceability 问题已解决后才允许进入 Test；
- SK 修订后同步更新 links、location 与 Revision Record。

### Phase 4

- TC 明确覆盖核心 INV、重要 VAR、重要 ANTI 与 SK；
- Refinement 能记录修改原因与 Test Evidence；
- Rule 修订后重新检查 Traceability、Audit、Retest 与 Regression；
- Freeze 时不存在阻断性 Integrity Error。

## 16. Granularity Principle

> Trace what matters to generation, validation, or revision.

正式 ID 优先用于：

- 重要 Observation；
- Invariant；
- Allowed Variation；
- Anti-pattern；
- 正式 VR / PR / QR；
- 核心 Skill Rule 或关键执行模块；
- 正式 Test Case。

以下内容通常不需要独立 ID：

- 过渡句；
- 普通解释文字；
- 重复释义；
- 没有生成、判断或修订后果的微小细节；
- Core / Adaptive Dimension 本身；
- 文件标题与格式性章节。

如果两个结论总是一起产生、一起编译、一起测试，可以合并为一个 Entity；如果它们具有不同 Evidence、Rule Strength、Variation Boundary 或测试后果，应拆分。

## 17. Update and Revision Principle

Traceability 更新遵循：

```text
Append / Update with evidence
Preserve stable IDs
Do not silently rewrite history
Mark deprecated items explicitly
```

### 17.1 Ordinary Update

statement 的非实质性澄清、文件位置变化或新增 downstream link 可以更新原 Entity，但应保持 ID，并在必要时记录 Revision。

### 17.2 Meaning Change

如果 Entity 的核心含义、角色或证据基础发生实质变化：

- 将旧 Entity 标记为 `deprecated` 或 `rejected`；
- 创建新 Entity 与新 ID；
- 在 Revision Record 中记录 predecessor / successor、原因与 Evidence；
- 更新所有 active downstream links；
- 重新验证受影响的 Gate。

例如 INV 被证明只是 Variation 时，不把同一 `INV-*` ID 改造成 `VAR-*`。保留旧 INV，改变其状态，并创建新的 VAR。

### 17.3 Revision Record

Revision Record 至少保存：

- `sequence`；
- `entity_id`；
- `change`；
- `reason`；
- `evidence_ids`；
- `prior_status`；
- `new_status`；
- `predecessor / successor`，若适用；
- `location`；
- `notes`。

它只记录关系和理由，不替代后续完整 Refinement Log。

## 18. File and Section References

每个 Entity 使用轻量定位结构：

```yaml
location:
  source_file: null
  source_section: null
  source_item: null
```

规则：

- `source_file` 指向正式 Artifact 或 Reference Source；
- `source_section` 记录稳定章节名；
- `source_item` 可记录条目名、表格键或其他局部定位；
- 不要求精确行号；
- 文件移动时更新 location，不改变 Entity ID；
- YAML 不复制对应章节全文。

## 19. Interface with Analysis Framework

Core / Adaptive Dimension 是分析组织方式，不自动成为 Traceability Entity：

```text
Core or Adaptive Dimension
↓
produces important Observation
↓
OBS
↓
INV / VAR / ANTI
```

接口要求：

- OBS 可以在 `analysis_dimensions` 中记录一个或多个 Dimension 名称；
- Adaptive Promotion 决定本身只有在影响生成、验证或修订时才需要 OBS 或 Revision 记录；
- Recurring Pattern 只有达到正式重要程度才创建 OBS；
- Invariant、Variation、Anti-pattern 必须连接其 supporting observations；
- Incidental Detail 默认不创建正式 Entity，除非后续需要解释拒绝、边界或修订。

## 20. Interface with Visual System Compiler

本规范为未来编译保留：

```text
INV / VAR / ANTI
↓
VR
↓
PR / QR
```

Visual System Compiler 需要进一步定义：

- Rule Strength 枚举与转换原则；
- 一个结果角色何时产生一个或多个 VR；
- PR / QR 的完整字段和编译检查；
- 规则合并、拆分与冲突处理；
- 三层规则的最小覆盖标准。

它不得绕过 `source_roles` 或用 Prompt / Quality Rule 发明视觉要求。

## 21. Interface with Skill Compiler

Skill Compiler 必须支持：

```text
VR / PR / QR
↓
SK
```

并能够回答：

- 哪些 Rule 已进入 Skill；
- 哪些 Rule 被压缩合并；
- 哪些 Rule 被有理由省略；
- 哪些 Invariant 被丢失；
- 哪些 Variation 被写死；
- 哪些 Anti-pattern Guardrail 未保留；
- 哪些 Rule Strength 发生变化。

压缩合并时，一个 SK 的 `source_rules` 可以包含多个 ID；省略 active 核心 Rule 必须有可审计理由，不能只删除链接。

## 22. Interface with Test Protocol

Test Protocol 必须使 TC 能够声明：

```text
INV  → Core TC
VAR  → Variation TC
ANTI → Stress TC
Boundary behavior → Boundary TC
SK   → Execution coverage
```

一个 TC 可以验证多个 Entity；一个 Entity 也可以由多个 TC 验证。`verifies` 记录验证目标，详细 Prompt、Expected Behavior、Rubric、Result 与 Diagnosis 保留在 Test Artifacts。

Test 触发规则修订时，TC ID 可作为 Revision Evidence。修订后的 Entity 必须重新检查相关 TC Coverage 与 Regression。

## 23. YAML Schema Contract

`Templates/traceability.yaml` 使用：

- 一个 `meta` mapping；
- 十个按 Entity Type 分组的 top-level sequences；
- 一个轻量 `revisions` sequence。

### 23.1 Required Top-level Keys

```text
meta
references
observations
invariants
variations
anti_patterns
visual_rules
prompt_rules
quality_rules
skill_rules
test_cases
revisions
```

### 23.2 YAML Rules

- 所有 ID 使用字符串；
- 所有关系列表使用 ID 字符串数组；
- 空集合使用 `[]`；
- 未填写标量使用 `null`，不要用含义不清的空字符串；
- Confidence 与 Status 使用本规范枚举；
- detailed正文不复制进 YAML；
- upstream 与 downstream 双向链接必须同步；
- 模板中的注释用于说明 item shape，不构成 Traceability 数据；
- 实际 Build 只向相应 sequence 添加正式条目。

## 24. Specification Boundary

本规范不负责：

- 定义 Visual System Compiler；
- 正式定义 Rule Strength 枚举和编译算法；
- 创建真实 VR、PR、QR、SK 或 TC；
- 定义 Skill Compiler、Audit Protocol 或 Test Protocol；
- 创建数据库、知识图谱或代码实现；
- 为历史 Skill 填充 Traceability 数据；
- 执行 Historical Backtest。

这些工作只能由后续明确授权的阶段完成。
