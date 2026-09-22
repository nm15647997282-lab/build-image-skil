
你现在要为 AI 图片 B-roll Skill：

image-broll-object

执行 Phase 1 的第二步：

Prompt 2 — Reference Analysis

本任务的目标是：

基于已经完成审核的 References 和 reference_set_audit.md，
系统提炼这组图片真正共享的视觉语言，
生成一份完整、结构化、可供后续 Visual System Specification 使用的：

reference_analysis.md

本 Prompt 只负责：

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

1. image-broll-object/References/
2. image-broll-object/reference_set_audit.md

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

1. image-broll-object 的核心视觉身份是什么？
2. References 在“如何呈现一个具体物件”这件事上，有哪些稳定规律？
3. 哪些视觉属性必须长期保持稳定？
4. 哪些属性允许变化？
5. 这些画面为什么不像普通产品摄影、广告摄影或装饰性静物？
6. 它如何通过构图、材质、光线、环境和不完美感形成独特气质？
7. References 中是否存在多个可兼容的视觉子类型？
8. 哪些特征是“风格核心”，哪些只是“内容变化”？
9. 哪些视觉方向一旦出现，就会让最终 Skill 明显跑偏？

注意：

这里需要做的是“视觉分析”。

不是生成规则。
不是写 prompt。
不是设计使用场景。
不是定义什么时候调用该 Skill。

--------------------------------------------------
三、关于 image-broll-object 的分析边界
--------------------------------------------------

image-broll-object 的研究对象是：

以具体实体物件为视觉主体的图片型 B-roll。

这里的 object 可以是：

- 日常用品
- 阅读用品
- 工作用品
- 消费物件
- 私人物件
- 制度性物件
- 具有社会或生活语义的物件

例如：

- 手机
- 闹钟
- 工牌
- 眼镜
- 钥匙
- 信用卡
- 小票
- 耳机
- 书
- 笔
- 药瓶
- 办公用品
- 生活用品

但：

不要从这些例子倒推出视觉风格。

视觉风格必须由 References 本身决定。

--------------------------------------------------
四、分析方法
--------------------------------------------------

### 1. Reference-first

所有结论必须有 Reference 支撑。

不要使用类似：

“好的 object photography 通常应该……”

这样的外部摄影常识来替代实际观察。

你可以使用摄影术语描述画面，
但不能用摄影常识补齐 References 没有提供的信息。

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
= 多数核心参考共享，且一旦丢失就会改变整体风格。

Allowed Variation
= 可以变化，但变化后仍属于同一视觉家族。

Incidental Detail
= 只属于个别图片，不应该进入风格定义核心。

---

### 3. 区分“物件内容”和“视觉语言”

不要把：

- 手机
- 眼镜
- 闹钟
- 信用卡
- 书

这些具体 subject 当成风格特征。

真正的视觉语言应该来自：

- 物件如何被观看
- 物件与环境如何建立关系
- 画面有多安静
- 主体是否被孤立
- 是否有使用痕迹
- 是否像“被观察到”
- 是否有人的生活痕迹
- 是否有广告化展示意图
- 是否有材质感
- 是否有编辑摄影感
- 是否有纪录感

--------------------------------------------------
五、必须完成的视觉分析维度
--------------------------------------------------

请至少从以下维度深入分析。

--------------------------------------------------
5.1 Core Visual Identity
--------------------------------------------------

首先用一段完整文字回答：

“这组 Reference 最核心的视觉身份是什么？”

不要只写几个形容词。

需要解释：

- 它在看什么
- 它如何看
- 它和普通静物摄影有何区别
- 它是否具有生活观察感、编辑感、纪录感或其他特征
- 物件为什么显得“有人文气质”
- 画面为什么不会像商品广告

最后提炼 5–10 个最核心关键词。

但关键词必须有后文支持。

--------------------------------------------------
5.2 Subject Treatment
--------------------------------------------------

分析：

- 物件通常是单一主体还是组合主体
- 主体是否明确
- 是否会出现辅助物
- 辅助物数量
- 辅助物与主物件之间是否存在明确关系
- 是否强调“被使用过”
- 是否存在磨损、折痕、指纹、划痕、生活痕迹
- 是否倾向完美、崭新、无瑕
- 是否存在刻意的产品英雄化

特别判断：

物件被呈现为：

A. Product
B. Prop
C. Evidence of lived experience
D. Symbolic object
E. Environmental object

哪一种最接近 References？

如果不同图片存在变化，请说明。

--------------------------------------------------
5.3 Composition
--------------------------------------------------

分析：

- 居中程度
- 偏置程度
- 对称 / 非对称
- 主体是否贴近边缘
- 是否保留大量留白
- 构图是否有编辑感
- 是否像桌面观察
- 是否像产品 hero shot
- 是否存在刻意戏剧化角度
- 是否存在静态、从容的观看感

判断：

这些构图更强调：

- clarity
- intimacy
- restraint
- isolation
- materiality
- atmosphere
- design

中的哪些？

--------------------------------------------------
5.4 Object-to-Frame Ratio
--------------------------------------------------

分析：

- 物件通常占画面多少视觉权重
- 是否偏近景
- 是否偏中近景
- 是否常填满画面
- 是否经常让背景存在
- 是否依赖大面积负空间
- 是否存在明显的视觉呼吸感

不要强行写精确百分比，
除非 Reference 足以支持。

可以使用：

small / moderate / dominant / frame-filling

等相对描述。

--------------------------------------------------
5.5 Camera Angle / Viewpoint
--------------------------------------------------

分析：

- 平视
- 俯视
- 斜俯视
- 极近视角
- 桌面视角
- 观察式视角

是否存在主导方向？

这些视角给人的感觉更像：

- observer
- owner
- user
- archivist
- product photographer

中的哪一种？

--------------------------------------------------
5.6 Context / Environment
--------------------------------------------------

分析物件是否被放在：

- 纯背景
- 桌面
- 工作台
- 书桌
- 床头
- 窗边
- 室内空间局部
- 其他现实表面

判断：

环境的作用是：

- 提供语义
- 提供材质
- 提供生活感
- 提供空间纵深
- 还是仅仅做背景

特别分析：

References 是否倾向：

“物件存在于人的生活世界中”

而不是：

“物件被从现实中抽离后进入摄影棚”

如果成立，请解释视觉证据。

--------------------------------------------------
5.7 Background
--------------------------------------------------

分析：

- 背景复杂度
- 背景颜色
- 背景材质
- 背景是否有纹理
- 是否完全纯色
- 是否存在空间环境
- 是否模糊
- 是否形成负空间
- 背景是否抢主体

判断背景总体更接近：

- studio backdrop
- lived-in surface
- neutral environment
- documentary environment
- editorial set

哪一种？

--------------------------------------------------
5.8 Lighting
--------------------------------------------------

分析：

- 自然光 / 人工光
- 硬光 / 柔光
- 侧光 / 正面光 / 顶光 / 逆光
- 阴影是否明显
- 是否存在局部高光
- 是否有戏剧性
- 是否有商业产品摄影式高控制布光
- 是否有自然光波动感
- 是否有“窗边”感觉

重点回答：

这种光线为什么让物件显得：

- 真实
- 安静
- 有材料感
- 有生活感
- 或具有编辑摄影感

--------------------------------------------------
5.9 Color Palette
--------------------------------------------------

分析：

- 主导色系
- 饱和度
- 冷暖倾向
- 是否偏中性色
- 是否偏暖灰 / 米白 / 木色 / 棕色
- 是否存在冷灰 / 蓝灰
- 是否存在高饱和强调
- 不同颜色之间是否保持克制

区分：

- stable palette
- allowed palette variation
- one-off accent colors

不要把单张图片颜色定义为整个 Skill 必须色值。

--------------------------------------------------
5.10 Materiality
--------------------------------------------------

这是本 Skill 的重点之一。

分析 References 如何呈现：

- 木
- 纸
- 金属
- 塑料
- 玻璃
- 皮革
- 布
- 陶瓷
- 其他材料

重点分析：

- 材质是否容易被感知
- 表面是否有真实细节
- 是否强调触感
- 是否存在磨损
- 是否存在反光
- 是否过度洁净
- 是否像 CGI / 3D render
- 是否保留现实物理不完美

说明：

什么让这些物件看起来“真实存在”。

--------------------------------------------------
5.11 Texture / Imperfection
--------------------------------------------------

分析：

- 划痕
- 磨损
- 灰尘
- 折痕
- 指纹
- 污渍
- 使用痕迹
- 边缘损耗
- 轻微杂乱

判断这些 imperfections 是：

- Dominant
- Common
- Occasional
- Rare

同时分析：

这种“不完美”是：

自然生活痕迹

还是

刻意做旧 / aesthetic distressing

两者必须区分。

--------------------------------------------------
5.12 Depth / Focus
--------------------------------------------------

分析：

- 浅景深
- 中景深
- 全清晰
- 主体与背景分离
- 焦外程度
- 是否存在商业摄影式强 bokeh
- 是否保留环境可辨识度

说明：

景深在这组视觉中主要承担什么作用。

--------------------------------------------------
5.13 Visual Density
--------------------------------------------------

分析：

- 单主体
- 双主体
- 少量辅助物
- 多物件
- 杂乱程度
- 空间是否拥挤

判断：

References 整体更偏：

low visual density
moderate visual density
high visual density

以及为什么。

--------------------------------------------------
5.14 Negative Space
--------------------------------------------------

分析：

- 留白是否是稳定风格特征
- 留白分布方式
- 留白是否来自背景
- 留白是否让画面更安静
- 留白是否形成编辑感
- 是否存在固定模板化留白

不要把“留白多”直接等于“极简”。

需要说明：

这种留白是：

- aesthetic minimalism
- visual breathing room
- contextual space
- editorial composition

中的哪一种。

--------------------------------------------------
5.15 Human Presence
--------------------------------------------------

检查是否出现：

- 手
- 手臂
- 身体局部
- 模糊人物
- 反射中的人物
- 使用中的物件

如果存在：

分析人物在画面中的作用。

判断：

Human presence 是：

- 核心元素
- allowed variation
- incidental detail
- 应避免

不要自行规定，只依据 References。

--------------------------------------------------
5.16 Emotional Tone
--------------------------------------------------

分析这组图共同传递什么情绪。

例如：

- quiet
- restrained
- intimate
- thoughtful
- lived-in
- warm
- cool
- lonely
- nostalgic
- clinical
- commercial
- dramatic

不要堆形容词。

需要明确：

哪些是核心，
哪些只是个别图。

并解释这些情绪是通过什么视觉属性实现的。

--------------------------------------------------
5.17 Editorial vs Documentary vs Commercial
--------------------------------------------------

这是非常关键的一节。

请判断这组 References 更接近：

- editorial still life
- documentary still life
- observational photography
- lifestyle photography
- product photography
- advertising photography
- conceptual still life

可以是混合类型。

必须解释：

为什么。

特别回答：

“它为什么没有明显的电商 / 产品广告感？”

以及：

“如果最终生成结果开始像商品广告，会出现哪些视觉变化？”

--------------------------------------------------
5.18 Realism
--------------------------------------------------

分析：

- 现实可信度
- 物件是否自然存在
- 材质是否可信
- 光线是否可信
- 是否有明显摆拍
- 是否有 CGI / AI 质感
- 是否过度精致
- 是否过度完美

判断这组 Reference 对“真实感”的要求大概是什么。

--------------------------------------------------
5.19 Recurring Visual Patterns
--------------------------------------------------

汇总真正稳定出现的视觉模式。

建议使用表格：

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
5.20 Allowed Variation
--------------------------------------------------

总结哪些变化不会破坏风格。

例如可能包括：

- 不同物件类型
- 不同背景
- 不同视角
- 不同景深
- 不同色温
- 单物件 / 少量组合

但必须以 References 为依据。

不要自行扩展无限 variation。

--------------------------------------------------
5.21 Invariant Characteristics
--------------------------------------------------

这是整个 reference_analysis 中最重要的输出之一。

列出：

如果未来生成 image-broll-object，
无论 subject 怎么变化，
哪些视觉属性仍然应该大体保持？

这里只提炼视觉核心。

不要转换为命令式生成规则。

使用描述性语言。

例如：

错误：
“Always use soft side light.”

正确：
“Soft, restrained side lighting appears to be a highly stable characteristic across the core references.”

--------------------------------------------------
5.22 Anti-patterns
--------------------------------------------------

根据 References 和 Prompt 1 的 audit，
分析哪些视觉方向明显不属于这个风格。

重点检查：

- e-commerce product photography
- luxury advertising
- glossy commercial studio photography
- pure white seamless background
- high saturation
- neon lighting
- cinematic product hero shots
- excessive bokeh
- surreal AI art
- conceptual fantasy
- decorative still-life styling
- high-density tabletop styling
- immaculate brand photography
- sterile CGI rendering
- generic Pinterest aesthetic

注意：

这里只做风格边界分析。

不要写成最终禁止规则列表。

--------------------------------------------------
5.23 Subtype Analysis
--------------------------------------------------

如果 Prompt 1 发现了 subtype，
在这里进行深入分析。

每个 subtype 说明：

- 它与核心风格共享什么
- 它独有的变化是什么
- 它是否值得保留
- 它是否只是 composition / context variation
- 它是否真的构成独立视觉语言

如果没有 subtype：

明确写：

Single coherent visual family.

--------------------------------------------------
六、不要分析的内容
--------------------------------------------------

本 Prompt 不需要分析：

- 什么时候使用 image-broll-object
- 什么语义应该触发它
- Asset Agent 如何调用
- 与 MG 的路由
- 与其他 B-roll Skill 的路由
- 视频剪辑窗口
- Camera Motion
- LUT
- Transition
- 使用频率
- 视频节奏

这些属于其他系统模块。

当前只研究：

静态图像本身的视觉语言。

--------------------------------------------------
七、输出文件
--------------------------------------------------

生成：

image-broll-object/reference_analysis.md

推荐结构：

# image-broll-object — Reference Analysis

## 1. Analysis Scope

说明：

- 使用了哪些 Core References
- 使用了哪些 Supporting References
- 排除了哪些 Outliers
- 是否存在证据不足

## 2. Core Visual Identity

## 3. Subject Treatment

## 4. Composition

## 5. Object-to-Frame Ratio

## 6. Camera Angle / Viewpoint

## 7. Context / Environment

## 8. Background

## 9. Lighting

## 10. Color Palette

## 11. Materiality

## 12. Texture & Imperfection

## 13. Depth / Focus

## 14. Visual Density

## 15. Negative Space

## 16. Human Presence

## 17. Emotional Tone

## 18. Editorial / Documentary / Commercial Positioning

## 19. Realism

## 20. Recurring Visual Patterns

## 21. Allowed Variation

## 22. Invariant Characteristics

## 23. Anti-patterns

## 24. Subtype Analysis

## 25. Final Visual Definition

最后使用一段完整、准确、非营销化的文字，
定义 image-broll-object 的视觉风格。

不要只输出：

“quiet, humanistic, editorial still life”

而要写清楚：

- 它如何呈现物件
- 它如何处理环境
- 它如何处理光线
- 它如何处理材质
- 它如何处理真实感
- 它与商品摄影的本质区别

## 26. Evidence Confidence

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
11. 不要引入某位摄影师或品牌作为最终风格定义，除非 Reference 本身明确支持。
12. 不要为了让分析显得专业而添加 References 无法支持的技术参数。
13. 不要自行指定焦段、光圈、ISO、色温数值等具体摄影参数。
14. 不要把偶然元素升级为核心规律。
15. 不要把 subject 本身当作风格。
16. 如果证据不足，明确写 Insufficient evidence。
17. 不要提前将描述性分析转换成命令式生成规则。

--------------------------------------------------
九、完成后的自检
--------------------------------------------------

提交前逐项检查：

- 是否读取了 reference_set_audit.md；
- 是否按照 Core / Supporting / Outlier 权重分析；
- 是否完整考虑了全部有效 Reference；
- 是否明确区分 Core / Variation / Incidental；
- 是否分析了 subject treatment；
- 是否分析了 composition；
- 是否分析了 context；
- 是否分析了 lighting；
- 是否分析了 color；
- 是否深入分析了 materiality；
- 是否深入分析了 imperfection；
- 是否分析了 negative space；
- 是否分析了 editorial / documentary / commercial 边界；
- 是否分析了 realism；
- 是否输出了 recurring patterns；
- 是否输出了 allowed variation；
- 是否输出了 invariant characteristics；
- 是否输出了 anti-patterns；
- 是否处理了 subtype；
- 是否给出了 Final Visual Definition；
- 是否标注了 Evidence Confidence；
- 是否没有提前编写生成规则；
- 是否没有提前编写 SKILL.md；
- 是否没有加入 Usage Contract。

如果任何一项未完成，请补全后再结束任务。
```

这一步和 Prompt 1 的核心差别是：

> **Prompt 1 判断“哪些 Reference 值得信”；Prompt 2 才判断“这些可信 Reference 到底共同构成了怎样的视觉语言”。**

这样到下一步 Prompt 3 时，Codex 才能把 `reference_analysis.md` 从**描述层**转换为真正可执行的 `Visual System Specification`。