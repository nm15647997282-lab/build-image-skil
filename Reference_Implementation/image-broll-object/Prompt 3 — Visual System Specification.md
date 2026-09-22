
你现在要为 AI 图片 B-roll Skill：

image-broll-object

执行 Phase 2：

Prompt 3 — Visual System Specification

本任务的目标是：

基于已经完成的：

1. image-broll-object/References/
2. image-broll-object/reference_set_audit.md
3. image-broll-object/reference_analysis.md

把 References 中提炼出的视觉语言，从“描述层”转换成“可执行的视觉系统规格”。

本 Prompt 不负责最终构建 SKILL.md。

本 Prompt 的任务是生成：

1. visual_rules.md
2. prompt_rules.md
3. quality_rules.md

这三个文件共同构成后续 SKILL.md 的规则基础。

--------------------------------------------------
一、必须读取的输入
--------------------------------------------------

请完整读取并综合：

image-broll-object/References/

image-broll-object/reference_set_audit.md

image-broll-object/reference_analysis.md

必须遵守以下证据优先级：

References
+
reference_set_audit.md
+
reference_analysis.md

其中：

- Reference 图片是原始视觉证据；
- reference_set_audit.md 决定哪些图片权重更高；
- reference_analysis.md 是视觉语言的正式分析结果。

如果三者存在冲突：

优先回到 Reference 图片本身判断。

不要自行引入外部风格体系覆盖现有分析。

--------------------------------------------------
二、任务目标
--------------------------------------------------

你现在需要完成的是：

把：

“这些图片通常看起来怎样”

转换成：

“未来生成图片时，应如何稳定复现这种视觉语言”。

也就是说：

Reference Analysis
↓
Visual Specification

必须完成三层转换：

A. Visual Rules
B. Prompt Construction Rules
C. Quality Evaluation Rules

这三个层级彼此不同，不要混在一起。

--------------------------------------------------
三、本 Prompt 不负责的内容
--------------------------------------------------

不要定义：

- 什么时候调用 image-broll-object
- 哪些语义触发它
- Asset Agent 如何路由
- 与 image-broll-document 的路由
- 与 image-broll-quote 的路由
- 与 MG 的路由
- 视频使用窗口
- B-roll 时长
- Camera Motion
- LUT
- Transition
- 视频节奏
- 使用频率

这些属于系统其他环节。

当前只负责：

“当系统已经决定要生成 image-broll-object 时，这张图具体应该如何生成。”

--------------------------------------------------
四、核心转换原则
--------------------------------------------------

### 1. 从描述性语言转换为执行性规则

reference_analysis 中可能存在：

“Soft, restrained side lighting appears consistently across the core references.”

这属于描述。

visual_rules.md 中应转换成类似：

“Prefer soft, restrained directional lighting with gentle shadow definition. Avoid hard commercial product lighting unless supported by the selected reference subtype.”

但：

不要机械把所有分析改成“Always”。

规则必须体现：

- 必须保持
- 默认倾向
- 可选变化
- 禁止跑偏

之间的区别。

---

### 2. 建立规则强度等级

所有重要视觉规则尽量分类为：

MUST
SHOULD
MAY
AVOID
DO NOT

定义：

MUST
= 一旦缺失，风格明显失真。

SHOULD
= 默认遵守，但允许受 subject 或 subtype 影响。

MAY
= References 支持的可选变化。

AVOID
= 容易跑偏，应尽量避免。

DO NOT
= 明显违反核心视觉语言。

不要滥用 MUST 和 DO NOT。

只有 Reference Analysis 的 High Confidence / Invariant Characteristics 才适合成为 MUST。

--------------------------------------------------
五、输出 1：visual_rules.md
--------------------------------------------------

生成：

image-broll-object/System/visual_rules.md

建议结构如下：

# image-broll-object — Visual Rules

## 1. Visual Objective

用一段简短文字定义：

这个 Skill 要稳定生成什么样的静态物件画面。

必须来自 reference_analysis 的 Final Visual Definition。

不要重新发明风格命名。

--------------------------------------------------
## 2. Rule Priority
--------------------------------------------------

定义优先级，例如：

1. Subject clarity
2. Real-world materiality
3. Human / lived-in character
4. Composition restraint
5. Lighting realism
6. Contextual coherence
7. Color restraint
8. Decorative styling avoidance

如果 reference_analysis 支持不同优先级，请据此调整。

--------------------------------------------------
## 3. Subject Rules
--------------------------------------------------

定义：

- 主体如何被呈现
- 单主体与多主体关系
- 主物件和辅助物关系
- 是否强调使用痕迹
- 是否允许崭新物件
- 是否允许对象英雄化
- 是否允许多个物件形成小型组合

重点明确：

物件必须是：

“具体存在的现实对象”

而不是：

“抽象概念的视觉隐喻”。

但不要把语义选择规则写进这里。

这里只处理画面呈现。

--------------------------------------------------
## 4. Composition Rules
--------------------------------------------------

将 Reference Analysis 中的构图规律转换成规则。

包括：

- 居中 / 偏置倾向
- 对称 / 非对称
- 主体位置
- 留白
- 边缘距离
- 是否允许近裁切
- 是否允许 frame-filling
- 是否允许强透视
- 是否允许戏剧化角度

必须区分：

Default
Allowed Variation
Avoid

--------------------------------------------------
## 5. Object-to-Frame Ratio
--------------------------------------------------

定义相对尺度规则。

不要伪造精确数值。

可以使用：

small
moderate
dominant
frame-filling

如果 Reference 足够支持范围，可以给出宽松百分比区间。

但只有证据充分时才允许。

--------------------------------------------------
## 6. Camera / Viewpoint Rules
--------------------------------------------------

规定：

- 常用视角
- 可接受视角
- 不适合视角
- 是否偏观察式
- 是否偏用户视角
- 是否偏桌面视角

不要指定具体镜头型号。

不要自行指定焦段，除非 Reference Analysis 有充分证据。

--------------------------------------------------
## 7. Context / Environment Rules
--------------------------------------------------

规定环境如何存在。

例如：

- 是否应保留现实表面
- 是否允许桌面 / 工作空间
- 环境是否应提供生活感
- 环境是否应该模糊
- 环境是否必须低干扰
- 是否允许摄影棚纯背景

重点防止：

物件被抽离成广告产品图。

--------------------------------------------------
## 8. Background Rules
--------------------------------------------------

定义：

- 背景复杂度
- 背景材质倾向
- 背景颜色倾向
- 背景与主体关系
- 负空间作用
- 是否允许纯白 seamless backdrop
- 是否允许高饱和背景

--------------------------------------------------
## 9. Lighting Rules
--------------------------------------------------

定义：

- 光线类型
- 光线方向
- 阴影强度
- 高光控制
- 是否保留材质细节
- 是否允许戏剧性布光
- 是否允许 commercial studio lighting

避免写死具体灯位和色温数值。

--------------------------------------------------
## 10. Color Rules
--------------------------------------------------

定义：

- 饱和度
- 冷暖
- 中性色倾向
- 允许色彩变化
- 强调色是否存在
- 高饱和色如何处理

如果 Reference Analysis 没有固定 palette：

明确写：

No fixed color palette; maintain the tonal restraint evidenced by references.

--------------------------------------------------
## 11. Materiality Rules
--------------------------------------------------

这是 image-broll-object 的核心模块。

定义：

- 材质必须可感知
- 表面纹理如何呈现
- 金属 / 塑料 / 纸张 / 木材等不能被过度平滑
- 反光如何控制
- 是否保留细小磨损
- 是否避免 CGI-like surfaces
- 是否避免过度 polished texture

--------------------------------------------------
## 12. Imperfection / Lived-in Rules
--------------------------------------------------

定义：

- 什么程度的使用痕迹合适
- 哪些 imperfections 可接受
- 哪些属于自然
- 哪些属于刻意做旧
- 是否允许轻微杂乱
- 是否允许灰尘 / 指纹 /划痕

特别避免：

“为了人文感而强行把所有物件做旧”。

--------------------------------------------------
## 13. Depth / Focus Rules
--------------------------------------------------

定义：

- 景深倾向
- 主体清晰度
- 背景可辨识度
- 是否允许强 bokeh
- 是否允许 macro look
- 是否允许全部清晰

--------------------------------------------------
## 14. Visual Density Rules
--------------------------------------------------

定义：

- 默认元素数量
- 辅助物密度
- 空间复杂度
- 是否允许高密度 tabletop styling

--------------------------------------------------
## 15. Negative Space Rules
--------------------------------------------------

定义：

- 留白的重要程度
- 留白是否必须
- 留白如何服务画面
- 如何避免过度极简设计感
- 如何避免模板化空白

--------------------------------------------------
## 16. Human Presence Rules
--------------------------------------------------

如果 References 支持：

定义：

- 是否允许手部
- 是否允许身体局部
- 是否允许模糊人物
- 人是否必须退居辅助
- 人是否可能抢主体

如果 Reference Analysis 证据不足：

明确写：

Insufficient evidence — do not elevate human presence into a default rule.

--------------------------------------------------
## 17. Emotional Tone Rules
--------------------------------------------------

把 reference_analysis 中的情绪气质转换成：

- 应保持的感觉
- 通过哪些视觉因素实现
- 不应通过哪些夸张方式实现

避免单纯形容词堆砌。

--------------------------------------------------
## 18. Realism Rules
--------------------------------------------------

规定：

- 现实可信度
- 物件物理逻辑
- 材质可信度
- 光线可信度
- 环境逻辑
- AI artifact
- CGI look
- excessive polish

--------------------------------------------------
## 19. Allowed Variation
--------------------------------------------------

明确列出：

哪些变化属于同一风格。

每项说明：

Variable
Allowed range
What must remain stable

例如：

Background material:
May vary
But must remain visually quiet and physically plausible

--------------------------------------------------
## 20. Invariants
--------------------------------------------------

从 reference_analysis 的 Invariant Characteristics 转换成正式规则。

这是视觉系统最高优先级。

数量不要过多。

建议控制在：

5–12 条。

--------------------------------------------------
## 21. Anti-patterns
--------------------------------------------------

将已确认的 Anti-patterns 转换成明确规则。

重点包括：

- e-commerce product photography
- luxury advertising
- glossy studio hero shot
- pure white catalog background
- neon technology look
- surreal AI art
- conceptual fantasy
- excessive cinematic dramatization
- decorative Pinterest still life
- high-density tabletop styling
- sterile CGI
- hyper-clean product rendering

每个 anti-pattern 尽量说明：

“为什么它破坏当前视觉语言”。

--------------------------------------------------
六、输出 2：prompt_rules.md
--------------------------------------------------

生成：

image-broll-object/System/prompt_rules.md

这个文件专门解决：

“如何把 visual_rules 转换成稳定的 image-generation prompt。”

不要生成具体生产 Prompt。

要生成：

Prompt Construction System。

推荐结构：

# image-broll-object — Prompt Rules

## 1. Prompt Objective

说明：

Prompt 的任务不是创造新风格，
而是把具体 object subject 映射进已冻结视觉系统。

--------------------------------------------------
## 2. Prompt Information Hierarchy
--------------------------------------------------

建议规定 Prompt 信息顺序。

例如：

1. Subject
2. Physical condition / state
3. Context
4. Composition
5. Lighting
6. Materiality
7. Color / tonal character
8. Depth / camera feel
9. Mood
10. Anti-style constraints

但必须根据现有 Visual Rules 调整。

--------------------------------------------------
## 3. Subject Description Rules
--------------------------------------------------

规定：

如何描述具体物件。

包括：

- material
- age
- condition
- orientation
- usage state
- relation to nearby objects

避免：

抽象、诗意但无法执行的描述。

--------------------------------------------------
## 4. Context Description Rules
--------------------------------------------------

如何描述：

- tabletop
- desk
- shelf
- workspace
- domestic surface
- neutral environment

等环境信息。

重点：

context 必须帮助物件真实存在，而不是制造无关装饰。

--------------------------------------------------
## 5. Composition Vocabulary
--------------------------------------------------

建立推荐的构图描述方式。

例如：

- restrained composition
- moderate negative space
- slightly off-center
- simple observational framing

但：

只能保留 Reference 支持的词。

--------------------------------------------------
## 6. Lighting Vocabulary
--------------------------------------------------

建立：

Preferred wording
Conditional wording
Avoid wording

例如：

Preferred:
soft natural side light

Avoid:
dramatic cinematic spotlight
luxury product lighting

但具体内容必须来自 Visual Rules。

--------------------------------------------------
## 7. Materiality Vocabulary
--------------------------------------------------

这是重点。

规定如何描述：

- tactile
- worn
- matte
- scratched
- slightly aged
- natural surface texture
- realistic reflections

同时防止：

- hyper-detailed
- ultra polished
- luxury finish
- CGI render

等词把结果带偏。

--------------------------------------------------
## 8. Realism Vocabulary
--------------------------------------------------

定义哪些词有助于：

- physically plausible
- observational
- lived-in
- realistic material response

哪些词可能导致：

- overly cinematic
- fashion editorial
- advertising
- surrealism

--------------------------------------------------
## 9. Mood Vocabulary
--------------------------------------------------

哪些情绪词可以使用。

哪些词必须谨慎。

例如：

quiet
restrained
thoughtful

可能适合。

但：

moody
cinematic
dramatic
luxurious
dreamlike

可能需要限制。

必须依据 Reference Analysis。

--------------------------------------------------
## 10. Negative Prompt / Avoidance Strategy
--------------------------------------------------

如果后续生成模型支持 negative prompt，
定义可使用的 anti-style vocabulary。

如果不支持：

说明这些约束应写入主 Prompt 的末段。

--------------------------------------------------
## 11. Risky Vocabulary
--------------------------------------------------

建立：

| Word / Phrase | Risk | Safer Alternative |

例如：

“editorial”
可能被模型解释成 fashion editorial。

“minimal”
可能导致 sterile studio minimalism。

“vintage”
可能导致 fake retro styling。

是否属于风险词，必须根据当前 Skill 实际情况判断。

--------------------------------------------------
## 12. Prompt Compression Rules
--------------------------------------------------

规定：

Prompt 不应该无限堆叠形容词。

需要确定：

- 哪些信息必须保留
- 哪些可以省略
- 哪些不能重复
- 如何避免 conflicting adjectives

--------------------------------------------------
## 13. Prompt Template Logic
--------------------------------------------------

只定义结构。

例如：

[subject]
+
[state / material]
+
[context]
+
[composition]
+
[lighting]
+
[color / tonal character]
+
[materiality / realism]
+
[style guardrails]

不要在这里创建最终 production prompt。

--------------------------------------------------
## 14. Variation Handling
--------------------------------------------------

说明：

当具体 subject 不同时，
哪些字段可以变化，
哪些字段仍要维持视觉一致。

--------------------------------------------------
## 15. Prompt Failure Patterns
--------------------------------------------------

列出容易导致：

- product ad
- catalog
- luxury commercial
- surreal object art
- CGI
- decorative still life

的 Prompt 写法。

--------------------------------------------------
七、输出 3：quality_rules.md
--------------------------------------------------

生成：

image-broll-object/System/quality_rules.md

这个文件用于：

判断最终生成图是否属于 image-broll-object。

它不是 Usage Contract。

只负责视觉质量评估。

推荐结构：

# image-broll-object — Quality Rules

## 1. Evaluation Goal

定义：

QA 判断的不是“图片漂不漂亮”，
而是：

“它是否忠实复现 Reference-derived visual system。”

--------------------------------------------------
## 2. Evaluation Dimensions
--------------------------------------------------

至少包括：

- Subject clarity
- Composition
- Context
- Lighting
- Color restraint
- Materiality
- Imperfection
- Realism
- Visual density
- Negative space
- Emotional tone
- Commercial contamination
- AI artifact risk

--------------------------------------------------
## 3. Pass Criteria
--------------------------------------------------

定义一张合格图应该满足什么。

按：

Critical
Important
Secondary

区分。

--------------------------------------------------
## 4. Fail Criteria
--------------------------------------------------

明确什么情况直接判 Fail。

例如可能包括：

- unmistakable product advertisement
- CGI-looking material
- surreal concept art
- excessive props
- fashion-commercial styling
- unrealistic object geometry
- excessive text artifact
- extreme cinematic lighting

具体标准必须依据 visual_rules。

--------------------------------------------------
## 5. Severity Levels
--------------------------------------------------

建议使用：

PASS
PASS WITH MINOR ISSUES
REVISE
FAIL

定义每一级。

--------------------------------------------------
## 6. Scoring Rubric
--------------------------------------------------

可以建立简单评分系统。

例如：

1–5 scale

但不要为了“量化”而制造伪精确。

如果使用评分：

明确哪些维度是一票否决项。

--------------------------------------------------
## 7. Commercial-look Check
--------------------------------------------------

单独建立检查：

- 是否像电商
- 是否像广告
- 是否像品牌 campaign
- 是否像奢侈品产品照
- 是否过度 polished

--------------------------------------------------
## 8. Materiality Check
--------------------------------------------------

检查：

- surface texture
- wear
- reflections
- material plausibility
- CGI feel

--------------------------------------------------
## 9. Context Check
--------------------------------------------------

检查：

- object 是否真的存在于可信空间
- 环境是否无关
- 是否被摄影棚化
- 是否有足够现实语境

--------------------------------------------------
## 10. AI Artifact Check
--------------------------------------------------

检查：

- distorted object structure
- impossible reflections
- impossible materials
- duplicated small details
- meaningless symbols
- fake branding
- malformed text

--------------------------------------------------
## 11. Reference Similarity Check
--------------------------------------------------

不是要求复制某张 Reference。

而是判断：

生成图是否仍然属于同一个 visual family。

明确：

“style-family similarity > literal composition copying”

--------------------------------------------------
## 12. Revision Guidance
--------------------------------------------------

针对常见失败建立：

Failure
Likely Cause
Revision Direction

例如：

Too commercial
→ lighting too polished / background too clean
→ reduce studio feel, restore lived-in material context

--------------------------------------------------
八、规则之间必须保持一致
--------------------------------------------------

完成三个文件后，进行 cross-check：

visual_rules.md
↕
prompt_rules.md
↕
quality_rules.md

确保：

每一个核心 visual rule：

至少能够在 prompt_rules 中被表达，
并且能够在 quality_rules 中被检测。

例如：

如果 visual_rules 规定：

“Materiality is core.”

那么：

prompt_rules 必须告诉 Prompt 如何表达 materiality。

quality_rules 必须告诉 QA 如何判断 materiality 是否成功。

禁止出现：

Visual Rule 存在
但 Prompt 无法实现
或 QA 无法检查

的情况。

--------------------------------------------------
九、不要过度工程化
--------------------------------------------------

这三个文件的目标是：

清晰、可执行、稳定。

不是：

为了显得专业而制造大量规则。

请主动：

- 删除重复规则
- 合并高度相似规则
- 避免同义反复
- 避免多层抽象术语
- 避免过度细碎参数
- 避免没有 Reference 支持的精确数值

一个规则如果不能：

帮助生成
或
帮助判断结果

就不应该进入正式规格。

--------------------------------------------------
十、输出目录
--------------------------------------------------

如果不存在：

image-broll-object/System/

创建该目录。

最终生成：

image-broll-object/
│
├── References/
├── reference_set_audit.md
├── reference_analysis.md
│
└── System/
    ├── visual_rules.md
    ├── prompt_rules.md
    └── quality_rules.md

不要创建其他无关文件。

--------------------------------------------------
十一、重要限制
--------------------------------------------------

1. 不要修改 References。
2. 不要修改 reference_set_audit.md。
3. 不要修改 reference_analysis.md。
4. 不要创建 SKILL.md。
5. 不要创建 Tests。
6. 不要生成图片。
7. 不要联网搜索。
8. 不要加入 Usage Contract。
9. 不要定义何时调用 Skill。
10. 不要加入视频剪辑规则。
11. 不要加入 Camera Motion。
12. 不要加入 LUT。
13. 不要加入 Transition。
14. 不要凭空加入摄影参数。
15. 不要因为个人审美修改 Reference-derived visual identity。
16. 不要把规则写成产品摄影最佳实践。
17. 不要把规则写成通用 still-life photography 教程。
18. 所有规则必须服务于 image-broll-object 这一具体视觉家族。

--------------------------------------------------
十二、完成后的自检
--------------------------------------------------

提交前检查：

- 是否读取了全部必要输入；
- 是否严格依据 Reference Analysis；
- 是否创建了 visual_rules.md；
- 是否创建了 prompt_rules.md；
- 是否创建了 quality_rules.md；
- 是否区分 MUST / SHOULD / MAY / AVOID / DO NOT；
- 是否把 description 转成了 execution specification；
- 是否明确处理了 subject；
- 是否明确处理了 composition；
- 是否明确处理了 environment；
- 是否明确处理了 lighting；
- 是否明确处理了 color；
- 是否重点处理了 materiality；
- 是否处理了 imperfection；
- 是否处理了 realism；
- 是否处理了 visual density；
- 是否处理了 negative space；
- 是否处理了 anti-patterns；
- 是否建立了 prompt vocabulary；
- 是否识别了 risky vocabulary；
- 是否建立了 quality pass/fail；
- 是否检查了 commercial contamination；
- 是否检查了 CGI / AI artifact；
- 是否确保 visual / prompt / quality 三层规则可互相映射；
- 是否没有创建 SKILL.md；
- 是否没有加入 Usage Contract；
- 是否没有提前开始测试。

如果任何一项未完成，请先补全再结束任务。
