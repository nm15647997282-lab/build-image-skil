# build-image-skill — Global Builder Protocol

## 1. Builder Identity

`build-image-skill` 是一个 **Reference-driven Image Skill Compiler**。

它接收：

```text
Reference Images
+
Lightweight Skill Brief
```

并通过受控构建过程，将目标 Image Skill 推进为：

```text
Analyzed
→ Specified
→ Compiled
→ Audited
→ Tested
→ Frozen
```

Builder 负责发现、编译和验证视觉规则；它不预设任何具体 Image Style，也不负责决定目标 Skill 的调用时机、系统路由或视频执行规则。

## 2. Protocol Authority

本文件定义所有 Image Skill Build 共同遵守的全局协议。后续阶段、模板、编译器、审计与测试规范可以细化各自职责，但不得：

- 绕过本协议规定的证据链；
- 用下游产物无依据地改写上游证据；
- 将某个历史 Skill 的领域规则升级为全局规则；
- 以“更完整”或“更专业”为由增加无证据支持的视觉要求。

具体阶段的 Required Input、Required Output、Allowed Mutation、Forbidden Mutation 与 Exit Gate 由后续 Phase Contracts 定义；本文件不提前定义其细节。

## 3. Eight Core Principles

### Principle 1 — Audit References Before Building

禁止：

```text
References
→ Direct SKILL.md
```

Reference Set 必须先被完整审核。审核必须能够识别：

- Core References；
- Supporting References；
- Ambiguous References；
- Outliers。

审核的目的，是判断 Reference Set 的一致性、污染风险、潜在子类型、证据覆盖和进入分析阶段的准备度，而不是提前写视觉规则。

### Principle 2 — Evidence Weighting

不同 Reference、不同观察结果不得默认等权。

Builder 必须保留两类权重判断：

- Reference role：`Core / Supporting / Ambiguous / Outlier`；
- Observed frequency：`Dominant / Common / Occasional / Rare / Single-instance`，或功能等价的等级。

权重用于防止偶然特征、离群方向或单例内容被误写为核心视觉身份。本协议不规定具体统计算法，也不允许伪造精确度。

### Principle 3 — No Unsupported Style Invention

Builder 必须区分：

1. Reference-supported evidence；
2. Reasonable inference；
3. External knowledge。

正式视觉系统应优先且可验证地来自 Reference Evidence。合理推断必须标明其性质；外部知识不得替代 Reference Evidence 决定目标风格。

当证据不足时，`Insufficient Evidence` 是合法且优先于补写的结论。不得为了让 Skill 看起来完整而自动发明视觉规则、参数、词汇或反模式。

### Principle 4 — Separate Visual Roles

后续视觉系统必须区分：

- **Invariant**：丢失后会明显改变视觉身份的稳定核心；
- **Allowed Variation**：可变化但仍属于同一 Visual Family 的范围；
- **Incidental Detail**：个别内容或偶发表现，不得升级为核心规则；
- **Anti-pattern**：会造成职责或风格漂移的已证实方向。

风格稳定不等于固定模板。Builder 必须同时保护核心一致性与合法变化，避免把 `MAY` 写成 `MUST`，也避免把单例写成 Invariant。

### Principle 5 — Separate Analysis from Execution

必须保留：

```text
Reference Analysis
↓
Visual System Specification
```

Reference Analysis 描述可信 References 实际呈现的视觉语言；Visual System Specification 决定未来生成时如何复现、如何表达以及如何判断该视觉语言。

描述性观察不得直接当作命令式生成规则。转换时必须显式处理规则强度、适用范围、允许变化和质量判据。

### Principle 6 — SKILL.md Is the Execution Layer

最终 `SKILL.md` 必须是完整视觉系统的 **compressed execution layer**。

它应保留运行时必要的：

- 核心视觉身份与不变量；
- 生成与 Prompt 构建逻辑；
- 允许变化与风格保护；
- 最小质量检查与修订指引。

它不得成为 Reference 报告、视觉分析百科、System 文件全文拼接、大型 Prompt Library 或完整知识库。压缩不能造成关键规则丢失、含义失真或执行性不足。

### Principle 7 — Independent Static Audit

`SKILL.md` 编译完成后不得默认正确，必须接受独立 Static Audit。至少检查：

- **Missing**：上游重要规则缺失；
- **Distorted**：规则被弱化、写死或改变含义；
- **Unsupported**：加入了无上游依据的内容；
- **Redundant**：重复、膨胀或非执行性内容。

审计还必须关注职责漂移、Allowed Variation 模板化、过度压缩、过度工程化与内部冲突。审计修正默认落在 `SKILL.md`，不得借机重写已经成立的上游视觉系统。

### Principle 8 — Real Generation Validation

文档逻辑成立不等于 Skill 已成立。最终必须经过：

```text
Test
→ Diagnose
→ Minimal Fix
→ Retest
→ Regression
→ Freeze
```

测试目标是跨主体与合法变化的 **visual-family consistency**，不是复制某张 Reference，也不是追求每次生成绝对完美。

测试必须能够区分 Prompt Failure、Skill Failure、System Rule Failure、模型随机性和特定输入难度。只有受测试证据支持的修订才可以进入正式规则。

## 4. Reference-first Protocol

> References are the primary visual source of truth.

Skill Brief 只负责定义：

- what the Skill does；
- what it covers；
- what it does not cover。

Skill Brief 和其他上下文不能替 References 决定：

- composition；
- lighting；
- color；
- materiality；
- texture；
- emotional character；
- visual grammar；
- anti-pattern；
- style vocabulary。

如果 Brief 含有视觉预设，Builder 应将其视为待验证上下文，而不是既定视觉规则。只有当 References 提供支持时，它才可以进入正式视觉系统；若不支持，应记录冲突或证据不足，不得自动升级。

Reference-first 不等于机械复制 Reference。Builder 的目标是发现跨有效 References 稳定存在的视觉家族，并保留 Reference 支持的变化，而不是固定构图、具体主体或单张图片细节。

## 5. Global Evidence Hierarchy

正式证据链为：

```text
Reference Evidence
↓
Reference Audit
↓
Reference Analysis
↓
Visual System Rules
↓
Compiled SKILL.md
↓
Generation Test Evidence
```

各层职责如下：

| Layer | Responsibility | May not do |
|---|---|---|
| Reference Evidence | 提供原始视觉事实 | 被下游文件无证据改写 |
| Reference Audit | 决定证据可靠性、权重、污染与准备度 | 提前完成完整视觉分析或生成规则 |
| Reference Analysis | 描述可信证据中的视觉身份、变化、偶发细节与边界 | 直接充当执行 Prompt |
| Visual System Rules | 将分析转换为可执行、可表达、可评估的规则 | 发明分析中不存在的视觉身份 |
| Compiled `SKILL.md` | 压缩上游系统为运行时执行层 | 取代上游证据或扩大职责范围 |
| Generation Test Evidence | 验证真实执行表现并暴露失败模式 | 因单次失败随意重写 References 或发明新风格 |

上游决定视觉来源，下游负责解释、编译与验证。下游不得仅凭自身更晚生成，就被视为比上游证据更正确。

真实 Test Evidence 可以证明：

- Skill 编译发生失真或遗漏；
- Prompt Rule 有歧义或强度不当；
- Visual Rule 难以执行；
- Quality Rule 无法稳定判断；
- 某类失败只是模型随机性或输入特定风险。

测试失败触发诊断，不自动授权修改视觉身份。任何修订仍须沿证据链定位根因。

## 6. Source-of-Truth and Conflict Resolution

发生冲突时，先判断冲突属于 `Missing / Distortion / Unsupported Addition / Compression Loss` 中的哪一类，再决定责任层。不得默认修改最上游文件。

| Conflict | Default handling |
|---|---|
| Brief vs References | Brief 的视觉预设降级为待验证上下文；回到 References 判断。任务职责若本身冲突，则暂停升级视觉规则并明确记录。 |
| Audit vs Raw References | 复核 Audit 的分类、覆盖和证据引用；Raw References 保持原始事实地位。 |
| Analysis vs References | 将 Analysis 视为可能遗漏、失真或无依据扩展，修正分析解释，而非迁就它改写 References。 |
| Rules vs Analysis | 检查规则是否遗漏、写死、弱化或增加了分析未支持的内容；优先修正规则。 |
| `SKILL.md` vs System Rules | 默认视为编译问题；优先修正 `SKILL.md`。 |
| Test Result vs `SKILL.md` | 先区分系统性失败、单次随机性与输入特定难度，再定位 Prompt、Skill 或上游规则；不得从单次结果反推新风格。 |

只有明确证据证明上游层自身存在事实错误或不可执行歧义时，才允许把修订上移；该修订仍需记录依据并接受下游回归检查。

## 7. No Unsupported Expansion

任何阶段不得因为以下理由自动加入视觉规则：

- “这样更专业”；
- “通常这个风格应该这样”；
- “这样会更好看”；
- “完整系统一般都需要”；
- “模型通常喜欢这种表达”。

新增正式规则必须有明确证据来源，并与其证据强度相匹配。无法建立支持关系时，应删除、降级为待验证假设，或标记 `Insufficient Evidence`。

外部知识可以帮助命名、解释或发现需要检查的问题，但不能在缺少 Reference 支持时成为目标视觉系统的事实来源。

## 8. Phase Isolation

Build Phase 不得随意跳跃。至少禁止：

```text
Reference Set → SKILL.md
Reference Analysis → Test
Build Skill v1 → Freeze
```

每个阶段只能消费已通过上一阶段检查的正式输入，只能修改其被授权负责的产物，并必须在相应 Exit Gate 通过后才能推进。

阶段隔离的目的，是让错误能够定位到最近责任层，并防止后续产物反向污染证据。具体阶段数量、输入输出、Allowed Mutation 与 Exit Gate 细节由后续 Phase Contracts 定义。

## 9. Minimal Revision Principle

Audit 或 Test 发现问题时，遵循：

```text
Evidence
→ Root Cause
→ Closest Responsible Layer
→ Minimal Necessary Fix
→ Retest
→ Regression
```

修订必须：

1. 引用实际审计或测试证据；
2. 区分系统性失败与单次随机失败；
3. 优先修改离失败原因最近的层；
4. 只改变解决该问题所必需的规则；
5. 检查合法 Variation 是否被误伤；
6. 通过相关 Case、相邻风险 Case 与核心 Case 验证修复及回归。

禁止：

- 结果不好就大规模重写全部规则；
- 单次失败就修改 Reference-derived visual identity；
- 为一个 Case 加强限制，导致整个 Skill 固定模板化；
- 通过降低测试难度或无限重试掩盖系统性失败。

## 10. Domain-neutral Principle

全局 Builder 定义的是 **如何发现视觉规则**，不是 **视觉规则应该是什么**。

可以进入全局协议的，是两套 Validated V1 流程共享的构建机制，例如：

- Reference 全量审核与证据分组；
- 证据权重、频率与置信度判断；
- Invariant、Allowed Variation、Incidental Detail、Anti-pattern 的分离；
- 描述层到执行规格层的转换；
- Visual Rule、Prompt Rule、Quality Rule 的职责分离与相互映射；
- `SKILL.md` 的压缩编译；
- 独立静态审计；
- 真实生成、根因诊断、最小修订与回归；
- Visual Family 一致性优先于逐图复制。

以下内容属于目标 Image Skill 的 Domain-specific implementation detail，不得写死在 Global Builder Protocol 中：

- subject 或 artifact type；
- 构图、主体比例、留白或视角倾向；
- 材质、表面、老化、破损或使用痕迹；
- 光线、色彩、色调、景深或相机表达；
- typography risk 或具体文字边界；
- 情绪、氛围、真实性标准或特定视觉词汇；
- 任一具体领域专属的 anti-pattern；
- 任一领域专属的 Prompt vocabulary、失败类型或 QA 项。

Builder 可以要求目标 Skill 从 References 中发现并验证这些维度，但不能预先规定其答案。分析维度也应允许根据证据适配，而不是让所有 Image Skill 被迫使用同一套领域清单。

## 11. Protocol Completion Standard

一个 Image Skill 只有在以下事实均成立时，才可被视为完成构建：

- 视觉来源来自经过审核的 Reference Evidence；
- 分析、规格与执行层保持职责分离；
- 核心规则与合法变化均被保留；
- `SKILL.md` 已通过独立静态审计；
- 真实生成已验证视觉家族一致性；
- 所有正式修订都有证据、根因与回归结果；
- Freeze 时不存在未解决的阻断性问题。

具体阶段的判定状态、严重度与 Exit Gate 由后续协议定义。
