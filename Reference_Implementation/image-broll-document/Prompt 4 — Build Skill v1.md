
你现在要为 AI 图片 B-roll Skill：

image-broll-document

执行 Phase 3：

Prompt 4 — Build Skill v1

本任务的目标是：

基于已经完成的 Reference Audit、Reference Analysis 与 Visual System Specification，
正式构建：

image-broll-document/SKILL.md

这是该 Skill 的 v1 版本。

本 Prompt 的重点是：

把已有规则整理成一个
清晰、紧凑、可执行、可调用、可维护的 Skill 文件。

不要重新发明风格。
不要重新做 Reference Analysis。
不要重新设计 Visual System。
不要提前进入 Test Suite / Refinement。

--------------------------------------------------
一、必须读取的输入
--------------------------------------------------

请完整读取：

1. image-broll-document/References/
2. image-broll-document/reference_set_audit.md
3. image-broll-document/reference_analysis.md
4. image-broll-document/System/visual_rules.md
5. image-broll-document/System/prompt_rules.md
6. image-broll-document/System/quality_rules.md

其中：

- References = 原始视觉证据
- reference_set_audit.md = Reference 权重与边界
- reference_analysis.md = 视觉语言描述
- visual_rules.md = 视觉执行规则
- prompt_rules.md = Prompt 构建规则
- quality_rules.md = 质量判断规则

构建 SKILL.md 时：

以 System/ 下三份规则文件为主要执行依据，
以 reference_analysis.md 和 References 为验证依据。

--------------------------------------------------
二、构建目标
--------------------------------------------------

你要生成：

image-broll-document/SKILL.md

这个文件未来需要回答：

“当系统已经决定调用 image-broll-document 时，
模型应该怎样构建一张符合该视觉语言的图片？”

它需要能够支持：

- paper artifact 构建
- 旧照片 / 纸本残片呈现
- archival / memory character
- Prompt 构建
- 结果自检
- 风格稳定
- 变体控制
- Anti-pattern 防漂移

但：

不要负责“什么时候调用这个 Skill”。

Usage Contract 不属于本 Skill。

--------------------------------------------------
三、本 Skill 的职责边界
--------------------------------------------------

image-broll-document 不是：

- readable document generator
- quotation renderer
- report renderer
- historical evidence renderer
- exact source text renderer
- newspaper/article text renderer

它不承担：

- 精确原文呈现
- 真实文献复现
- 可验证报告展示
- 长段文字生成
- source-based evidence reproduction

它负责的是：

以旧照片、纸本残片、私人档案、纸质记忆载体、历史痕迹或类似 archival paper artifact 为视觉主体的静态 B-roll 图片。

核心是：

paper artifact as physical object

而不是：

document as readable text.

--------------------------------------------------
四、SKILL.md 的定位
--------------------------------------------------

SKILL.md 不是：

- Reference 分析报告
- 档案美学文章
- 复古摄影教程
- 文档分类规则
- B-roll 使用规则
- Agent 路由规则
- 测试报告

SKILL.md 是：

“面向执行的视觉生成协议”。

因此必须做到：

- 简洁
- 有优先级
- 可执行
- 不重复
- 不堆术语
- 不写大量解释性废话

--------------------------------------------------
五、核心构建原则
--------------------------------------------------

### 1. 不重新发明视觉风格

禁止加入：

- References 没有支持的新风格
- 泛 vintage aesthetic
- 泛 nostalgic aesthetic
- 新的 archival design 体系
- 新的 collage 语言
- 新的 scrapbook 语言
- 新的 retro graphic design 语言
- 新的色彩系统
- 新的老化系统
- 新的构图审美

如果已有规则中不存在：

不要为了“让 SKILL 更完整”而自行补充。

---

### 2. 压缩，而不是复制

不要把：

reference_analysis.md
visual_rules.md
prompt_rules.md
quality_rules.md

全文拼接到 SKILL.md。

SKILL.md 应该是：

“执行层摘要”。

去除：

- 分析过程
- Reference 证据解释
- 重复定义
- 长篇背景
- 非执行性描述

保留：

- Core Visual Identity
- Visual Invariants
- Artifact Construction
- Composition
- Negative Space
- Materiality
- Aging
- Prompt Construction Logic
- Style Guardrails
- QA
- Revision Guidance

--------------------------------------------------
六、推荐 SKILL.md 结构
--------------------------------------------------

请按照以下结构构建。

# image-broll-document

## 1. Purpose

用极简短的一段话说明：

该 Skill 负责生成什么视觉对象。

只描述视觉职责。

必须明确：

它生成的是：

archival paper artifact / old photograph / memory fragment style still image

而不是：

readable document or source text.

不要定义什么时候使用。

--------------------------------------------------
## 2. Core Visual Identity

提炼：

reference_analysis.md 中的 Final Visual Definition
+
visual_rules.md 中的 Invariants

写成一段紧凑定义。

需要回答：

- 纸本对象如何被呈现
- 为什么主体具有物理存在感
- 留白如何作用
- 老化如何呈现
- 背景如何存在
- 为什么画面有档案感 / 记忆感
- 为什么不是 scrapbook
- 为什么不是 retro poster
- 为什么不是 generic vintage aesthetic

--------------------------------------------------
## 3. Core Invariants

列出最重要的 5–12 条。

优先来自：

visual_rules.md / Invariants

使用清晰的 MUST / SHOULD 表述。

例如结构：

- MUST ...
- MUST ...
- SHOULD ...
- SHOULD ...

只保留真正决定视觉身份的规则。

不要把偶发的：

- 撕裂
- 胶带
- 手写
- 重度泛黄
- 某种具体背景

误写成 invariant。

--------------------------------------------------
## 4. Artifact Construction

定义生成时如何处理纸本主体。

包括：

- 单张旧照片
- 多张旧照片
- 纸本残片
- mounted photograph
- faded print
- paper fragment
- card / small archival object

需要说明：

- 主体应该作为真实物理对象存在
- 是否允许单件 / 少量组合
- artifact 如何与背景接触
- 是否允许轻微重叠
- 是否允许轻微倾斜
- 是否允许装裱
- 是否允许不同 paper subtype

避免：

把 artifact 当成平面设计元素。

--------------------------------------------------
## 5. Artifact Treatment

整合：

- flat
- mounted
- attached
- stacked
- gently overlapping
- slightly angled
- torn
- creased
- curled edge

需要区分：

Default
Allowed Variation
Avoid

特别强调：

damage / aging 不是为了做“复古效果”，

而是为了支持：

physical realism
time trace
archive character

--------------------------------------------------
## 6. Composition

整合：

- artifact-to-frame ratio
- subject placement
- visual density
- orientation
- background exposure
- edge relationship

重点体现：

- restraint
- stillness
- low density
- artifact clarity

不要写成 collage 构图指南。

--------------------------------------------------
## 7. Negative Space

这是本 Skill 的核心章节之一。

提炼：

- 留白的重要程度
- 留白如何围绕主体存在
- 留白如何帮助形成 archive / memory character
- 留白如何帮助降低视觉噪音

同时明确避免：

- decorative minimalism
- subject-too-small-for-aesthetic-only
- poster-like spacing
- layout-driven empty space

--------------------------------------------------
## 8. Background / Support Surface

整合：

- 墙面
- 卡纸
- 布面
- 桌面
- 中性纸面
- 其他 Reference 支持的低干扰表面

重点定义：

背景的作用是：

- 承载
- 提供材质
- 提供色彩分离
- 提供物理接触关系

不是：

- 做造型
- 建立 scrapbook 场景
- 堆复古装饰

--------------------------------------------------
## 9. Paper Materiality / Physical Realism

这是本 Skill 的核心章节。

整合：

- paper thickness
- edge realism
- fibers
- photographic paper
- matte / slight gloss
- folds
- curl
- surface wear
- contact shadow
- mounting relation

需要明确：

什么让 paper artifact 看起来像：

“真实存在的旧照片或纸本物件”

而不是：

- digital texture
- Photoshop mockup
- CGI card
- flat printed layer

--------------------------------------------------
## 10. Aging / Imperfection

整合：

- fading
- yellowing
- edge wear
- creases
- stains
- scratches
- torn corners
- surface degradation

需要明确区分：

natural aging
vs
aesthetic distressing

核心原则：

aging should be restrained and physically plausible.

不要把：

sepia
grunge
heavy distress
dramatic decay

当作默认。

--------------------------------------------------
## 11. Photograph Treatment

如果主体是照片：

提炼：

- black-and-white
- faded color
- low saturation
- border
- white margin
- print grain
- tonal softness

但必须确保：

physical photograph object

优先于：

image content itself.

不要让 Skill 退化成：

人物老照片生成器。

--------------------------------------------------
## 12. Lighting

提炼：

- 默认光线
- 可接受变化
- 阴影
- 边缘表现
- 纸张纹理表现
- 反光控制
- 明显跑偏方向

不要加入具体设备参数。

重点：

光线要帮助看见：

paper thickness
edge
fold
surface
mounting relation

而不是制造：

cinematic nostalgia。

--------------------------------------------------
## 13. Color / Tonal Character

提炼：

- 饱和度
- 色温
- 中性色倾向
- 黑白与褪色彩色照片
- paper tone
- background tone

如果不存在固定 palette：

明确说明。

不要自行创造：

sepia default
fixed beige palette
fixed vintage LUT

--------------------------------------------------
## 14. Typography Presence

这是必须明确的一节。

说明：

文字如果出现：

- 可以是少量编号
- 日期
- 背书
- 标签
- 手写痕迹
- incidental text

但：

文字不能成为主体。

明确：

DO NOT generate large readable text blocks as the primary visual content.

不要让：

AI gibberish
fake quote
fake report
fake newspaper

进入默认画面。

--------------------------------------------------
## 15. Human Content Inside Artifact

如果旧照片中有人物：

说明：

- 人物属于 artifact 内部内容
- 画面主体仍然是 paper artifact
- 不应转成完整人物肖像画面
- 人物可以帮助建立私人记忆感，但不改变本 Skill 的视觉主体

--------------------------------------------------
## 16. Allowed Variation

从 visual_rules.md 中提炼。

建议使用：

| Variable | Allowed Variation | Must Remain Stable |

例如可能包括：

- artifact type
- single / double artifact
- black-and-white / faded color
- background surface
- damage level
- mounting style
- placement angle

内容必须来自已有规则。

--------------------------------------------------
## 17. Prompt Construction

这是 Skill 的核心执行模块。

将 prompt_rules.md 压缩成清晰流程。

建议结构：

### Prompt Order

1. Artifact type
2. Physical state
3. Placement / treatment
4. Background
5. Composition / negative space
6. Lighting
7. Paper materiality
8. Aging / imperfection
9. Color / tonal character
10. Archive / memory character
11. Style guardrails

如果 System 文件定义不同顺序，以 System 为准。

--------------------------------------------------
## 18. Prompt Language Guidance

提炼：

### Preferred
### Conditional
### Risky
### Avoid

重点处理高风险词：

- vintage
- retro
- nostalgic
- archival
- antique
- ephemera
- distressed
- cinematic
- moody
- historical

不要简单全部禁止。

要保留 System 已经确定的：

- 哪些可用
- 哪些需要限定
- 哪些容易跑向错误视觉
- 哪些有更安全的替代词

--------------------------------------------------
## 19. Physical-description First Principle

单独写一个简短规则：

优先使用：

- paper thickness
- faded surface
- slight edge wear
- gentle crease
- matte photographic paper
- natural curl
- restrained fading
- realistic contact shadow

这类物理描述。

少依赖：

- vintage
- nostalgic
- antique
- retro
- old-fashioned

这类抽象风格词。

目标是：

让“旧感”来自物理证据，

而不是来自抽象复古标签。

--------------------------------------------------
## 20. Anti-patterns

列出最重要的风格跑偏方向。

重点可能包括：

- scrapbook
- moodboard collage
- memory board
- retro poster design
- vintage graphic design
- journal spread
- decorative stationery
- excessive tape / sticker styling
- fake antique parchment
- exaggerated distressing
- fake newspaper
- fake historical evidence
- AI gibberish text
- social-media quote card
- typography-led composition
- dense paper collage
- cinematic archive drama
- generic sepia nostalgia
- sentimental vintage cliché
- digital mockup

每一项只需要一句短说明。

--------------------------------------------------
## 21. Generation Checklist

生成前检查：

- artifact 是否是视觉主体
- paper 是否具有物理存在感
- 是否保留合理留白
- aging 是否克制自然
- background 是否低干扰
- visual density 是否足够低
- 是否避免 scrapbook
- 是否避免 fake antique
- 是否避免大量可读文字
- 是否避免 generic vintage styling
- 是否避免 digital mockup 感

不要加入：

“是否应该使用本 Skill”。

--------------------------------------------------
## 22. Quality Check

将 quality_rules.md 压缩成最终 QA。

建议：

### PASS
### REVISE
### FAIL

重点检查：

- artifact clarity
- paper physicality
- negative space
- aging realism
- background restraint
- typography non-dominance
- archive / memory character
- decorative contamination
- AI artifacts
- style-family consistency

不要强行做复杂评分系统，
除非 quality_rules.md 已经明确需要。

--------------------------------------------------
## 23. Revision Guidance

为高频失败提供短修正逻辑。

建议使用：

| Failure | Likely Cause | Fix |

例如：

Too scrapbook-like
→ too many layered artifacts / decorative accessories
→ reduce artifact count, simplify composition, restore negative space

Too fake-antique
→ aging language too aggressive
→ reduce distress, use subtle fading and natural edge wear

Too text-heavy
→ prompt describes readable document
→ reduce typography role, return focus to paper artifact

Too digital
→ insufficient paper thickness / contact shadow / surface texture
→ restore physical paper cues

Too sentimental
→ mood vocabulary too strong
→ reduce nostalgia wording, rely on material and spacing

只保留高频、重要失败。

--------------------------------------------------
## 24. Final Execution Rule

用一个非常短的原则收尾。

核心逻辑应来自当前 visual system。

例如可以概括为：

When in doubt, preserve:

paper-object physicality,
restrained aging,
quiet negative space,
material realism,
archival restraint.

但具体措辞必须与已有规则一致。

不要自行发明新的视觉哲学。

--------------------------------------------------
七、Prompt 构建层必须可直接执行
--------------------------------------------------

SKILL.md 中的 Prompt Construction 不能只写：

“Use a nostalgic archival aesthetic.”

这种描述不可执行且风险很高。

必须告诉模型如何组织：

- artifact
- physical state
- placement
- background
- negative space
- lighting
- paper materiality
- aging
- tone
- style guardrails

尤其应该优先：

physical description

而不是：

abstract vintage adjective stacking。

--------------------------------------------------
八、不要把 SKILL.md 写成具体 Prompt 模板集合
--------------------------------------------------

本阶段不需要分别为：

- old family photograph
- torn photo
- mounted photograph
- stacked photos
- faded print
- paper fragment

创建完整 production prompts。

这些属于：

Examples 或 Tests。

SKILL.md 只需要：

Prompt Construction Logic。

--------------------------------------------------
九、不要加入 Usage Contract
--------------------------------------------------

再次强调：

不要写：

Use when...
Do not use when...
Trigger...
Routing...
Semantic condition...
Visual Director decision...
Asset Agent decision...

这些不属于本 Skill。

SKILL.md 只处理：

调用以后怎么生成。

--------------------------------------------------
十、可以创建的附加文件
--------------------------------------------------

本 Prompt 的主要产物必须是：

SKILL.md

如果当前项目结构中：

Examples/
Tests/

不存在，

可以创建目录：

image-broll-document/Examples/
image-broll-document/Tests/

但：

本 Prompt 不要正式填充完整 Test Suite。

只允许：

创建空目录
或
创建最小占位 README。

如果没有必要：

不要创建。

--------------------------------------------------
十一、SKILL.md 长度控制
--------------------------------------------------

SKILL.md 应该：

足够完整，

但明显短于：

reference_analysis.md
+
System 三份规则文件。

原则：

SKILL.md = execution layer

不是全部知识库。

如果出现：

大量重复 System 文件内容

说明压缩失败。

--------------------------------------------------
十二、Cross-check
--------------------------------------------------

完成 SKILL.md 后，逐项对照：

reference_analysis.md
visual_rules.md
prompt_rules.md
quality_rules.md

检查：

1. 是否遗漏核心 invariant
2. 是否遗漏 paper materiality
3. 是否遗漏 negative space
4. 是否遗漏 natural aging
5. 是否遗漏 typography non-dominance
6. 是否遗漏关键 anti-pattern
7. 是否遗漏 Prompt 核心结构
8. 是否遗漏 QA 核心标准
9. 是否加入来源不存在的新规则
10. 是否把 Allowed Variation 写成硬规则
11. 是否把 incidental damage 写成 invariant
12. 是否把 vintage / sepia 写成默认
13. 是否出现规则冲突
14. 是否把 Skill 错误写成 readable document generator

如果发现：

SKILL.md 与 System 规则冲突，

优先修正 SKILL.md。

不要反向修改 System 文件。

--------------------------------------------------
十三、输出目录
--------------------------------------------------

最终结构至少应为：

image-broll-document/
│
├── References/
├── reference_set_audit.md
├── reference_analysis.md
├── System/
│   ├── visual_rules.md
│   ├── prompt_rules.md
│   └── quality_rules.md
│
└── SKILL.md

如果已有：

Examples/
Tests/

保持不变。

--------------------------------------------------
十四、重要限制
--------------------------------------------------

1. 不要修改 References。
2. 不要修改 reference_set_audit.md。
3. 不要修改 reference_analysis.md。
4. 不要修改 visual_rules.md。
5. 不要修改 prompt_rules.md。
6. 不要修改 quality_rules.md。
7. 不要联网搜索。
8. 不要生成图片。
9. 不要开始正式 Test Suite。
10. 不要进行 Refinement Loop。
11. 不要加入 Usage Contract。
12. 不要定义系统调用时机。
13. 不要加入视频剪辑规则。
14. 不要加入 Camera Motion。
15. 不要加入 LUT。
16. 不要加入 Transition。
17. 不要加入 B-roll 时长规则。
18. 不要加入新的视觉风格。
19. 不要写成通用 vintage photography Skill。
20. 不要写成 archival graphic design Skill。
21. 不要写成 scrapbook / collage Skill。
22. 不要写成 readable document generation Skill。
23. 不要把 sepia 当默认。
24. 不要把 heavy damage 当默认。
25. 不要为了完整性加入 References 未支持的摄影参数。
26. 不要创建复杂代码实现，除非当前 Skill 架构明确要求。

--------------------------------------------------
十五、完成后的自检
--------------------------------------------------

提交前检查：

- 是否读取全部必要输入；
- 是否创建了 SKILL.md；
- 是否将 SKILL 定位为 execution layer；
- 是否明确了 non-readable-document boundary；
- 是否保留 Core Visual Identity；
- 是否保留 Invariants；
- 是否包含 Artifact Construction；
- 是否包含 Artifact Treatment；
- 是否包含 Composition；
- 是否重点包含 Negative Space；
- 是否包含 Background / Support Surface；
- 是否重点包含 Paper Materiality / Physical Realism；
- 是否重点包含 Aging / Imperfection；
- 是否包含 Photograph Treatment；
- 是否包含 Lighting；
- 是否包含 Color / Tonal Character；
- 是否包含 Typography Presence；
- 是否包含 Human Content Inside Artifact；
- 是否包含 Allowed Variation；
- 是否包含 Prompt Construction；
- 是否包含 Prompt Language Guidance；
- 是否包含 Physical-description First Principle；
- 是否包含 Anti-patterns；
- 是否包含 Generation Checklist；
- 是否包含 Quality Check；
- 是否包含 Revision Guidance；
- 是否没有重新做 Reference Analysis；
- 是否没有重新发明 Visual System；
- 是否没有加入 Usage Contract；
- 是否没有开始正式测试；
- 是否没有修改 System 文件；
- 是否没有将整个 System 文件机械复制进 SKILL.md；
- 是否没有把 vintage / retro / sepia 变成默认；
- 是否没有把 readable text 变成核心；
- 是否没有把 scrapbook / collage 引入默认语言；
- 是否检查了规则冲突；
- 是否确保 Skill 可适配不同 paper artifact subtype。

如果任何一项未完成，请先补全再结束任务。

