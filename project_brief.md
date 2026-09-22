# build-image-skill — Project Brief

# 1. Project Overview

`build-image-skill` 是一个用于构建 AI 图片生成 Skill 的元 Skill。

它的目标不是直接生成某一种固定视觉风格，而是：

> 基于一组 Reference Images，通过结构化的审核、分析、规则提取、Skill 编译、静态审计、真实生成测试与回归检查，稳定构建出一个可执行、可维护、可验证的 Image Generation Skill。

可以将其理解为：

> **Reference-driven Image Skill Compiler**

其核心流程不是：

```
References
→ 直接生成 SKILL.md
```

而是：

```
Evidence
→ Understanding
→ Specification
→ Compilation
→ Verification
→ Validation
→ Freeze
```

---

# 2. Project Background

此前已经通过两套独立流程成功构建：

- `image-broll-document`
    
- `image-broll-object`
    

两套 Skill 均使用 6 个阶段性 Prompt 完成构建。

虽然两套 Prompt 在具体视觉内容上有所差异，但整体架构高度相似，并且在实际图片生成中表现出较高的视觉复现率与风格稳定性。

因此，本项目不再继续为每个 Image Skill 单独手工编写一整套 6 Prompt。

新的目标是：

> 从已经验证有效的两套 V1 构建流程中，提取稳定、通用、可复用的构建机制，并将其封装为一个统一的 `build-image-skill`。

未来创建新的 Image Skill 时，主要变化的应当是：

```
Reference Set
+
Skill Brief
```

而不是重新设计整套 Skill 构建方法。

---

# 3. Core Objective

`build-image-skill` 最终应能够：

1. 接收一个新的 Image Skill 构建任务；
    
2. 读取目标 Skill 的 References；
    
3. 审核 Reference Set 是否可靠；
    
4. 提取真正共享的视觉语言；
    
5. 区分核心规则、允许变化和异常方向；
    
6. 将视觉分析转换为可执行的视觉系统；
    
7. 将视觉系统压缩为最终 `SKILL.md`；
    
8. 对 `SKILL.md` 进行独立一致性审计；
    
9. 通过真实生成测试验证 Skill；
    
10. 根据测试证据进行最小必要修正；
    
11. 执行 Regression Check；
    
12. 达到标准后 Freeze 目标 Skill。
    

最终目标不是：

> 偶尔生成一张与 Reference 相似的图片。

而是：

> 在不同主体、内容和合法视觉变化下，仍然能够稳定生成属于同一 Visual Family 的图片。

---

# 4. What build-image-skill Is

`build-image-skill` 是：

- Image Skill Builder；
    
- Reference-driven visual system builder；
    
- Visual rule compiler；
    
- Skill compiler；
    
- Skill audit system；
    
- Image Skill testing and refinement system；
    
- 多阶段构建 Orchestrator。
    

它负责的是：

> **如何根据 References 构建一个可靠的 Image Generation Skill。**

---

# 5. What build-image-skill Is Not

`build-image-skill` 不负责：

- 决定什么时候应该调用某个目标 Image Skill；
    
- 设计 Asset Agent 的路由；
    
- 设计 Visual Director 的语义决策；
    
- 决定视频中什么时候使用 B-roll；
    
- 定义 Camera Motion；
    
- 定义 LUT；
    
- 定义 Transition；
    
- 定义视频节奏；
    
- 定义 B-roll 时长；
    
- 自动决定内容选题；
    
- 替目标 Skill 发明视觉风格；
    
- 用外部审美常识覆盖 References；
    
- 把不同 Image Skill 强制统一成一种视觉体系；
    
- 将 Reference 图片直接复制成固定模板。
    

`build-image-skill` 只负责：

> 当系统已经决定要构建一个 Image Generation Skill 时，如何从 References 中建立一个稳定的视觉生成系统。

---

# 6. Source of Truth

整个 Builder 必须遵循：

> **References are the primary visual source of truth.**

Skill Brief 可以说明：

- Skill 是做什么的；
    
- 负责什么视觉对象；
    
- 有什么职责边界。
    

但 Skill Brief 不应该提前完整定义：

- 构图；
    
- 色彩；
    
- 光线；
    
- 材质；
    
- 情绪；
    
- 风格标签；
    
- 视觉规则。
    

这些应主要由 References 决定。

如果 Brief 与 References 在视觉语言上发生冲突：

> 应优先回到 References 检查，而不是强行让 References 服从预设风格。

---

# 7. Required Input

未来每一次调用 `build-image-skill`，最低应提供：

```
skill_name
purpose
references_path
scope_boundary
optional_context
```

### skill_name

目标 Image Skill 的名称。

### purpose

说明该 Skill 负责生成什么类型的视觉对象或图片。

这里只定义：

> 做什么。

不提前完整定义：

> 长什么样。

### references_path

目标 Skill 的 Reference Images 所在位置。

这是视觉语言最主要的证据来源。

### scope_boundary

说明目标 Skill 不负责什么，防止职责漂移。

### optional_context

可选补充信息。

只能帮助理解目标任务，不能覆盖 Reference Evidence。

正式 Input Contract 将在后续单独定义。

---

# 8. Expected Output

`build-image-skill` 最终应构建出一个完整的 Image Skill 项目。

至少包括：

```
Reference Audit
Reference Analysis
Visual Rules
Prompt Rules
Quality Rules
Traceability
SKILL.md
Skill Audit
Test Suite
Test Results
Refinement History
Final Test Report
```

具体文件结构由后续 System Protocol 与 Templates 正式确定。

最终结果必须是：

> 一个经过证据分析、规则编译、静态审计和真实测试验证的 Image Generation Skill。

---

# 9. Eight Core Principles

以下 8 条原则来自已成功运行的 V1 构建流程，是 `build-image-skill` 必须保留的核心机制。

它们不得因为通用化或简化而被删除。

---

## Principle 1 — Audit References Before Building

禁止：

```
References
→ SKILL.md
```

必须先审核 Reference Set。

需要识别：

```
Core References
Supporting References
Ambiguous References
Outliers
```

并判断：

- Reference Set 是否属于同一视觉家族；
    
- 是否存在污染；
    
- 是否存在多个子风格；
    
- 是否足够支持下一阶段分析。
    

---

## Principle 2 — Use Evidence Weighting

不同 References 和不同视觉特征不能默认等权。

需要能够区分：

```
Core
Supporting
Ambiguous
Outlier
```

以及：

```
Dominant
Common
Occasional
Rare
Single-instance
```

避免把偶然特征误写成核心风格规则。

---

## Principle 3 — Do Not Invent Unsupported Style

Builder 必须区分：

```
Reference-supported evidence
Reasonable inference
External knowledge
```

正式视觉规则必须优先来自 Reference Evidence。

如果证据不足，应明确记录：

```
Insufficient Evidence
```

不能为了让 Skill 看起来更完整而自行补写风格规则。

---

## Principle 4 — Separate Invariant, Variation, Incidental and Anti-pattern

每个目标 Image Skill 必须区分：

```
Invariant
Allowed Variation
Incidental Detail
Anti-pattern
```

也就是说必须回答：

```
什么必须大体保持？
什么可以变化？
什么只是偶发内容？
什么方向会造成 Style Drift？
```

风格稳定不能依赖固定模板。

---

## Principle 5 — Separate Analysis from Execution Specification

必须存在：

```
Reference Analysis
↓
Visual System Specification
```

Reference Analysis 回答：

> 这些 References 到底呈现了什么视觉语言？

Visual System Specification 回答：

> 未来生成图片时，应该如何稳定复现这种视觉语言？

描述性结论不能直接等同于执行规则。

---

## Principle 6 — Keep SKILL.md as the Execution Layer

最终 `SKILL.md` 必须是：

> 紧凑、清晰、可执行的执行协议。

它不能成为：

- Reference Analysis 全文；
    
- Visual System 文件拼接；
    
- 视觉理论文章；
    
- 巨型 Prompt 集合；
    
- 完整知识库。
    

Detailed Knowledge 应留在 System 文件中。

`SKILL.md` 只保留运行时真正必要的执行逻辑。

---

## Principle 7 — Audit the Compiled Skill Independently

`SKILL.md` 生成后不能默认正确。

必须进行独立 Static Audit。

至少检查：

```
Missing
Distorted
Unsupported
Redundant
```

同时检查：

- Core Invariant 是否丢失；
    
- Allowed Variation 是否被写死；
    
- 是否加入无 Reference 支持的新规则；
    
- 是否出现职责漂移；
    
- 是否压缩过度；
    
- 是否过度膨胀。
    

---

## Principle 8 — Validate Through Real Generation and Regression

Skill 必须经过真实生成测试。

正式流程：

```
Test
→ Diagnose
→ Minimal Fix
→ Retest
→ Regression
→ Freeze
```

测试目标不是：

> exact reference copying

而是：

> visual-family consistency。

同时必须避免为了修复某个失败而破坏合法 Variation。

---

# 10. V1 Problems to Solve

`build-image-skill` 不只是把原来两套 6 Prompt 合并。

它必须解决以下 V1 问题。

---

## V1 Problem 1 — Repeated Instructions Across Prompts

原 6 Prompt 中存在大量重复规则，例如：

- 不要跳阶段；
    
- 不要发明风格；
    
- 不要修改 References；
    
- 不要提前写下一阶段文件；
    
- 不要加入 Usage Contract；
    
- 不要让职责漂移。
    

### V2 Direction

抽象成：

```
Global Builder Protocol
+
Phase Contracts
```

Global Protocol 只定义一次全局规则。

每个 Phase 只定义自己的：

```
Required Input
Responsibility
Required Output
Allowed Mutation
Forbidden Mutation
Exit Gate
```

---

## V1 Problem 2 — Strong Coupling to Specific Image Skill Domains

原 Prompt 会包含大量领域特定内容。

例如不同 Skill 可能拥有完全不同的：

- visual subject；
    
- material；
    
- anti-pattern；
    
- composition risk；
    
- typography risk；
    
- realism problem。
    

### V2 Direction

`build-image-skill` 必须保持 Domain-neutral。

Builder 应知道：

> 如何发现 Anti-pattern。

而不是预先知道：

> Anti-pattern 是什么。

具体视觉规则必须由目标 References 产生。

---

## V1 Problem 3 — Overly Dense Fixed Analysis Dimensions

原 Reference Analysis 包含大量固定分析章节。

这能够减少遗漏，但会导致不同 Image Skill 被迫使用同一分析框架。

### V2 Direction

建立：

```
Core Dimensions
+
Adaptive Dimensions
```

Core Dimensions 是通用视觉基础。

Adaptive Dimensions 根据 Reference Evidence 自动产生。

只有满足一定 Evidence Threshold 的视觉特征才能升级成正式分析维度。

---

## V1 Problem 4 — Lack of Formal Traceability

原流程虽然存在：

```
Reference
→ Analysis
→ Rules
→ Skill
→ Test
```

但这种关系主要依赖自然语言理解。

### V2 Direction

建立正式 Traceability：

```
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

目标是：

> 每一条核心执行规则，都可以追溯到 Reference Evidence。

---

# 11. Six-Phase Build Architecture

`build-image-skill` 必须保留以下六个正式阶段。

---

## Phase 1A — Reference Set Audit

回答：

> 当前 References 是否可靠？

主要负责：

- Reference consistency；
    
- Reference weighting；
    
- Core / Supporting / Ambiguous / Outlier；
    
- contamination risk；
    
- subtype check；
    
- readiness check。
    

---

## Phase 1B — Reference Analysis

回答：

> 这组有效 References 的视觉语言到底是什么？

主要负责：

- Core Visual Identity；
    
- Core Dimensions；
    
- Adaptive Dimensions；
    
- recurring patterns；
    
- invariants；
    
- allowed variation；
    
- incidental details；
    
- anti-patterns；
    
- evidence confidence。
    

---

## Phase 2 — Visual System Specification

回答：

> 如何把视觉分析转换成可执行系统？

主要产生：

```
visual_rules
prompt_rules
quality_rules
```

---

## Phase 3A — Build Skill v1

回答：

> 如何把完整视觉系统压缩成运行时可执行的 SKILL.md？

主要完成：

```
System
↓
Execution Layer
```

---

## Phase 3B — Skill Consistency Audit

回答：

> SKILL.md 是否正确编译了上游视觉系统？

主要检查：

- Missing；
    
- Distorted；
    
- Unsupported；
    
- Redundant；
    
- Traceability integrity；
    
- Rule strength；
    
- Scope；
    
- Overengineering；
    
- Under-specification。
    

---

## Phase 4 — Test + Refine + Freeze

回答：

> 这个 Skill 在真实图片生成中是否稳定成立？

流程：

```
Test
→ Diagnose
→ Minimal Fix
→ Retest
→ Regression
→ Freeze
```

---

# 12. Traceability Direction

V2 必须建立统一 ID 系统。

预期包括：

```
REF   Reference
OBS   Observation
INV   Invariant
VAR   Allowed Variation
ANTI  Anti-pattern
VR    Visual Rule
PR    Prompt Rule
QR    Quality Rule
SK    Skill Rule
TC    Test Case
```

正式 Traceability Specification 将在后续阶段设计。

本 Project Brief 只确定：

> Traceability 是 `build-image-skill` 的核心架构要求，而不是可选功能。

---

# 13. Testing Philosophy

测试系统必须同时验证：

```
Consistency
Variation
Robustness
Boundary
Recoverability
```

目标不是让所有 Case 100% 单次成功。

而是确保：

- Core Case 稳定；
    
- Allowed Variation 不被模板锁死；
    
- Anti-pattern 不反复污染输出；
    
- Boundary 可控；
    
- Failure Pattern 可识别；
    
- 修复不会产生明显 Regression。
    

---

# 14. Historical Validation Strategy

`build-image-skill` 构建完成后，不能直接认为 Builder 成功。

必须使用两个已经验证成功的历史 Skill 进行 Backtest：

```
image-broll-document
image-broll-object
```

执行原则：

> 不再使用原来的 6 Prompt 作为执行指令。

而是：

```
Original References / Inputs
+
new build-image-skill
```

重新构建。

旧 Prompt 和旧 Skill 只作为：

```
Historical Benchmark
```

最终验证：

- 新 Builder 是否保持原有高复现率；
    
- 是否出现 V1 → V2 Regression；
    
- 是否真正 Domain-neutral；
    
- Adaptive Dimensions 是否能够针对不同 Skill 自适应；
    
- Traceability 是否实际可用；
    
- Test / Refinement / Regression 是否跑通。
    

---

# 15. Reference Implementation Role

项目中的：

```
Reference_Implementation/
```

保存：

```
image-broll-document — 6 historical prompts
image-broll-object   — 6 historical prompts
```

它们的定位是：

> **Validated V1 Reference Implementation**

建设 `build-image-skill` 时：

> 用于抽取成功机制。

Builder 完成后：

> 用于 Regression Benchmark。

未来日常运行 `build-image-skill` 时：

> 不应依赖这些旧 Prompt。

---

# 16. Success Criteria

`build-image-skill v1` 只有在满足以下条件后才能 Freeze：

### Architecture

- 六阶段完整；
    
- Global Protocol 清晰；
    
- Input Contract 清晰；
    
- Phase Contract 清晰；
    
- System / Templates / SKILL 职责分离。
    

### Reproduction

- `image-broll-document` Historical Backtest 通过；
    
- `image-broll-object` Historical Backtest 通过；
    
- 新 Builder 没有明显降低视觉复现率。
    

### Generalization

- 没有写死 document 或 object 的具体视觉规则；
    
- Core Dimensions 足够通用；
    
- Adaptive Dimensions 能根据 References 动态产生；
    
- Anti-pattern 来自目标 Reference，而不是 Builder 预设。
    

### Traceability

核心规则能够沿：

```
REF
→ OBS
→ INV / VAR / ANTI
→ VR
→ PR / QR
→ SK
→ TC
```

完成追踪。

### Audit

无未解决的 Critical / Major Compiler Issue。

### Testing

真实运行：

```
Test
→ Diagnose
→ Minimal Fix
→ Retest
→ Regression
→ Freeze
```

能够成立。

---

# 17. Final Design Principle

`build-image-skill` 最重要的原则是：

> **通用的是“如何发现、编译和验证视觉规则的方法”，而不是“视觉规则本身”。**

Builder 不应该知道某一种风格应该是什么样。

Builder 应该知道：

> 如何从可靠 References 中发现目标视觉系统，并把它稳定编译成一个可以执行、可以审计、可以测试、可以维护的 Image Skill。