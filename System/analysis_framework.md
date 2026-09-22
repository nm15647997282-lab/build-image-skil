# build-image-skill — Adaptive Reference Analysis Framework

## 1. Purpose

本文件定义 `Phase 1B — Reference Analysis` 的通用分析方法。

目标是在不同 Image Skill 之间复用同一套分析逻辑，同时避免把所有 Skill 强制装入同一组密集、领域耦合的固定章节。Framework 采用：

```text
Layer 1 — Core Dimensions
+
Layer 2 — Adaptive Dimensions
↓
Cross-dimensional Synthesis
```

Core Dimensions 提供最小但完整的视觉结构检查；Adaptive Dimensions 只在当前 Reference Set 有充分证据时产生。两层分析最终共同形成 Core Visual Identity、Invariant、Allowed Variation、Incidental Detail、Anti-pattern、Subtype 与 Evidence Confidence。

本文件只服务 Reference Analysis。它不创建执行规则、Traceability ID、`SKILL.md`、Audit Rubric 或 Test Cases。

## 2. Analysis Philosophy

### 2.1 Reference-first

Reference Analysis 的视觉结论必须来自 Phase 1A 已审核的 Reference Evidence。

Target Skill Brief 中的 `purpose`、`scope_boundary` 与 `optional_context` 可以帮助理解任务和职责边界，但不是视觉证据。Brief 中的视觉预设只有在 References 支持时才可成为分析结论；否则应记录为未获支持的上下文或冲突。

### 2.2 Weighted Evidence

Phase 1B 必须继承 Phase 1A 的：

- `Core References`；
- `Supporting References`；
- `Ambiguous References`；
- `Outliers`。

不得在 Phase 1B 中把所有 References 重新视为等权。Reference role、观察频率、重要性与置信度是不同概念，必须分别判断。

### 2.3 Describe Before Specifying

Reference Analysis 回答：

- what is observed；
- what appears stable；
- what may vary；
- what appears incidental；
- what appears incompatible。

它不回答未来生成时“必须怎么做”。`MUST / SHOULD / MAY / AVOID / DO NOT` 等命令式规则属于 Phase 2。

### 2.4 Evidence Sufficiency over Completeness

分析不以填满章节为目标。没有证据时，`Insufficient Evidence` 优于推测；没有独立分析价值的维度可以简短记录，而不能为了显得完整而硬写结论。

## 3. Core + Adaptive Architecture

### 3.1 Layer 1 — Core Dimensions

Core Dimensions 是所有 Image Skill 原则上都应检查的基础视觉结构。它们：

- domain-neutral；
- 不预设视觉答案；
- 数量有限；
- 足以支持整体视觉身份判断；
- 可以在证据很弱时输出 `Insufficient Evidence`；
- 可以由 Adaptive Dimension 进一步细化，但不会被另一套分析系统取代。

### 3.2 Layer 2 — Adaptive Dimensions

Adaptive Dimensions 是从当前 Reference Set 中发现的、值得单独分析的领域特定维度。它们：

- 必须 evidence-driven；
- 必须影响视觉身份、变化边界、生成稳定性或质量判断；
- 不构成预置清单；
- 不能由单张图片中的特殊细节自动触发；
- 必须通过 Promotion Threshold。

### 3.3 Cross-dimensional Synthesis

以下内容不是固定视觉维度，而是 Core 与 Adaptive 分析完成后的综合结果：

- Recurring Visual Patterns；
- Invariants；
- Allowed Variations；
- Incidental Details；
- Anti-patterns；
- Subtype Analysis；
- Core Visual Identity；
- Evidence Confidence；
- Phase 2 Readiness。

把这些结果分类误写成视觉维度，会造成重复分析和结构膨胀。

## 4. Core Dimension Contract

每个 Core Dimension 都使用以下五项分析要求：

### What to inspect

当前维度需要观察哪些视觉关系、稳定模式、变化与矛盾。

### Why it matters

该维度如何帮助区分视觉身份、合法变化与风格漂移。

### What counts as evidence

哪些可见、可比较、可定位到有效 References 的事实能够支持结论。

### What not to infer

哪些内容不能从当前观察自动推导，尤其是具体参数、风格标签、因果解释或命令式规则。

### Possible outputs

该维度可能产生的描述性结论类型，而不是预设答案。

Core Dimension 不要求每次产生强结论。简短的低置信度结论或 `Insufficient Evidence` 都是有效输出。

## 5. Core Dimensions

最终采用九个 Core Dimensions。它们由两套 V1 中重复出现的基础结构合并而来；具体领域现象不进入 Core。

### 5.1 Subject / Visual Object Treatment

**What to inspect**

- 主要视觉对象是什么，以及是否能被稳定识别；
- 单一主体、组合主体与辅助元素之间的层级；
- 主体被如何观看、呈现、裁切或强调；
- 内容差异与呈现方式差异是否被正确区分；
- 主体状态是否形成重复模式或合法变化。

**Why it matters**

主体处理决定画面的注意力中心与基本观看方式，也是区分“subject 变化”与“visual language 变化”的第一步。

**What counts as evidence**

- 多个有效 References 中可比较的主体层级、数量、清晰度与呈现关系；
- Core 与 Supporting References 之间稳定或有结构的差异；
- Outlier 中与核心呈现方式明显冲突的处理。

**What not to infer**

- 不把某个具体 subject 自动定义为风格；
- 不因主体类别推断未经观察的构图、光线或情绪；
- 不把 Brief 中列举的对象当成视觉规律。

**Possible outputs**

- 主体层级与呈现方式的稳定描述；
- 主体数量或状态的 Allowed Variation 候选；
- 主体处理上的 Incidental Detail、Subtype 或 Anti-pattern 候选。

### 5.2 Composition & Frame Relationship

**What to inspect**

- 元素在画面中的位置、平衡、方向、裁切与边缘关系；
- 主体相对画框的视觉尺度与权重；
- 正负空间如何分布；
- 视觉密度与元素数量如何组织；
- 构图是否稳定、存在变化结构或呈现模板锁定。

**Why it matters**

构图与画框关系决定画面的整体视觉结构。把尺度、留空与密度放在同一 Core Dimension 中，可以避免为每种布局现象建立重复章节。

**What counts as evidence**

- 多个有效 References 中重复的 placement、balance、crop、scale、spacing 与 density；
- 同一视觉家族内稳定的构图变化范围；
- Core 与 Outlier 在画面组织上的可见差异。

**What not to infer**

- 不从单张图推断固定位置、固定比例或固定留空；
- 不把“平衡”“高级”“自然”等评价词当作观察证据；
- 不伪造精确百分比或几何参数。

**Possible outputs**

- 主导构图关系与画框尺度的描述；
- 密度、裁切、位置或留空的变化范围；
- 构图模板化、失衡或过度复杂等边界候选。

### 5.3 Spatial Context & Element Relationships

**What to inspect**

- 主体、辅助元素、背景与环境之间的空间关系；
- 元素是否接触、遮挡、重叠、分离或形成层级；
- 环境是提供语义、支撑、深度还是仅充当背景；
- 比例、重力、方向和相互作用是否可信；
- 多元素安排是否存在稳定结构。

**Why it matters**

空间关系决定对象是否属于同一场景、是否具有可信上下文，以及视觉系统如何处理多元素而不发生职责或风格漂移。

**What counts as evidence**

- 有效 References 中重复的接触、距离、遮挡、层级和环境关系；
- 背景复杂度与主体分离方式的跨图一致性；
- 相同关系在不同主体或场景中的稳定复现。

**What not to infer**

- 不把某个具体环境自动设为默认；
- 不从空间关系推断未经观察的叙事含义；
- 不把一个特殊道具或交互升级为通用结构。

**Possible outputs**

- 空间组织、背景作用和元素关系的稳定描述；
- 上下文或交互方式的 Variation / Subtype 候选；
- 不可信空间、无关环境或关系冲突等 Anti-pattern 候选。

### 5.4 Lighting & Shadow Structure

**What to inspect**

- 光线的方向性、软硬、分布与强弱关系；
- 高光、阴影、反差与可见光源线索；
- 光线如何影响主体层级、空间、表面与情绪感知；
- 是否存在稳定光线体系或有结构的变化。

**Why it matters**

Lighting 不只影响亮度，也影响体积、材质、真实感和感知气质，是跨领域稳定存在的视觉维度。

**What counts as evidence**

- 多张有效 References 中可观察的阴影边缘、明暗方向、高光响应与曝光关系；
- Core / Supporting References 之间重复的照明特征；
- 与 Outlier 或污染方向形成稳定对比的光线处理。

**What not to infer**

- 不推断镜头、灯具、布光图、精确角度、色温或曝光参数；
- 不用风格标签代替可见的光影证据；
- 不因单张高反差图片推断整体光线体系。

**Possible outputs**

- 光线与阴影结构的稳定描述；
- 方向、软硬或反差的 Variation 候选；
- 与核心身份冲突的照明方向候选。

### 5.5 Color, Contrast & Tonality

**What to inspect**

- 色相关系、饱和度、冷暖与中性色倾向；
- 明暗范围、黑白关系、对比度与局部色彩强调；
- 色彩来自主体、环境、光线还是整体处理；
- 是否存在固定 palette，还是只有更宽泛的 tonal character。

**Why it matters**

色彩和色调影响视觉统一、主体分离与情绪感知，但也最容易因 Reference 内容偏向而被误写成固定色值。

**What counts as evidence**

- 多个高权重 References 中重复的色彩关系与 tonal behavior；
- 不同 subject 下仍保持的色调特征；
- 支持合法色彩变化的 Supporting References；
- 与污染方向形成清楚对比的色调处理。

**What not to infer**

- 不从单张图片提取固定 palette；
- 不伪造色值、色温或后期参数；
- 不把 subject 自带颜色误当成全局视觉规则。

**Possible outputs**

- 稳定 tonal character；
- palette 是否固定的证据判断；
- 色彩与对比的 Allowed Variation、Incidental Detail 或 Anti-pattern 候选。

### 5.6 Surface, Texture & Material Response

**What to inspect**

- 表面是否呈现可辨识的纹理、光泽、粗糙度与边缘特征；
- 不同材料在光线、接触和细节上的可见响应；
- 表面状态是否稳定、变化或具有可信物理逻辑；
- 材质表现是否与整体真实—风格化程度一致。

**Why it matters**

材质响应决定视觉对象是否具有可信表面与物理存在感，同时为领域特定的表面现象提供统一上位入口。

**What counts as evidence**

- 有效 References 中重复的表面细节、边缘、光泽、纹理与接触表现；
- 多种材料之间保持一致的呈现逻辑；
- Core 与 Outlier 在材质可信度或表面处理上的差异。

**What not to infer**

- 不假设某一种材料、纹理或表面状态必然存在；
- 不从单例推导完整的材质系统；
- 不自动加入未观察到的技术细节或物理参数。

**Possible outputs**

- 通用材质响应和表面表现的描述；
- 需要进一步拆分的 Adaptive Dimension 候选；
- 材质变化范围、偶发表面细节或不可信表现候选。

### 5.7 Depth, Focus & Image-space Separation

**What to inspect**

- 主体与其他平面的清晰度关系；
- 景深、焦点分布、前后层次与背景分离；
- 清晰或模糊如何服务主体层级、环境可读性与空间感；
- 是否存在稳定的 image-space separation 方式。

**Why it matters**

Depth 与 Focus 影响主体识别、空间关系和整体观看方式，且不能被简单等同于某种镜头或摄影参数。

**What counts as evidence**

- 多个有效 References 中可比较的焦点位置、清晰范围、层次与分离方式；
- 相同视觉身份下允许的深度变化；
- 极端模糊、过度分离或平面化与核心家族的对比。

**What not to infer**

- 不推断焦段、光圈、传感器或具体拍摄设置；
- 不把单次模糊或锐化当作稳定风格；
- 不因主体清晰就假设背景必须虚化。

**Possible outputs**

- 焦点与空间分离的稳定描述；
- Depth / Focus 的合法变化与边界；
- 影响主体识别或空间可信度的失败方向候选。

### 5.8 Realism, Stylization & Physical Plausibility

**What to inspect**

- 画面更接近观察性再现、受控风格化还是明显人工构造；
- 几何、比例、接触、重力、阴影与材料响应是否相互一致；
- 风格化发生在哪些层面，是否仍保持内部逻辑；
- 是否存在明显的生成痕迹、过度理想化或视觉伪影。

**Why it matters**

所有 Image Skill 都需要明确真实与风格化的相对位置，但 Framework 不能预设“越真实越好”。关键是 References 自身的稳定程度与内部一致性。

**What counts as evidence**

- Core References 中重复的真实感或风格化处理；
- 几何、光影、材料和空间线索之间的一致性；
- Outlier 与核心在人工感、理想化程度或物理逻辑上的差异。

**What not to infer**

- 不把个人审美偏好当作真实感标准；
- 不把任何媒介外观或生成痕迹预先判为优劣；
- 不因一个瑕疵推断整个视觉家族的风格化程度。

**Possible outputs**

- 真实—风格化位置与可信度要求的描述；
- 物理合理性与视觉伪影边界；
- 可能需要 Adaptive 分析的特定真实感机制。

### 5.9 Emotional & Perceptual Character

**What to inspect**

- 画面稳定产生的感知气质、观看距离、节奏与情绪倾向；
- 这些感受由哪些可见机制共同形成；
- 哪些感受跨多个有效 References 稳定存在，哪些只是 subject 内容造成；
- 情绪是否存在合法变化或与污染方向形成对比。

**Why it matters**

视觉身份不仅由形式属性构成，但情绪词最容易变成无证据的形容词堆叠。本维度要求把感知结论重新连接到可见机制。

**What counts as evidence**

- 多个高权重 References 中重复的构图、光线、色调、密度、空间和材质组合；
- 不同 subject 下仍然出现的相似感知结果；
- 与核心相反方向的可见视觉机制。

**What not to infer**

- 不把主题含义、故事设定或 Brief 的情绪词直接当作视觉证据；
- 不输出没有可见机制支持的形容词列表；
- 不假设情绪必然由单一颜色或光线造成。

**Possible outputs**

- 有机制支撑的 emotional / perceptual character；
- 合法气质变化与冲突方向；
- 情绪相关 Adaptive Dimension 或 Subtype 候选。

## 6. Adaptive Dimension Definition

> Adaptive Dimension 是当前 Reference Set 中证据足够强、对视觉身份或后续生成与判断足够重要，因而值得从 Core Dimension 中拆出并单独分析的领域特定视觉维度。

Adaptive Dimension 必须：

- 指向一个清楚、可观察的视觉现象或关系；
- 能说明其上位 Core Dimension；
- 有多个有效 References 或其他可核验的比较证据支持；
- 具有独立分析价值，而不是重复 Core Dimension；
- 能影响至少一类重要结果：Identity、Variation、Boundary、Generation Stability 或 Quality Evaluation；
- 明确其证据范围、矛盾和置信度。

不存在固定 Adaptive Dimension 清单。历史 Skill 中出现过的领域维度只可作为发现灵感，不能在新 Build 中默认启用。

## 7. Adaptive Dimension Detection

Builder 在 Core Dimension 分析过程中寻找以下信号：

### Signal A — Repetition

同一视觉属性或关系在多个 Core / Supporting References 中反复出现，并且不是单纯由重复 subject 造成。

### Signal B — Identity Importance

跨 Reference 比较表明，该属性的明显缺失或反转会改变视觉家族身份。该判断必须有多张有效 Reference 或边界对照支持，不能只凭直觉。

### Signal C — Differentiation

该属性能稳定区分 Core References 与 Outlier、污染方向或另一候选视觉家族。

### Signal D — Generation Stability

已有、可记录的生成证据表明，忽略该属性会导致重复失败。Phase 1B 不得假设模型未来会失败；没有既有证据时，此信号保持未证实。后续 Test Evidence 可以通过正式 Rollback 触发重新分析。

### Signal E — Variation Structure

该属性具有可重复辨认的 `default / allowed variation / boundary` 结构，而不是随机差异。

### Signal F — Quality Importance

如果不单独描述该属性，后续 Quality Rules 将无法判断一个关键视觉成功或失败。

检测到信号只会创建 **Adaptive Candidate**，不会自动完成 Promotion。

## 8. Adaptive Dimension Promotion Threshold

### 8.1 Mandatory Conditions

候选维度必须同时满足：

1. **Evidence anchored**：依据来自 Phase 1A 认可的有效 References，而不是 Brief、外部常识或模型偏好；
2. **Cross-reference support**：不能仅由一个 Single-instance 支撑；证据需跨多个有效 References，或具有可核验的核心—边界比较；
3. **Analytical distinctness**：单独分析能够揭示 Core Dimension 摘要无法清楚表达的结构；
4. **Material consequence**：它会影响视觉身份、合法变化、边界、生成稳定性或质量判断中的至少一项；
5. **Bounded scope**：能够说明它检查什么、不检查什么，以及与上位 Core Dimension 的关系；
6. **Contradiction handling**：相反或缺失证据已被考虑，不能只挑选支持样本。

### 8.2 Promotion Evidence

满足 Mandatory Conditions 后，还必须具备：

- 至少一个主要信号：`Repetition` 或有跨 Reference 证据支持的 `Identity Importance`；
- 至少一个后果信号：`Differentiation / Generation Stability / Variation Structure / Quality Importance`。

这是一项证据结构要求，不是固定图片数量或统计公式。Reference Set 的规模与 Phase 1A 权重仍需参与判断。

### 8.3 Promotion Decision

候选维度只能得到以下结果之一：

- **PROMOTE**：满足阈值，建立正式 Adaptive Dimension；
- **RETAIN AS OBSERVED DETAIL**：现象真实存在，但独立分析价值或证据强度不足；
- **INCIDENTAL DETAIL**：仅属于具体内容或偶发表现；
- **INSUFFICIENT EVIDENCE**：尚不能判断其结构或重要性。

Promotion 决定应简要记录支持信号、反证、上位 Core Dimension 与置信度，为后续 Traceability 保留结构基础，但本阶段不创建 ID。

## 9. Single-instance and Observed Detail Handling

如果某个特征：

- 只出现一次；
- 不影响整体 Core Visual Identity；
- 没有稳定 Variation / Boundary 结构；
- 没有经验证的生成或质量风险；

则默认不得成为 Adaptive Dimension。

Single-instance 可以：

- 作为 Observed Detail 被记录；
- 在证据不足时标记 `Insufficient Evidence`；
- 在 Outlier 中作为边界对照；
- 在未来新增 References 或 Test Evidence 后重新评估。

它不能单独支持 Invariant、Subtype 或完整领域系统。不得把一次出现的对象、标签、姿态、透视、材质或装饰扩写成独立分析体系。

Observed Detail 至少应保留：

- 可见事实；
- 出现于哪些有效 Reference 或 Reference role；
- Frequency；
- 当前 Importance；
- Confidence；
- 当前处理结论。

## 10. Core and Adaptive Relationship

Adaptive Dimension 不是与 Core Analysis 并列的第二套系统，而是对某一 Core Dimension 的：

- **补充**：加入该领域必须检查的特殊现象；
- **细化**：把过于宽泛但高重要性的现象独立分析；
- **拆分**：当一个 Core Dimension 内存在多个稳定、不同后果的子机制时分别处理。

每个 Adaptive Dimension 必须声明：

- Parent Core Dimension；
- Promotion Evidence；
- What to inspect；
- Why separate analysis is needed；
- Evidence scope；
- Known contradictions；
- Possible analytical outputs；
- Confidence。

Adaptive 分析完成后，其结论仍需与其他 Core Dimensions 一起进入跨维度综合，不能形成孤立的小型风格系统。

## 11. Recurring Pattern Analysis

Recurring Pattern 是跨一个或多个 Dimension 重复出现的视觉现象或关系。每个重要 Pattern 至少区分：

| Field | Meaning |
|---|---|
| Pattern | 对可见现象或关系的描述 |
| Dimension | 所属 Core / Adaptive Dimension |
| Evidence scope | 支持它的 Reference role 与范围 |
| Frequency | 出现频率 |
| Importance | 对视觉身份或边界的重要程度 |
| Confidence | 当前证据可靠度 |
| Contradiction | 相反、缺失或不一致证据 |
| Potential role | Invariant / Variation / Incidental / Anti-pattern candidate |

### 11.1 Frequency

可使用：

- **Dominant**：在高权重有效 References 中持续占主导；
- **Common**：在有意义的多个有效 References 中重复出现；
- **Occasional**：在少数但不止孤立的有效 References 中出现；
- **Rare**：证据有限，但仍可能代表合法边界或变化；
- **Single-instance**：只出现一次。

不得伪造精确百分比，除非 Reference Set 允许可靠统计且确有必要。

### 11.2 Importance

Importance 应独立判断，例如：

- **Identity-critical**；
- **Supporting**；
- **Boundary-relevant**；
- **Incidental**。

Frequency 不等于 Importance。Rare Pattern 可能是合法 Variation；Dominant Pattern 也可能只是 Reference Set 的内容偏向。

## 12. Analysis Result Roles

### 12.1 Invariant

Invariant 回答：

> 哪些属性如果明显缺失、反转或被替换，会改变这个 Visual Family 的身份？

成为 Invariant 的结论应：

- 有高权重、跨 Reference 的支持；
- 对身份具有明确重要性；
- 考虑反证与合法 Variation；
- 不由 Single-instance 单独支持；
- 保持描述性，不转写为命令。

High Frequency 本身不足以证明 Invariant，High Confidence 也不自动等于 Identity-critical。

### 12.2 Allowed Variation

Allowed Variation 回答：

> 哪些属性可以变化，但变化后仍属于同一 Visual Family？

每个重要 Variation 应说明：

- 变化的维度；
- References 支持的相对范围或类型；
- 变化时仍保持的视觉核心；
- 接近边界时可能出现的漂移；
- Evidence Confidence。

Variation 必须有 Reference 支持，不能为了“增加灵活性”无限扩展。

### 12.3 Incidental Detail

Incidental Detail 回答：

> 哪些只是具体 Reference 的内容、偶发条件或低重要性差异？

Incidental Detail 默认：

- 不进入 Core Visual Identity；
- 不成为 Invariant；
- 不建立 Adaptive Dimension；
- 不直接进入 Phase 2 Rules。

它可以保留为未来证据变化时的观察记录。

### 12.4 Anti-pattern

Anti-pattern 回答：

> 哪些视觉方向与目标 Visual Family 不兼容，并可能造成稳定 Style Drift？

Anti-pattern 必须来自：

- Core 与 Outlier 的可见对比；
- 已审核的 contamination evidence；
- Core Identity 的明确反方向；
- 多个有效 References 支持的边界；
- 已存在且可核验的稳定失败证据。

Builder 不得从外部风格常识预置 Anti-pattern。缺乏比较证据时，只能记录风险假设或 `Insufficient Evidence`。

### 12.5 Role Assignment Rules

- 同一观察可以参与多个更高层结论，但每个角色必须说明不同理由；
- 一个属性不能在相同范围内同时被标记为 Invariant 和自由 Variation；
- Invariant 可以包含一个稳定原则，而其具体表现具有 Allowed Variation；
- Anti-pattern 必须描述不兼容方向，而不是把所有非主导变化都判错；
- 角色结论必须保留其来源与 Confidence，为未来 Traceability 做准备。

## 13. Evidence Confidence

关键观察、Pattern、Adaptive Promotion、结果角色、Subtype 与 Core Visual Identity 均应标记 Confidence：

### High Confidence

- 得到多个 Core References 的一致支持；
- 覆盖充分，重复清楚；
- 重要矛盾很少或已得到解释；
- Supporting References 没有系统性反驳。

### Medium Confidence

- 有多个有效 References 支持，但覆盖有限；或
- Core 与 Supporting Evidence 基本一致，但存在可解释矛盾；或
- 结论稳定存在，但适用范围尚未完全确定。

### Low Confidence

- 支持主要来自有限或低权重 Evidence；或
- 存在明显矛盾；或
- 重要性、范围或机制仍不清楚。

### Insufficient Evidence

- 证据不足以形成可靠结论；
- 只能依赖 Single-instance；
- Reference classification 或可见事实无法支持该判断；
- 结论主要来自 Brief 或外部知识。

Confidence 应综合：

- Reference coverage；
- Phase 1A weighting；
- repetition；
- consistency；
- Core Reference support；
- contradiction；
- 可观察性。

不得使用伪精确分数。Confidence 不等同于 Frequency、Importance 或未来 Rule Strength。

## 14. Subtype Analysis

Subtype 是同一 Visual Family 内部具有稳定、成组差异的视觉分支，不是任意变化标签。

### 14.1 Subtype Candidate Signals

只有当多个有效 References 形成相对稳定的聚类，并在一个或多个重要维度上持续不同，才建立候选 Subtype。可检查：

- composition system；
- subject treatment；
- spatial relationship；
- lighting system；
- material treatment；
- emotional character；
- 已有证据支持的 generation behavior。

单一属性、轻微差异或一个 Reference 不足以形成 Subtype。

### 14.2 Subtype Decision

每个候选聚类必须判断为：

1. **Same visual family + Allowed Variation**：共享核心身份，差异未形成独立系统；
2. **Meaningful Subtype**：共享核心 Invariants，但存在稳定、成组且有生成意义的差异；
3. **Separate Skill Candidate**：Core Visual Identity 或必要规则发生根本冲突，合并会造成持续漂移；
4. **Insufficient Evidence**：聚类规模、稳定性或边界不足。

Subtype 分析应说明共享核心、差异维度、证据范围、边界与 Confidence。不得为了让分析更精细而过度拆分。

## 15. Core Visual Identity

Reference Analysis 最终必须用一段完整、非营销化的综合定义回答：

> 这个 Visual Family 最核心的视觉身份是什么？

Core Visual Identity 应综合：

- 主要视觉对象如何被呈现；
- 构图与画框关系；
- 空间与元素关系；
- 光线与阴影结构；
- 色彩、对比与色调；
- 表面、纹理与材质响应；
- 景深、焦点与空间分离；
- 真实—风格化位置与物理合理性；
- 感知气质及其可见机制；
- 已晋升 Adaptive Dimensions 提供的关键领域机制；
- 与主要 Anti-pattern 的差异。

它不能只是形容词列表，也不能通过固定 subject、单张构图或风格标签替代机制解释。

Core Visual Identity 需要指出结论的证据范围与总体 Confidence，但保持描述性，不生成 Phase 2 Rules。

## 16. Reference Weighting in Phase 1B

Reference role 的默认用途为：

| Reference role | Analysis use |
|---|---|
| Core | 定义 Core Visual Identity、重要 Pattern 与 Invariant 的主要证据 |
| Supporting | 验证共享方向，发现 Allowed Variation、边界与 Subtype 候选 |
| Ambiguous | 只用于受限假设、矛盾记录或待观察方向；不得单独支撑核心结论 |
| Outlier | 用于 boundary comparison、contamination analysis 与有证据的 Anti-pattern；不得定义 Core Visual Identity |

分析时还必须：

- 引用具体 Reference 文件或 Phase 1A 定义的集合，而不是笼统写“References 显示”；
- 记录缺失、矛盾和反例，而不是只保留支持样本；
- 如果 Phase 1A 的分类明显有事实错误，停止相关结论并按 Phase Contracts 回退，不在 Phase 1B 静默改权重。

## 17. Analysis Workflow

Phase 1B 推荐按以下顺序执行：

1. **Inherit Audit Scope**：确认 Core、Supporting、Ambiguous、Outlier 与 recommended analysis set；
2. **Run Core Dimension Pass**：对九个 Core Dimensions 完成证据检查，允许 `Insufficient Evidence`；
3. **Collect Adaptive Candidates**：从重复、身份、区分、变化、生成与质量信号中收集候选；
4. **Apply Promotion Threshold**：Promote、保留为 Observed Detail、归为 Incidental 或标记证据不足；
5. **Analyze Promoted Dimensions**：按 Adaptive Dimension Contract 完成专门分析；
6. **Synthesize Recurring Patterns**：分离 Frequency、Importance、Confidence 与 Contradiction；
7. **Assign Result Roles**：形成 Invariant、Allowed Variation、Incidental Detail 与 Anti-pattern；
8. **Evaluate Subtypes**：区分普通变化、Meaningful Subtype 与 Separate Skill Candidate；
9. **Write Core Visual Identity**：综合视觉机制而不是堆叠标签；
10. **Determine Phase 2 Readiness**：检查分析是否足以支持执行规格转换。

该顺序是分析流程，不是文件模板；实际 Artifact 可以在不丢失职责的前提下合理组织。

## 18. Analysis vs Specification Boundary

### 18.1 Allowed in Phase 1B

- 描述可见事实；
- 判断稳定性、变化、偶发性与不兼容方向；
- 解释视觉机制；
- 记录 Evidence、Frequency、Importance、Confidence 与 Contradiction；
- 形成描述性的 Core Visual Identity 与结果角色。

### 18.2 Not Allowed in Phase 1B

- 把结论转写成命令；
- 分配 `MUST / SHOULD / MAY / AVOID / DO NOT`；
- 编写生成 Prompt 或 Prompt vocabulary；
- 创建 Visual Rules、Prompt Rules 或 Quality Rules；
- 规定具体 QA 阈值；
- 因为模型偏好而增强或补写结论。

分析表达示例：

```text
The lower visual density recurs across the strongest references and appears to contribute materially to the family’s restrained organization.
```

不应在 Phase 1B 写成：

```text
MUST use low visual density.
```

Phase 2 负责判断前一条观察应转成何种规则强度、如何表达以及如何检测。

## 19. Output Expectations

Reference Analysis Artifact 至少应包含以下信息类别；本 Framework 不规定具体文件模板：

1. **Analysis Scope**：使用、限制或排除的 References 及其 Phase 1A 权重；
2. **Core Dimension Findings**：九个 Core Dimensions 的 Evidence、结论、矛盾与 Confidence；
3. **Adaptive Dimension Decisions**：候选、Promotion 结果、Parent Core Dimension 与证据；
4. **Recurring Patterns**：Frequency、Importance、Confidence、Contradiction 与潜在角色；
5. **Invariant Characteristics**；
6. **Allowed Variations**；
7. **Incidental Details / Observed Details**；
8. **Anti-patterns**；
9. **Subtype Analysis**；
10. **Core Visual Identity**；
11. **Evidence Confidence Summary**；
12. **Major Contradictions and Insufficient Evidence**；
13. **Readiness Verdict**。

为了支持未来 Traceability，每个关键结论必须能够指出其 Reference Evidence 与中间 Observation，但本阶段不分配 `REF / OBS / INV / VAR / ANTI` ID，也不定义链接 Schema。

## 20. Readiness for Visual System Specification

Phase 1B 最终只给出：

- `READY FOR VISUAL SYSTEM SPECIFICATION`；或
- `NOT READY`。

非阻断性限制可以随 READY Verdict 一并记录，但不得掩盖关键证据缺口。

### 20.1 READY Gate

只有同时满足以下条件，才可判定 READY：

- Core Visual Identity 已得到有证据的解释；
- 九个 Core Dimensions 已检查，弱证据项已明确标记；
- 所有高相关 Adaptive Candidates 已完成 Promotion 决定；
- 已晋升 Adaptive Dimensions 已完成分析；
- Invariants 已识别，且未由 Single-instance 单独支持；
- Allowed Variations 已识别，未被误写为固定模板；
- Incidental / Observed Details 已与核心结论分离；
- Anti-patterns 有 Reference 对比或污染证据；
- Evidence Confidence 已记录；
- Subtype 状态已判断；
- 重大矛盾已解决，或被证明不阻断 Phase 2；
- 分析保持描述性，没有提前创建执行规则。

### 20.2 NOT READY Conditions

以下任一情况通常意味着 NOT READY：

- Core Visual Identity 无法从有效 References 中成立；
- 关键 Core Dimension 的证据缺口阻止规则转换；
- 一个高重要性 Adaptive Candidate 无法判断，却会实质改变视觉身份；
- Invariant 与 Allowed Variation 仍相互冲突；
- Anti-pattern 主要来自 Builder 预设而非证据；
- 关键结论依赖 Ambiguous / Outlier Evidence；
- Subtype 与 Separate Skill 边界未解决；
- Brief 正在覆盖 Reference Evidence；
- 需要回退 Phase 1A 修正 Reference classification 或 evidence coverage。

NOT READY 时 Build 停留在 Phase 1B，或根据 `phase_contracts.md` 回退 Phase 1A。不得为了推进 Pipeline 而降低证据要求。

## 21. Framework Boundary

本 Framework 不负责：

- 定义或创建 Traceability ID / Schema；
- 创建 Visual Rules、Prompt Rules 或 Quality Rules；
- 分配执行层 Rule Strength；
- 编译目标 `SKILL.md`；
- 创建 Skill Audit；
- 创建 Test Cases、Rubric 或生成结果；
- 执行 Historical Backtest；
- 修改历史 Image Skill 或其 References。

这些工作只能在相应后续 Phase 获得明确授权后进行。
