
你现在要为 AI 图片 B-roll Skill：

image-broll-document

执行 Phase 1 的第二步：

Prompt 2 — Reference Analysis

本任务的目标是：

基于已经完成审核的 References 和 reference_set_audit.md，
系统提炼这组图片真正共享的视觉语言，
生成一份完整、结构化、可供后续 Visual System Specification 使用的：

reference_analysis.md

本 Prompt 只负责回答：

“这组 References 的视觉语言到底是什么？”

不要提前进入：

- visual_rules.md
- prompt_rules.md
- quality_rules.md
- SKILL.md
- Tests
- Prompt Template

--------------------------------------------------
一、必须读取的输入
--------------------------------------------------

请完整读取并综合：

1. image-broll-document/References/
2. image-broll-document/reference_set_audit.md

如果 Prompt 1 已经给出了：

- Core References
- Supporting References
- Ambiguous References
- Outliers
- Recommended Reference Set for Prompt 2

请严格按照该审核结果决定分析权重。

分析优先级：

Core References
↓
Supporting References
↓
Ambiguous References（仅在有价值时参考）
↓
Outliers（不得用于定义核心风格，只可作为边界对照）

--------------------------------------------------
二、任务目标
--------------------------------------------------

你需要回答的核心问题是：

1. image-broll-document 的核心视觉身份是什么？
2. References 是如何呈现旧照片、纸本残片、档案遗物和记忆材料的？
3. 哪些视觉属性构成这一风格的稳定核心？
4. 哪些属性允许变化？
5. 这些画面为什么像“被留下来的纸本痕迹”，而不是普通复古设计？
6. 画面如何通过纸张、老化、留白、背景和物理质感形成档案感与记忆感？
7. References 中是否存在多个兼容的视觉子类型？
8. 哪些特征是风格核心，哪些只是某张图的具体内容？
9. 哪些视觉方向一旦出现，就会让最终 Skill 跑向 scrapbook、retro design、fake archive 或 generic vintage aesthetic？

注意：

这里需要做的是“视觉分析”。

不是生成规则。
不是写 prompt。
不是设计使用场景。
不是定义什么时候调用该 Skill。

--------------------------------------------------
三、关于 image-broll-document 的分析边界
--------------------------------------------------

image-broll-document 的研究对象是：

以旧照片、纸本残片、私人档案、纸质记忆载体、历史痕迹或类似 paper artifact 为视觉主体的图片型 B-roll。

这里的 “document” 不等于：

- 可读的论文正文；
- 真实报告截图；
- 可验证历史文件；
- 精确引用的书页；
- 新闻报道原文；
- 需要准确文字内容的文档。

这些属于：

- quote
- real evidence
- source-based visual

不属于本 Skill。

本 Skill 更接近：

- old photograph
- archival paper artifact
- memory fragment
- found photograph
- torn paper artifact
- faded print
- mounted photograph
- personal archive
- paper relic

但：

不要从这些标签倒推最终风格。

最终视觉语言必须由 References 本身决定。

--------------------------------------------------
四、分析方法
--------------------------------------------------

### 1. Reference-first

所有结论必须有 Reference 支撑。

不要使用类似：

“档案风格通常应该……”

这样的外部常识来替代实际观察。

可以使用摄影、设计、材质和档案相关术语描述画面，
但不能补写 References 没有提供的视觉事实。

如果某项无法从当前 Reference Set 判断，明确写：

Insufficient evidence.

---

### 2. 区分三个层级

每一个视觉结论都尽量判断属于：

A. Core Visual Identity
B. Allowed Variation
C. Incidental Detail

其中：

Core Visual Identity
= 多数核心参考共享，且一旦丢失会明显改变整体气质。

Allowed Variation
= 可以变化，但仍属于同一视觉家族。

Incidental Detail
= 只属于个别图片，不应该进入核心定义。

---

### 3. 区分“纸本内容”和“视觉语言”

不要把：

- 某张照片里的人物
- 某个地点
- 某种具体年代
- 某个字迹
- 某张纸上的具体内容

当成风格本身。

真正需要分析的是：

- 纸本对象如何被呈现
- 它与背景之间的关系
- 它是被放置、贴附、叠放还是破损呈现
- 主体占画面多少
- 留白如何存在
- 纸张和照片的物理质感如何被强调
- 老化是否自然
- 画面为什么有时间痕迹
- 为什么有私人记忆感或档案感
- 为什么不像设计拼贴或复古海报

--------------------------------------------------
五、必须完成的视觉分析维度
--------------------------------------------------

--------------------------------------------------
5.1 Core Visual Identity
--------------------------------------------------

首先用一段完整文字回答：

“这组 Reference 最核心的视觉身份是什么？”

不要只写几个形容词。

需要解释：

- 它主要让观众看到什么
- 这些纸本对象是如何被观看的
- 它更接近私人档案、记忆遗物、found object 还是设计作品
- 为什么画面有安静的人文感
- 为什么它不是普通的 vintage aesthetic
- 为什么它不是 scrapbook
- 为什么它不是 fake historical evidence

最后提炼 5–10 个核心关键词。

但关键词必须有后文支持。

--------------------------------------------------
5.2 Artifact Type
--------------------------------------------------

分析 References 中主要出现哪些纸本对象：

- 单张旧照片
- 多张照片
- 撕裂照片
- 泛黄照片
- 褪色彩色照片
- 装裱照片
- 卡片
- 纸本残片
- 信件式纸张
- 其他 archival artifact

不要把类型频率直接当作最终限制。

重点回答：

这些不同 artifact 是否仍共享同一种视觉语法？

--------------------------------------------------
5.3 Artifact Treatment
--------------------------------------------------

分析纸本对象本身如何被处理：

- 平放
- 贴在背景上
- 叠放
- 轻微倾斜
- 部分遮挡
- 撕裂
- 卷边
- 折痕
- 边缘磨损
- 表面褪色

判断：

这种处理更像：

A. natural archival object
B. deliberately styled vintage prop
C. designed collage element
D. memory artifact
E. historical document display

哪一种最接近核心 References？

--------------------------------------------------
5.4 Composition
--------------------------------------------------

分析：

- 居中程度
- 接近居中还是明显偏置
- 是否轻微倾斜
- 是否保持单一主体
- 是否存在两三件小规模组合
- 是否大量留白
- 是否有固定模板感
- 是否有视觉静止感
- 是否存在强烈设计构图

重点判断：

这些构图更强调：

- stillness
- intimacy
- fragility
- memory
- archive
- design

中的哪些？

--------------------------------------------------
5.5 Artifact-to-Frame Ratio
--------------------------------------------------

分析：

- 纸本主体通常占画面多少视觉权重
- 是否经常较小
- 是否允许主体成为画面主导
- 是否常有大面积背景
- 是否依赖负空间形成安静感
- 是否有 edge-to-edge 的情况

不要强行给精确百分比。

可以使用：

small / moderate / dominant / frame-filling

等相对描述。

--------------------------------------------------
5.6 Negative Space
--------------------------------------------------

这是本 Skill 的重点。

分析：

- 留白是否是稳定特征
- 留白如何分布
- 留白来自墙面、纸面、布面还是其他背景
- 留白是否让主体显得脆弱、孤立、被保存
- 留白是否构成“档案陈列感”或“私人记忆感”
- 是否存在模板化居中 + 四周留白

进一步判断：

这种留白属于：

- decorative minimalism
- visual breathing room
- archival presentation
- memory isolation
- editorial restraint

中的哪一种或哪几种。

--------------------------------------------------
5.7 Background
--------------------------------------------------

分析：

- 墙面
- 卡纸
- 布面
- 桌面
- 纸面
- 中性色平面
- 有纹理表面

重点分析：

- 背景是否低干扰
- 是否有明显材质
- 是否与主体形成色彩分离
- 是否过度精致
- 是否像摄影棚背景
- 是否像真实保存环境
- 是否只是“漂亮背景”

判断背景总体更接近：

- neutral archival support
- tactile surface
- editorial backdrop
- domestic surface
- designed set

哪一种？

--------------------------------------------------
5.8 Surface / Materiality
--------------------------------------------------

深入分析：

- 照片纸
- 普通纸张
- 卡纸
- 布料
- 墙面
- 纤维
- 胶带
- 装裱边框
- 纸张厚度
- 纸面反光

重点回答：

什么让这些纸本对象看起来具有：

- 物理存在感
- 触感
- 时间感
- 保存痕迹

而不是像数字贴图或 Photoshop mockup。

--------------------------------------------------
5.9 Aging
--------------------------------------------------

这是核心分析项。

分析 References 中出现的：

- 泛黄
- 褪色
- 折痕
- 撕裂
- 磨损
- 污渍
- 斑点
- 边缘卷曲
- 表面脱色
- 印刷退化

判断这些老化特征：

- Dominant
- Common
- Occasional
- Rare

重点区分：

A. naturally aged
B. restrained archival wear
C. deliberately distressed
D. exaggerated antique effect

分析核心 References 更接近哪一种。

--------------------------------------------------
5.10 Damage / Imperfection
--------------------------------------------------

分析：

- 撕裂是否常见
- 缺角是否常见
- 折痕是否明显
- 是否存在边缘破损
- 是否存在胶带或粘贴痕迹
- 是否有污损
- 是否存在极端残破

判断：

“破损感”是风格核心，
还是只是 allowed variation。

尤其注意：

不要把重度破损误判为必要条件。

--------------------------------------------------
5.11 Photograph Treatment
--------------------------------------------------

如果主体是旧照片，分析：

- 黑白
- 棕褐色
- 褪色彩色
- 低饱和
- 低对比
- 高对比
- 边框
- 白边
- 老式印刷颗粒

判断：

照片内容是否比“照片作为物件”更重要？

通常需要区分：

image content

和

physical photograph object

哪个是视觉主体。

--------------------------------------------------
5.12 Lighting
--------------------------------------------------

分析：

- 自然光 / 人工光
- 柔光 / 硬光
- 侧光 / 平光 / 顶光
- 阴影是否轻微
- 是否有局部高光
- 是否戏剧化
- 是否具有摄影棚感
- 是否存在强方向性

重点回答：

这种光线如何帮助呈现：

- 纸张纹理
- 边缘
- 折痕
- 撕裂
- 时间痕迹
- 安静气氛

--------------------------------------------------
5.13 Color Palette
--------------------------------------------------

分析：

- 米白
- 暖灰
- 蓝灰
- 棕色
- 纸张黄
- 亚麻色
- 低饱和冷色
- 黑白照片
- 褪色彩色照片

区分：

- stable palette
- allowed variation
- incidental color

特别判断：

色彩是否整体低饱和、褪色、克制，
还是 Reference 中其实存在更广泛变化。

--------------------------------------------------
5.14 Contrast / Tonal Range
--------------------------------------------------

分析：

- 高对比 / 低对比
- 阴影是否柔和
- 黑位是否压得很重
- 高光是否强
- 是否存在 faded tonal range
- 是否有 vintage filter 式统一色偏

重点区分：

自然老化导致的色调变化

vs

后期滤镜制造的“复古感”。

--------------------------------------------------
5.15 Depth / Focus
--------------------------------------------------

分析：

- 全清晰
- 浅景深
- 中景深
- 纸张主体与背景是否明显分离
- 边缘是否清晰
- 是否存在强 bokeh
- 是否像 macro photography

说明：

景深在这套视觉里承担什么作用。

--------------------------------------------------
5.16 Visual Density
--------------------------------------------------

分析：

- 单一纸本对象
- 双对象
- 少量叠放
- 多张照片
- 大量拼贴

判断整体更偏：

low visual density
moderate visual density
high visual density

特别检查：

多元素是否容易使风格滑向 scrapbook / collage。

--------------------------------------------------
5.17 Typography Presence
--------------------------------------------------

分析：

- 是否有文字
- 是否可读
- 是否只是背书、编号、批注、日期、手写痕迹
- 是否成为视觉主体
- 是否有大量排版
- 是否像 quote card

重点回答：

文字在 References 中扮演的是：

A. semantic content
B. incidental trace
C. material detail
D. design element

哪一种？

如果文字不是核心，请明确指出。

--------------------------------------------------
5.18 Human Content Inside the Artifact
--------------------------------------------------

如果旧照片里有人物：

分析人物内容的作用。

判断：

- 人物是否是照片内容
- 还是整个画面的现实主体
- 是否需要人物辨识
- 是否更强调私人记忆感
- 是否存在正式肖像 / 家庭照 / 日常快照差异

注意：

本 Skill 的主体应分析为：

“纸本照片这个物件”

而不是简单转成“人物肖像 Skill”。

--------------------------------------------------
5.19 Emotional Tone
--------------------------------------------------

分析真正稳定的情绪：

例如：

- quiet
- restrained
- intimate
- nostalgic
- fragile
- private
- melancholic
- warm
- archival
- distant
- sentimental

不要堆形容词。

必须解释：

这些情绪由哪些视觉因素实现：

- 留白
- 老化
- 褪色
- 小尺寸主体
- 材质
- 光线
- 背景
- 破损

--------------------------------------------------
5.20 Archival vs Decorative
--------------------------------------------------

这是关键章节。

请明确判断这组 References 更接近：

- archival artifact photography
- memory-object photography
- editorial archival still life
- found photograph presentation
- decorative vintage styling
- scrapbook
- retro graphic design
- collage

可以是混合类型。

必须解释：

为什么。

特别回答：

“它为什么不是 scrapbook？”

“它为什么不是普通 vintage aesthetic？”

“它为什么不是 retro poster design？”

--------------------------------------------------
5.21 Authenticity / Realism
--------------------------------------------------

分析：

- 纸张是否真实
- 老化是否可信
- 光线是否可信
- 是否像真实保存下来的物件
- 是否存在明显 AI 生成感
- 是否像数字 mockup
- 是否过度设计
- 是否过度做旧

重点判断：

References 所追求的是：

“真实旧物感”

还是

“审美化的旧物风”。

两者必须区分。

--------------------------------------------------
5.22 Memory / Archive Character
--------------------------------------------------

分析这组图为什么会产生：

- memory
- private archive
- historical trace
- personal relic
- found object
- preserved fragment

这样的感受。

不要只写情绪。

需要明确：

这种“记忆 / 档案感”是通过哪些视觉机制产生的。

--------------------------------------------------
5.23 Recurring Visual Patterns
--------------------------------------------------

汇总稳定出现的视觉模式。

建议表格：

| Pattern | Frequency | Importance | Confidence | Evidence |

Frequency：

Dominant
Common
Occasional
Rare

Importance：

Core
Supporting
Incidental

Confidence：

High
Medium
Low

--------------------------------------------------
5.24 Allowed Variation
--------------------------------------------------

总结哪些变化不会破坏风格。

例如可能包括：

- 单张 / 双张照片
- 黑白 / 褪色彩色
- 不同背景材质
- 不同程度破损
- 不同摆放角度
- mounted / loose / stacked

但必须以 References 为依据。

不要自行无限扩展。

--------------------------------------------------
5.25 Invariant Characteristics
--------------------------------------------------

这是整个 reference_analysis 中最重要的输出之一。

列出：

如果未来生成 image-broll-document，
无论 paper artifact 的具体内容如何变化，
哪些视觉属性仍然应该大体保持？

这里只提炼视觉核心。

不要转换成命令式规则。

例如：

错误：
“Always use large negative space.”

正确：
“Substantial negative space appears consistently across the core references and contributes strongly to the restrained archival presentation.”

--------------------------------------------------
5.26 Anti-patterns
--------------------------------------------------

根据 References 和 Prompt 1 的 audit，
分析哪些视觉方向明显不属于这个风格。

重点检查：

- scrapbook
- moodboard collage
- memory board
- retro poster
- vintage graphic design
- decorative stationery styling
- journal spread
- excessive tape/sticker styling
- overly distressed antique effect
- fake historical evidence
- fake newspaper/document design
- AI-generated gibberish text
- typography-led composition
- social-media quote card
- highly cinematic archive scene
- sepia cliché
- generic vintage aesthetic
- overly sentimental nostalgia
- dense multi-paper composition

注意：

这里只做视觉边界分析。

不要提前写成最终生成禁令。

--------------------------------------------------
5.27 Subtype Analysis
--------------------------------------------------

如果 Prompt 1 发现了 subtype，
进行深入分析。

可能包括：

- single archival photograph
- stacked photographs
- torn / damaged artifact
- mounted photograph
- faded color print
- labeled / handwritten artifact

每个 subtype 说明：

- 与核心视觉共享什么
- 独有变化是什么
- 是否属于 Allowed Variation
- 是否值得保留
- 是否真的构成独立视觉语言

如果没有 subtype：

明确写：

Single coherent visual family.

--------------------------------------------------
六、不要分析的内容
--------------------------------------------------

本 Prompt 不需要分析：

- 什么时候使用 image-broll-document
- 什么语义触发它
- 与 image-broll-quote 的系统路由
- 与真实档案素材的路由
- Asset Agent 如何调用
- 与 MG 的路由
- 视频剪辑窗口
- Camera Motion
- LUT
- Transition
- 使用频率
- 节奏

这些属于其他系统模块。

当前只研究：

静态图像本身的视觉语言。

--------------------------------------------------
七、输出文件
--------------------------------------------------

生成：

image-broll-document/reference_analysis.md

推荐结构：

# image-broll-document — Reference Analysis

## 1. Analysis Scope

说明：

- 使用了哪些 Core References
- 使用了哪些 Supporting References
- 排除了哪些 Outliers
- 是否存在证据不足

## 2. Core Visual Identity

## 3. Artifact Type

## 4. Artifact Treatment

## 5. Composition

## 6. Artifact-to-Frame Ratio

## 7. Negative Space

## 8. Background

## 9. Surface & Materiality

## 10. Aging

## 11. Damage & Imperfection

## 12. Photograph Treatment

## 13. Lighting

## 14. Color Palette

## 15. Contrast & Tonal Range

## 16. Depth / Focus

## 17. Visual Density

## 18. Typography Presence

## 19. Human Content Inside Artifact

## 20. Emotional Tone

## 21. Archival / Memory / Decorative Positioning

## 22. Authenticity & Realism

## 23. Memory / Archive Character

## 24. Recurring Visual Patterns

## 25. Allowed Variation

## 26. Invariant Characteristics

## 27. Anti-patterns

## 28. Subtype Analysis

## 29. Final Visual Definition

最后使用一段完整、准确、非营销化的文字，
定义 image-broll-document 的视觉风格。

不要只输出：

“quiet archival vintage photography”

而要写清楚：

- 它如何呈现纸本对象
- 它如何处理旧照片
- 它如何处理背景
- 它如何处理留白
- 它如何处理老化与破损
- 它如何形成真实档案感和记忆感
- 它为什么不是 scrapbook
- 它为什么不是 generic vintage aesthetic
- 它为什么不承担真实可读文档展示职责

## 30. Evidence Confidence

将主要结论分为：

High Confidence
Medium Confidence
Low Confidence / Insufficient Evidence

--------------------------------------------------
八、重要限制
--------------------------------------------------

1. 不要修改 References。
2. 不要删除或移动任何图片。
3. 不要修改 reference_set_audit.md。
4. 不要创建 visual_rules.md。
5. 不要创建 prompt_rules.md。
6. 不要创建 quality_rules.md。
7. 不要创建 SKILL.md。
8. 不要创建 Tests。
9. 不要生成图片。
10. 不要联网搜索额外 Reference。
11. 不要引入外部摄影师、品牌或流派作为风格核心，除非 References 明确支持。
12. 不要为了让分析显得专业而补写 References 无法支持的技术参数。
13. 不要自行指定焦段、光圈、ISO、色温等具体数值。
14. 不要把偶然的撕裂、胶带、手写、泛黄升级为硬性核心。
15. 不要把照片中的人物内容误当成本 Skill 的主体定义。
16. 不要把可读文字当作核心视觉职责。
17. 不要把该 Skill 分析成 quote / report / readable-document generator。
18. 如果证据不足，明确写 Insufficient evidence。
19. 不要提前把描述性分析转换成命令式生成规则。

--------------------------------------------------
九、完成后的自检
--------------------------------------------------

提交前逐项检查：

- 是否读取了 reference_set_audit.md；
- 是否按照 Core / Supporting / Outlier 权重分析；
- 是否完整考虑了全部有效 Reference；
- 是否明确区分 Core / Variation / Incidental；
- 是否分析了 artifact type；
- 是否分析了 artifact treatment；
- 是否分析了 composition；
- 是否重点分析了 negative space；
- 是否分析了 background；
- 是否深入分析了 materiality；
- 是否深入分析了 aging；
- 是否深入分析了 damage / imperfection；
- 是否分析了 photograph treatment；
- 是否分析了 lighting；
- 是否分析了 color；
- 是否分析了 typography presence；
- 是否区分了 archival 与 decorative；
- 是否区分了 natural aging 与 fake antique effect；
- 是否分析了 authenticity / realism；
- 是否解释了 memory / archive character；
- 是否输出了 recurring patterns；
- 是否输出了 allowed variation；
- 是否输出了 invariant characteristics；
- 是否输出了 anti-patterns；
- 是否处理了 subtype；
- 是否给出了 Final Visual Definition；
- 是否标注了 Evidence Confidence；
- 是否没有提前编写生成规则；
- 是否没有提前编写 SKILL.md；
- 是否没有加入 Usage Contract；
- 是否没有把本 Skill 错误定义为真实可读文档生成 Skill。

如果任何一项未完成，请补全后再结束任务。
