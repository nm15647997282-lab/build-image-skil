你现在要为 AI 图片 B-roll Skill：

image-broll-object

执行 Phase 3：

Prompt 4 — Build Skill v1

本任务的目标是：

基于已经完成的 Reference Audit、Reference Analysis 与 Visual System Specification，
正式构建：

image-broll-object/SKILL.md

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

1. image-broll-object/References/
2. image-broll-object/reference_set_audit.md
3. image-broll-object/reference_analysis.md
4. image-broll-object/System/visual_rules.md
5. image-broll-object/System/prompt_rules.md
6. image-broll-object/System/quality_rules.md

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

image-broll-object/SKILL.md

这个文件未来需要回答：

“当系统已经决定调用 image-broll-object 时，
模型应该怎样构建一张符合该视觉语言的图片？”

它需要能够支持：

- 视觉生成
- Prompt 构建
- 结果自检
- 风格稳定
- 变体控制
- Anti-pattern 防漂移

但：

不要负责“什么时候调用这个 Skill”。

Usage Contract 不属于本 Skill。

--------------------------------------------------
三、SKILL.md 的定位
--------------------------------------------------

SKILL.md 不是：

- Reference 分析报告
- 摄影理论文章
- 风格说明书
- B-roll 分类规则
- Agent 路由规则
- 使用场景清单
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
四、核心构建原则
--------------------------------------------------

### 1. 不重新发明视觉风格

禁止加入：

- References 没有支持的新风格
- 新的摄影流派
- 新的色彩系统
- 新的布光系统
- 新的材质规则
- 新的构图审美
- 新的风格关键词

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

- 重复定义
- 分析过程
- 证据解释
- 长篇背景
- 非执行性文字

保留：

- 核心视觉目标
- 视觉不变量
- 生成流程
- Prompt 构建逻辑
- 关键可变项
- 风格保护规则
- QA 检查
- 失败修正方向

--------------------------------------------------
五、推荐 SKILL.md 结构
--------------------------------------------------

请按照以下结构构建。

# image-broll-object

## 1. Purpose

用极简短的一段话说明：

该 Skill 负责生成什么视觉对象。

只描述视觉职责。

不要定义：

什么时候使用。

--------------------------------------------------
## 2. Core Visual Identity

提炼 reference_analysis 中：

Final Visual Definition
+
Invariants

写成一段紧凑定义。

回答：

- 物件如何被呈现
- 环境如何存在
- 材质如何呈现
- 光线如何呈现
- 为什么不是商业产品摄影

不要超过必要长度。

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

--------------------------------------------------
## 4. Subject Construction

定义生成时如何处理主体。

包括：

- 主体清晰度
- 单主体 / 多主体
- 辅助物
- 物件状态
- 使用痕迹
- 是否允许新旧变化
- 主体与环境关系

强调：

object 必须具有现实物理存在感。

不要写语义路由规则。

--------------------------------------------------
## 5. Composition

整合：

- composition
- object-to-frame ratio
- viewpoint
- negative space
- visual density

要求：

优先写成可执行的构图指导。

不要重复每个 System 文件的细节。

--------------------------------------------------
## 6. Environment / Background

整合：

- context
- background
- spatial relation
- surface

重点保证：

物件不会滑向：

- catalog
- product hero shot
- sterile studio rendering

--------------------------------------------------
## 7. Lighting

提炼：

- 默认光线
- 可接受变化
- 明显跑偏方向

不要加入具体摄影器材参数。

--------------------------------------------------
## 8. Color / Tonal Character

提炼：

- 饱和度
- 冷暖
- 色彩克制
- 是否存在固定 palette

如果不存在固定 palette：

明确说明。

不要自行创造色值。

--------------------------------------------------
## 9. Materiality / Physical Realism

这是 image-broll-object 的核心章节之一。

整合：

- materiality
- surface texture
- reflections
- wear
- imperfections
- lived-in character
- CGI avoidance

这一节应该明确：

什么让物件看起来像真实生活中的物体，
而不是广告产品或数字渲染。

--------------------------------------------------
## 10. Depth / Focus

提炼：

- 主体清晰度
- 背景分离
- 景深倾向
- 是否允许强 bokeh / macro

--------------------------------------------------
## 11. Allowed Variation

从 visual_rules.md 中提炼。

使用类似结构：

| Variable | Allowed Variation | Must Remain Stable |

例如：

Subject type
Background surface
Viewpoint
Object age
Supporting props

但内容必须来自已有规则。

--------------------------------------------------
## 12. Prompt Construction

这是 Skill 的核心执行模块。

将 prompt_rules.md 压缩成一个清晰流程。

建议结构：

### Prompt Order

1. Subject
2. Physical state
3. Context
4. Composition
5. Lighting
6. Materiality
7. Color / tonal character
8. Depth / focus
9. Mood
10. Style guardrails

如果 System 文件定义不同顺序，以 System 为准。

--------------------------------------------------
## 13. Prompt Language Guidance

提炼：

### Preferred
### Conditional
### Risky
### Avoid

重点保留：

- 有效词汇
- 高风险词汇
- 更安全替代表达

不要做成巨大词典。

只保留真正影响稳定生成的词。

--------------------------------------------------
## 14. Anti-patterns

列出最重要的风格跑偏方向。

例如可能包括：

- e-commerce product photography
- luxury advertising
- glossy studio product shot
- pure white catalog background
- neon technology aesthetic
- surreal concept art
- sterile CGI
- decorative Pinterest still life
- excessive cinematic dramatization
- high-density tabletop styling

每一项只需要一句非常短的说明。

--------------------------------------------------
## 15. Generation Checklist

在生成前检查：

- 主体是否清楚
- 是否具备真实材质
- 环境是否低干扰
- 是否避免产品广告感
- 是否保持低视觉密度
- 是否有真实生活痕迹
- 是否有不必要的商业 polish

不要加入“是否应该使用本 Skill”。

--------------------------------------------------
## 16. Quality Check

将 quality_rules.md 压缩成最终 QA。

建议：

### PASS
### REVISE
### FAIL

不要强行建立复杂评分系统，
除非 quality_rules.md 已明确需要。

重点检查：

- visual family consistency
- commercial contamination
- material realism
- object geometry
- environment plausibility
- AI artifacts
- visual density
- lighting
- style drift

--------------------------------------------------
## 17. Revision Guidance

为高频失败提供短修正逻辑。

建议使用：

| Failure | Likely Cause | Fix |

例如：

Too commercial
→ too polished / too studio-like
→ reduce studio styling, restore realistic context and material wear

Too decorative
→ too many props
→ simplify composition

Too CGI
→ overly smooth material / impossible reflection
→ restore tactile surface and physical plausibility

只保留高频、重要失败。

--------------------------------------------------
## 18. Final Execution Rule

用一个很短的原则收尾。

例如逻辑可以是：

When in doubt, preserve:
real-world physicality,
material honesty,
restrained composition,
quiet contextual presence.

但具体措辞必须来自当前 visual system，
不要自行发明新的视觉哲学。

--------------------------------------------------
六、Prompt 构建层必须可直接执行
--------------------------------------------------

SKILL.md 中的 Prompt Construction 部分不能只写：

“Use quiet, restrained, humanistic photography.”

这种描述不够执行。

必须告诉模型：

如何组织：

- subject
- state
- context
- composition
- lighting
- material
- tonal character
- realism guardrails

但：

不要把某一个具体 subject 写死。

Skill 应能够适配不同 object。

--------------------------------------------------
七、不要把 SKILL.md 写成具体 Prompt 模板集合
--------------------------------------------------

本阶段不需要：

为 smartphone
alarm clock
employee badge
credit card
glasses

分别生成 production prompt。

这些属于：

Examples 或 Tests。

SKILL.md 只需要：

Prompt Construction Logic。

--------------------------------------------------
八、不要加入 Usage Contract
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
九、可以创建的附加文件
--------------------------------------------------

本 Prompt 的主要产物必须是：

SKILL.md

如果当前项目结构中：

Examples/
Tests/

不存在，

可以创建目录：

image-broll-object/Examples/
image-broll-object/Tests/

但：

本 Prompt 不要正式填充完整 Test Suite。

只允许：

创建空目录
或
创建最小占位 README

如果没有必要：

不要创建。

--------------------------------------------------
十、SKILL.md 长度控制
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
十一、Cross-check
--------------------------------------------------

完成 SKILL.md 后，逐项对照：

reference_analysis.md
visual_rules.md
prompt_rules.md
quality_rules.md

检查：

1. 是否遗漏核心 invariant
2. 是否遗漏关键 anti-pattern
3. 是否遗漏 Prompt 核心结构
4. 是否遗漏 QA 核心标准
5. 是否加入来源不存在的新规则
6. 是否把 Allowed Variation 写成了硬规则
7. 是否把 incidental feature 写成了 invariant
8. 是否出现规则冲突

如果发现：

SKILL.md 与 System 规则冲突，

优先修正 SKILL.md。

不要反向修改 System 文件。

--------------------------------------------------
十二、输出目录
--------------------------------------------------

最终结构至少应为：

image-broll-object/
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
十三、重要限制
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
19. 不要写成通用 still-life photography Skill。
20. 不要写成产品摄影 Skill。
21. 不要为了完整性加入 References 未支持的摄影参数。
22. 不要创建复杂代码实现，除非当前 Skill 架构明确要求。

--------------------------------------------------
十四、完成后的自检
--------------------------------------------------

提交前检查：

- 是否读取全部必要输入；
- 是否创建了 SKILL.md；
- 是否将 SKILL 定位为 execution layer；
- 是否保留 Core Visual Identity；
- 是否保留 Invariants；
- 是否包含 Subject Construction；
- 是否包含 Composition；
- 是否包含 Environment / Background；
- 是否包含 Lighting；
- 是否包含 Color；
- 是否重点包含 Materiality / Physical Realism；
- 是否包含 Depth / Focus；
- 是否包含 Allowed Variation；
- 是否包含 Prompt Construction；
- 是否包含 Prompt Language Guidance；
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
- 是否检查了规则冲突；
- 是否确保 Skill 可适配不同 object subject。

如果任何一项未完成，请先补全再结束任务。


