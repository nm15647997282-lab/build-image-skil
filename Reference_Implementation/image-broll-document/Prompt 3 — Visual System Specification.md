
你现在要为 AI 图片 B-roll Skill：

image-broll-document

执行 Phase 2：

Prompt 3 — Visual System Specification

本任务的目标是：

基于已经完成的：

1. image-broll-document/References/
2. image-broll-document/reference_set_audit.md
3. image-broll-document/reference_analysis.md

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

image-broll-document/References/

image-broll-document/reference_set_audit.md

image-broll-document/reference_analysis.md

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

不要自行引入外部“档案风”“复古风”“老照片风”知识覆盖现有分析。

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
三、本 Skill 的视觉职责边界
--------------------------------------------------

image-broll-document 的视觉对象是：

以旧照片、纸本残片、私人档案、纸质记忆载体、历史痕迹或类似 archival paper artifact 为视觉主体的图片型 B-roll。

这里的 “document” 不意味着：

- 生成真实可读论文正文；
- 生成真实报告；
- 生成可验证历史文件；
- 生成精确引文；
- 生成新闻原文；
- 生成带有准确来源和长段文字的文档。

本 Skill 不承担：

readable document generation
quotation rendering
source verification
evidence reproduction

这些属于其他 Skill 或真实素材系统。

本 Skill 只负责：

“纸本对象本身的视觉呈现”。

--------------------------------------------------
四、本 Prompt 不负责的内容
--------------------------------------------------

不要定义：

- 什么时候调用 image-broll-document
- 什么语义触发它
- Asset Agent 如何路由
- 与 image-broll-quote 的路由
- 与真实档案素材的路由
- 与 image-broll-object 的路由
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

“当系统已经决定要生成 image-broll-document 时，这张图具体应该如何生成。”

--------------------------------------------------
五、核心转换原则
--------------------------------------------------

### 1. 从描述性语言转换为执行性规则

reference_analysis 中可能存在：

“Substantial negative space appears consistently across the core references and contributes strongly to the restrained archival presentation.”

这属于描述。

visual_rules.md 中应转换成类似：

“Preserve substantial negative space around the paper artifact as a default compositional condition. Avoid dense multi-paper filling unless supported by the selected subtype.”

但：

不要机械把所有分析改成 “Always”。

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
= 默认遵守，但允许受 artifact subtype 影响。

MAY
= References 支持的可选变化。

AVOID
= 容易跑偏，应尽量避免。

DO NOT
= 明显违反核心视觉语言。

不要滥用 MUST 和 DO NOT。

只有 Reference Analysis 的 High Confidence / Invariant Characteristics 才适合成为 MUST。

--------------------------------------------------
六、输出 1：visual_rules.md
--------------------------------------------------

生成：

image-broll-document/System/visual_rules.md

建议结构如下：

# image-broll-document — Visual Rules

## 1. Visual Objective

用一段简短文字定义：

这个 Skill 要稳定生成什么样的静态纸本档案 / 记忆物件画面。

必须来自 reference_analysis 的 Final Visual Definition。

不要重新发明风格命名。

--------------------------------------------------
## 2. Rule Priority
--------------------------------------------------

根据 reference_analysis 确定优先级。

可考虑：

1. Paper artifact physicality
2. Archival / memory character
3. Negative space
4. Restrained composition
5. Natural aging
6. Material realism
7. Quiet background
8. Lighting restraint
9. Decorative styling avoidance
10. Text non-dominance

但最终顺序必须由 Reference Analysis 支持。

--------------------------------------------------
## 3. Artifact Rules
--------------------------------------------------

定义：

- 主体应如何被呈现
- 单张照片 / 多张照片 / 纸本残片之间的关系
- artifact 是否应保持明确主体性
- 是否允许卡片、装裱、纸片、旧照片等变化
- 是否允许多件组合
- 多件组合的复杂度
- 主体是否应被当作“物理物件”而非平面贴图

重点强调：

artifact 是现实中的纸本对象。

不是：

- 版式元素
- 平面海报组件
- 数字 collage element
- fake historical document mockup

--------------------------------------------------
## 4. Artifact Treatment Rules
--------------------------------------------------

定义：

- 平放
- 贴附
- 叠放
- 轻微倾斜
- 装裱
- 局部遮挡
- 撕裂
- 卷边
- 折痕

分别哪些属于：

Default
Allowed Variation
Avoid

不要因为某几张图存在撕裂，就把“破损”写成所有输出必备条件。

--------------------------------------------------
## 5. Composition Rules
--------------------------------------------------

将 reference_analysis 中构图规律转换成规则。

包括：

- 居中 / 近居中 / 偏置
- 单一主体 vs 少量组合
- 主体角度
- 边缘关系
- 是否允许强烈透视
- 是否允许设计化拼贴
- 是否允许对角线堆叠
- 是否允许复杂 multi-layer composition

重点保持：

克制、安静、低密度。

但如果 References 不支持，不要强行写入。

--------------------------------------------------
## 6. Artifact-to-Frame Ratio
--------------------------------------------------

定义：

- 主体通常是 small / moderate / dominant
- 是否允许 frame-filling
- 是否需要保留背景
- 是否需要明显呼吸空间

如果 Reference 足够支持，可给宽松范围。

否则使用相对描述，不伪造精确百分比。

--------------------------------------------------
## 7. Negative Space Rules
--------------------------------------------------

这是 image-broll-document 的核心模块之一。

定义：

- 留白的重要程度
- 留白是否默认保留
- 留白如何围绕 artifact 分布
- 留白是否承担“被保存 / 被观察 / 被留下”的视觉效果
- 如何避免极端设计极简
- 如何避免“主体很小只是为了好看”的空洞构图

特别明确：

negative space 应服务：

archival restraint
memory isolation
visual breathing room

而不是纯 decorative minimalism。

--------------------------------------------------
## 8. Background Rules
--------------------------------------------------

定义：

- 墙面
- 卡纸
- 布面
- 桌面
- 纸面
- 中性平面

哪些属于常见或允许变化。

规定：

- 背景复杂度
- 材质感
- 颜色关系
- 是否低干扰
- 是否允许明显环境空间
- 是否允许过度精致 studio set

避免：

- scrapbook background
- decorative collage surface
- highly styled stationery setup
- fake vintage desk scene

--------------------------------------------------
## 9. Surface / Materiality Rules
--------------------------------------------------

这是核心模块。

定义：

- 照片纸质感
- 普通纸张
- 卡纸
- 布料
- 墙面
- 胶带 / 装裱等辅助材质

强调：

- 纸张必须有真实厚度感
- 边缘必须有物理存在感
- 表面不能像数字贴图
- 纹理不能过度增强
- 反光不能像塑料 CGI
- artifact 与背景必须存在可信接触关系

--------------------------------------------------
## 10. Aging Rules
--------------------------------------------------

定义：

- 泛黄
- 褪色
- 磨损
- 折痕
- 边缘损耗
- 污渍
- 斑点

分别哪些：

SHOULD
MAY
AVOID

重点：

老化必须：

natural
restrained
physically plausible

避免：

- exaggerated antique effect
- fake sepia filter
- heavy distressed texture
- artificial grunge overlay
- theatrical decay

--------------------------------------------------
## 11. Damage / Imperfection Rules
--------------------------------------------------

定义：

- 撕裂
- 缺角
- 卷边
- 胶带痕迹
- 表面划痕
- 边缘破损

不要强迫所有图都“残破”。

必须区分：

natural wear
vs
aesthetic distressing

规则应确保：

“时间痕迹”不变成“故意做旧表演”。

--------------------------------------------------
## 12. Photograph Treatment Rules
--------------------------------------------------

如果主体是旧照片：

定义：

- 黑白
- 褪色彩色
- 棕褐
- 低饱和
- 边框
- 白边
- 印刷颗粒

哪些属于：

Default
Allowed Variation
Avoid

特别明确：

照片内容本身不能完全压过：

“照片作为纸本对象”的物理存在。

--------------------------------------------------
## 13. Lighting Rules
--------------------------------------------------

定义：

- 光线类型
- 光线方向
- 阴影
- 高光
- 纸张纹理可见性
- 是否允许戏剧化
- 是否允许商业棚拍感

重点：

光线要帮助看见：

- 纸张厚度
- 边缘
- 折痕
- 表面纹理
- 贴附关系

而不是制造 cinematic drama。

--------------------------------------------------
## 14. Color Rules
--------------------------------------------------

定义：

- 饱和度
- 色温
- 中性色倾向
- 纸张颜色
- 黑白照片与褪色彩照的变化
- 背景与主体的色彩关系

如果 Reference Analysis 没有固定 palette：

明确：

No fixed color palette; preserve the restrained, low-interference tonal character derived from the references.

不要把“sepia”误设为默认。

--------------------------------------------------
## 15. Contrast / Tonal Range Rules
--------------------------------------------------

定义：

- 对比强度
- 黑位
- 高光
- fading
- 层次

重点避免：

“复古滤镜感”成为主要风格来源。

如果 Reference 的旧感主要来自：

material aging

而不是：

color grading

应明确写入。

--------------------------------------------------
## 16. Depth / Focus Rules
--------------------------------------------------

定义：

- 主体清晰度
- 背景虚化程度
- 是否允许浅景深
- 是否需要纸张边缘清晰
- 是否允许 macro look
- 是否允许强 bokeh

--------------------------------------------------
## 17. Visual Density Rules
--------------------------------------------------

定义：

- 默认 artifact 数量
- 可接受组合数量
- 叠放复杂度
- 背景元素密度

重点防止：

- scrapbook
- dense collage
- memory board
- journal spread

--------------------------------------------------
## 18. Typography Presence Rules
--------------------------------------------------

这是本 Skill 的关键边界。

定义：

- 文字如果出现，应处于什么地位
- 是否允许少量日期、编号、手写痕迹、标签
- 文字是否必须非主体
- 是否允许大段可读文本
- 是否允许 quote-like composition

明确：

DO NOT turn readable text into the primary visual content.

本 Skill 不负责：

精确引文
真实报告正文
可读文献展示

--------------------------------------------------
## 19. Human Content Inside Artifact Rules
--------------------------------------------------

如果照片里有人物：

定义：

- 人物是照片内部内容
- 不应把整个画面转成真人肖像
- 人物内容可服务 memory / archive character
- 人物不应改变“paper artifact is the primary visual object”这一原则

--------------------------------------------------
## 20. Emotional Tone Rules
--------------------------------------------------

把 reference_analysis 中的情绪气质转换成：

- 应保持的感受
- 通过哪些视觉因素实现
- 不应通过哪些夸张手段实现

例如：

quiet
restrained
intimate
fragile
archival
private

但具体词必须依据 Reference Analysis。

避免：

- melodramatic nostalgia
- sentimental cliché
- “伤感滤镜”
- overly cinematic melancholy

--------------------------------------------------
## 21. Authenticity / Realism Rules
--------------------------------------------------

规定：

- 纸张物理逻辑
- 老化逻辑
- 光线逻辑
- 背景接触逻辑
- 阴影逻辑
- 材质逻辑
- artifact 几何
- 贴附 / 叠放关系

避免：

- floating paper
- impossible shadow
- fake printed texture
- repeated AI damage pattern
- digital mockup look

--------------------------------------------------
## 22. Archive / Memory Character Rules
--------------------------------------------------

把 reference_analysis 中“为什么有记忆感 / 档案感”转换成明确视觉原则。

重点定义：

这种感受应该来自：

- object age
- material trace
- scale
- negative space
- restrained presentation
- low visual density
- physical realism

而不是来自：

- sepia filter
- fake handwriting
- fake stamps
- decorative tape
- vintage stickers
- retro typography

--------------------------------------------------
## 23. Allowed Variation
--------------------------------------------------

明确列出：

哪些变化仍属于同一视觉家族。

每项说明：

Variable
Allowed range
What must remain stable

例如：

Artifact type:
May vary between loose photograph, mounted photograph, paper fragment
But physical paper-object character must remain dominant

--------------------------------------------------
## 24. Invariants
--------------------------------------------------

从 reference_analysis 的 Invariant Characteristics 转换成正式规则。

这是视觉系统最高优先级。

数量不要过多。

建议控制在：

5–12 条。

--------------------------------------------------
## 25. Anti-patterns
--------------------------------------------------

将已确认 Anti-patterns 转换成明确规则。

重点包括：

- scrapbook
- moodboard collage
- memory board
- retro poster
- vintage graphic design
- decorative stationery
- journal spread
- excessive tape / sticker styling
- fake antique styling
- exaggerated distressed texture
- fake newspaper layout
- fake historical evidence
- AI gibberish text
- quote card
- typography-led composition
- dense paper collage
- cinematic archive drama
- generic sepia nostalgia
- sentimental vintage aesthetic

每个 anti-pattern 尽量说明：

“为什么它破坏当前视觉语言”。

--------------------------------------------------
七、输出 2：prompt_rules.md
--------------------------------------------------

生成：

image-broll-document/System/prompt_rules.md

这个文件专门解决：

“如何把 visual_rules 转换成稳定的 image-generation prompt。”

不要生成具体 production prompt。

要生成：

Prompt Construction System。

推荐结构：

# image-broll-document — Prompt Rules

## 1. Prompt Objective

说明：

Prompt 的任务不是创造新的 vintage / archival 风格，

而是：

把具体 paper artifact subject 映射进已冻结视觉系统。

--------------------------------------------------
## 2. Prompt Information Hierarchy
--------------------------------------------------

建议规定 Prompt 信息顺序，例如：

1. Artifact type
2. Physical state
3. Placement / treatment
4. Background
5. Composition / negative space
6. Lighting
7. Paper materiality
8. Aging / imperfection
9. Color / tonal character
10. Archive / memory mood
11. Anti-style constraints

但最终必须根据 Visual Rules 调整。

--------------------------------------------------
## 3. Artifact Description Rules
--------------------------------------------------

规定如何描述：

- old photograph
- mounted photo
- torn photo
- faded print
- paper fragment
- small archival card

以及：

- size
- orientation
- edge condition
- surface state
- aging
- mounting state
- stacking relation

避免抽象、诗意但无法执行的描述。

--------------------------------------------------
## 4. Physical State Vocabulary
--------------------------------------------------

建立适合的描述词：

- slightly worn
- faded
- creased
- softly curled edge
- restrained surface aging
- natural paper wear

并区分：

Preferred
Conditional
Risky
Avoid

--------------------------------------------------
## 5. Aging Vocabulary
--------------------------------------------------

重点建立：

自然老化的词汇系统。

需要区分：

Preferred:
restrained aging
subtle fading
natural edge wear

Risky:
vintage
antique
distressed

Avoid:
heavily distressed
grunge texture
ancient parchment
dramatic decay

如果某些词不适合 References，请替换。

--------------------------------------------------
## 6. Placement Vocabulary
--------------------------------------------------

规定如何描述：

- lying flat
- lightly mounted
- gently overlapping
- slightly angled
- attached to a neutral surface

并避免：

- collage
- scrapbook arrangement
- decorative layout

--------------------------------------------------
## 7. Composition Vocabulary
--------------------------------------------------

建立推荐描述方式。

例如：

- restrained composition
- generous negative space
- quiet centered presentation
- slightly off-center archival placement

但只能保留 Reference 支持的表达。

--------------------------------------------------
## 8. Background Vocabulary
--------------------------------------------------

建立：

Preferred
Conditional
Avoid

例如可能包括：

Preferred:
neutral paper surface
muted fabric background
quiet wall surface

Avoid:
ornamental desk styling
decorative scrapbook background
busy vintage tabletop

具体以 Visual Rules 为准。

--------------------------------------------------
## 9. Lighting Vocabulary
--------------------------------------------------

建立：

Preferred wording
Conditional wording
Avoid wording

重点避免：

dramatic cinematic lighting
museum spotlight
commercial studio gloss

如果这些不符合 References。

--------------------------------------------------
## 10. Materiality Vocabulary
--------------------------------------------------

规定如何描述：

- paper fibers
- matte photographic paper
- subtle surface wear
- softened edges
- slight physical curl
- realistic paper thickness

防止结果变成：

- flat digital print
- Photoshop mockup
- CGI card
- plastic-looking paper

--------------------------------------------------
## 11. Color / Tonal Vocabulary
--------------------------------------------------

规定：

- low saturation
- faded black-and-white
- muted color print
- warm neutral paper
- restrained tonal range

哪些可用。

特别避免：

把 sepia 当作通用关键词。

--------------------------------------------------
## 12. Archive / Memory Vocabulary
--------------------------------------------------

定义：

哪些词有助于表达：

- archival
- private
- memory fragment
- preserved
- found
- intimate

哪些词容易导致：

- sentimental nostalgia
- scrapbook
- cinematic melancholy
- retro poster

--------------------------------------------------
## 13. Typography Handling
--------------------------------------------------

规定：

如果 artifact 上出现文字：

- 应如何描述成 incidental
- 如何避免 AI 自动生成大量乱码
- 如何避免变成 quote card
- 如何避免文字成为主视觉

如果生成任务不需要文字：

Prompt 应避免主动要求 detailed readable text。

--------------------------------------------------
## 14. Risky Vocabulary
--------------------------------------------------

建立表格：

| Word / Phrase | Risk | Safer Alternative |

重点检查：

vintage
retro
nostalgic
archival
ephemera
scrapbook
collage
antique
cinematic
moody
historical

这些词可能有很大歧义。

不要简单禁止。

要分析：

哪些可以用，
哪些需要限定，
哪些最好替换。

--------------------------------------------------
## 15. Negative Prompt / Avoidance Strategy
--------------------------------------------------

如果模型支持 negative prompt：

定义 anti-style vocabulary。

如果不支持：

说明如何把这些约束放进主 Prompt。

重点可包括：

- scrapbook
- collage
- retro poster
- fake handwriting
- vintage stickers
- decorative tape
- dense paper layering
- AI gibberish text
- dramatic sepia
- digital mockup

具体依据 visual_rules。

--------------------------------------------------
## 16. Prompt Compression Rules
--------------------------------------------------

Prompt 不应无限堆叠：

archival
nostalgic
old
vintage
retro
aged
antique

这类同义词。

规定：

- 哪些信息必须保留
- 哪些只选一个
- 哪些容易产生冲突
- 哪些描述应该通过物理属性表达，而不是形容词

重点：

尽量用：

physical evidence

替代：

abstract vintage adjectives。

--------------------------------------------------
## 17. Prompt Template Logic
--------------------------------------------------

只定义结构：

[artifact]
+
[physical state]
+
[placement]
+
[background]
+
[composition / negative space]
+
[lighting]
+
[paper materiality]
+
[color / tonal character]
+
[archive / memory character]
+
[style guardrails]

不要在这里创建最终 production prompt。

--------------------------------------------------
## 18. Variation Handling
--------------------------------------------------

说明：

当 artifact 不同时：

- 哪些字段变化
- 哪些字段仍需保持
- 如何处理单张 / 双张 / damaged / mounted subtype

--------------------------------------------------
## 19. Prompt Failure Patterns
--------------------------------------------------

列出容易导致：

- scrapbook
- collage
- fake antique
- fake historical evidence
- retro poster
- journal spread
- sentimental nostalgia
- AI text
- digital mockup

的 Prompt 写法。

--------------------------------------------------
八、输出 3：quality_rules.md
--------------------------------------------------

生成：

image-broll-document/System/quality_rules.md

这个文件用于：

判断最终生成图是否属于 image-broll-document。

它不是 Usage Contract。

只负责视觉质量评估。

推荐结构：

# image-broll-document — Quality Rules

## 1. Evaluation Goal

定义：

QA 判断的不是：

“这张图复不复古”

而是：

“它是否忠实复现 Reference-derived archival paper artifact visual system。”

--------------------------------------------------
## 2. Evaluation Dimensions
--------------------------------------------------

至少包括：

- Artifact clarity
- Paper physicality
- Composition
- Negative space
- Background restraint
- Aging realism
- Damage restraint
- Lighting
- Color / tonal restraint
- Materiality
- Archive / memory character
- Typography non-dominance
- Decorative contamination
- AI artifact risk

--------------------------------------------------
## 3. Pass Criteria
--------------------------------------------------

定义一张合格图应满足什么。

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

- scrapbook layout
- dense decorative collage
- fake antique parchment
- obvious retro poster design
- AI-generated gibberish text dominating image
- quote-card composition
- impossible paper geometry
- floating artifact
- exaggerated distressed effect
- sentimental vintage cliché
- digital mockup look

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

可建立简单评分系统。

例如 1–5。

但不要制造伪精确。

如使用评分：

明确哪些维度是一票否决项。

--------------------------------------------------
## 7. Paper Physicality Check
--------------------------------------------------

检查：

- paper thickness
- edge realism
- curl
- fold
- texture
- mounting relation
- shadow
- contact with background

--------------------------------------------------
## 8. Aging Check
--------------------------------------------------

检查：

- 是否自然
- 是否克制
- 是否像统一滤镜
- 是否过度 grunge
- 是否出现重复 AI 老化纹理

--------------------------------------------------
## 9. Negative Space Check
--------------------------------------------------

检查：

- 是否保留足够呼吸
- 是否变成纯设计极简
- 主体是否太小导致失去视觉信息
- 留白是否仍服务 archival / memory character

--------------------------------------------------
## 10. Decorative Contamination Check
--------------------------------------------------

单独检查：

- scrapbook
- stickers
- decorative tape
- stamps
- moodboard
- stationery styling
- journal spread
- collage layering
- typography decoration

--------------------------------------------------
## 11. Typography Check
--------------------------------------------------

检查：

- 是否出现大段乱码
- 是否文字抢主体
- 是否变成 quote
- 是否变成 fake document rendering
- incidental text 是否仍然只是 material trace

--------------------------------------------------
## 12. Archive / Memory Character Check
--------------------------------------------------

判断：

画面的 archive / memory 感是否来自：

- material
- aging
- scale
- negative space
- quiet presentation

还是错误来自：

- sepia filter
- fake stamp
- retro font
- dramatic nostalgia

--------------------------------------------------
## 13. AI Artifact Check
--------------------------------------------------

检查：

- impossible text
- malformed photographs
- duplicated borders
- impossible paper folds
- inconsistent shadows
- floating paper
- impossible overlap
- warped photo geometry
- repeated damage texture

--------------------------------------------------
## 14. Reference Similarity Check
--------------------------------------------------

不是要求复制具体 Reference。

而是判断：

生成图是否仍属于同一个 visual family。

明确：

style-family similarity > literal composition copying

--------------------------------------------------
## 15. Revision Guidance
--------------------------------------------------

针对常见失败建立：

Failure
Likely Cause
Revision Direction

例如：

Too scrapbook-like
→ too many layered paper elements / decorative accessories
→ reduce artifact count, simplify composition, restore negative space

Too fake-antique
→ aging language too aggressive
→ reduce distressing, restore restrained material wear

Too much text
→ artifact described as readable document
→ reduce typography role, return focus to paper object

--------------------------------------------------
九、三层规则必须互相映射
--------------------------------------------------

完成三个文件后进行 cross-check：

visual_rules.md
↕
prompt_rules.md
↕
quality_rules.md

确保：

每一个核心 Visual Rule：

都能在 prompt_rules 中被实现，
并且能在 quality_rules 中被检测。

例如：

如果 visual_rules 规定：

“Natural aging is core.”

那么：

prompt_rules 必须说明如何用物理描述表达 natural aging。

quality_rules 必须说明如何区分：

natural aging
vs
fake antique styling。

如果 visual_rules 规定：

“Typography must remain secondary.”

那么：

prompt_rules 必须告诉 Prompt 如何弱化文字。

quality_rules 必须能检查文字是否抢主体。

禁止出现：

Visual Rule 存在
但 Prompt 无法表达
或 QA 无法检测。

--------------------------------------------------
十、不要过度工程化
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
- 避免没有 Reference 支持的精确数值
- 避免把所有 aging 特征都做成硬规则
- 避免把所有 paper artifact 都要求“破旧”

一个规则如果不能：

帮助生成
或
帮助判断结果

就不应该进入正式规格。

--------------------------------------------------
十一、输出目录
--------------------------------------------------

如果不存在：

image-broll-document/System/

创建该目录。

最终生成：

image-broll-document/
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
十二、重要限制
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
16. 不要把规则写成“复古摄影最佳实践”。
17. 不要把规则写成通用 archival aesthetic 教程。
18. 不要把可读文字生成职责加入本 Skill。
19. 不要让 scrapbook / collage / vintage graphic design 偷偷进入默认视觉语言。
20. 所有规则必须服务于 image-broll-document 这一具体 Reference-derived visual family。

--------------------------------------------------
十三、完成后的自检
--------------------------------------------------

提交前检查：

- 是否读取了全部必要输入；
- 是否严格依据 Reference Analysis；
- 是否创建了 visual_rules.md；
- 是否创建了 prompt_rules.md；
- 是否创建了 quality_rules.md；
- 是否区分 MUST / SHOULD / MAY / AVOID / DO NOT；
- 是否把 description 转成 execution specification；
- 是否明确处理了 artifact；
- 是否明确处理了 artifact treatment；
- 是否明确处理了 composition；
- 是否重点处理了 negative space；
- 是否重点处理了 materiality；
- 是否重点处理了 aging；
- 是否处理了 damage / imperfection；
- 是否处理了 background；
- 是否处理了 lighting；
- 是否处理了 color / tonal range；
- 是否处理了 typography non-dominance；
- 是否处理了 archive / memory character；
- 是否处理了 authenticity / realism；
- 是否处理了 anti-patterns；
- 是否建立了 prompt vocabulary；
- 是否识别了 risky vocabulary；
- 是否建立了 quality pass/fail；
- 是否检查了 scrapbook / collage contamination；
- 是否检查了 fake antique contamination；
- 是否检查了 AI text contamination；
- 是否检查了 digital mockup / fake paper physicality；
- 是否确保 visual / prompt / quality 三层规则可互相映射；
- 是否没有创建 SKILL.md；
- 是否没有加入 Usage Contract；
- 是否没有提前开始测试。

如果任何一项未完成，请先补全再结束任务。


