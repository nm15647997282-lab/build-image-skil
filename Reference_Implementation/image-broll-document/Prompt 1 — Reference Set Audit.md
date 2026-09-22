你现在要为新的 AI 图片 B-roll Skill：

image-broll-document

执行 Phase 1 的第一步：

Prompt 1 — Reference Set Audit

目标不是分析完整视觉风格，也不是编写 SKILL.md，而是先审核当前 References 集合本身是否足够一致、可靠、可用于后续视觉规则提取。

--------------------------------------------------
一、任务目标
--------------------------------------------------

请检查：

image-broll-document/References/

中的全部 Reference 图片。

你需要回答的核心问题是：

1. 这些图片是否真的属于同一个可稳定复现的视觉方向？
2. 哪些图片最能代表这个 Skill 的核心视觉语言？
3. 哪些图片属于次级变化，而不是核心规则？
4. 哪些图片可能是离群图、误收集图或会污染后续分析？
5. 当前 Reference Set 是否存在多个明显子风格？
6. 哪些视觉特征是高频共性，哪些只是个别图片偶然出现？
7. 当前 Reference Set 是否已经足够支持下一步 Reference Analysis？

注意：

本 Prompt 只负责 Reference Set Audit。
不要生成 reference_analysis.md。
不要生成 visual_rules.md。
不要生成 prompt_rules.md。
不要生成 quality_rules.md。
不要生成 SKILL.md。
不要开始设计最终 Skill。

--------------------------------------------------
二、关于 image-broll-document 的当前任务边界
--------------------------------------------------

image-broll-document 是一个“图片型 B-roll 视觉生成 Skill”。

它未来负责生成：

以旧照片、纸本残片、私人档案、纸质记忆载体、历史痕迹或类似 paper artifact 为视觉主体的 B-roll 图片。

这里的 “document” 不是指：

- 可读的论文正文；
- 可验证的真实报告；
- 精确引用的历史文献；
- 需要真实文字内容的书页；
- 需要准确来源的新闻或研究材料。

这些属于真实证据或 quotation 类视觉，不由本 Skill 解决。

本 Skill 的核心更接近：

- old photograph
- archival paper artifact
- memory fragment
- found photograph
- torn paper artifact
- mounted photograph
- faded print
- personal archive
- paper relic

它强调的是：

纸本载体本身的物理存在、时间痕迹、记忆感、档案感和人文气质。

但：

不要因为这些描述就自行假设最终视觉风格。

最终视觉语言必须由 References 决定。

--------------------------------------------------
三、必须遵守的分析原则
--------------------------------------------------

### 1. Reference-first

所有判断必须优先来自实际 References。

不要因为你认为“archival paper 应该怎样”，就把外部摄影知识强加给 Reference Set。

必须区分：

A. References 明确支持的规律
B. 你根据图片做出的合理推断
C. 外部摄影常识

本 Prompt 中应尽量只使用 A 和必要的 B。

不要把 C 写成既定风格规则。

---

### 2. 不要把偶然特征误判为规则

如果只有 1–2 张图片出现：

- 特殊纸张颜色
- 特殊背景材质
- 特殊破损程度
- 特殊照片尺寸
- 特殊手写字
- 特殊贴纸或胶带
- 特殊构图
- 特殊老化效果

不要直接认为它属于 Skill 核心语言。

你需要统计和比较：

- 高频
- 中频
- 低频
- 单例

然后判断它更可能属于：

- Core Pattern
- Allowed Variation
- Outlier

---

### 3. 区分“内容差异”和“风格差异”

不同 Reference 中可能出现：

- 单张旧照片
- 两张叠放照片
- 撕裂照片
- 泛黄照片
- 黑白照片
- 褪色彩色照片
- 小尺寸印刷照片
- 带边框的照片
- 纸片残件

这本身不代表风格不一致。

你真正要比较的是：

- 纸本对象如何进入画面
- 主体占画面比例
- 留白
- 背景材质
- 光线
- 色调
- 老化程度
- 破损程度
- 是否强调真实物理质感
- 是否像私人收藏 / 档案遗物
- 是否像 scrapbook / collage
- 是否像设计海报
- 是否过度复古化
- 是否过度装饰

---

### 4. 特别警惕以下污染方向

请检查当前 References 是否混入以下视觉语言：

- scrapbook
- moodboard collage
- vintage poster design
- retro graphic design
- decorative ephemera collage
- stationery styling
- journal spread
- memory board
- high-density paper collage
- excessive stickers / tape / stamps
- overly distressed vintage effect
- fake antique styling
- fake historical evidence
- AI-generated illegible text
- social-media quote card
- typography-led composition
- editorial layout where design overwhelms the paper artifact
- highly cinematic dramatic archive imagery
- sentimental cliché nostalgia
- generic “vintage aesthetic”

如果存在，不要直接删除。
请标记并说明为什么它可能不适合作为核心 Reference。

--------------------------------------------------
四、审核维度
--------------------------------------------------

请至少从以下维度审核整个 Reference Set：

1. Artifact Type
   - 单张照片
   - 多张照片
   - 撕裂照片
   - 卡片
   - 纸本残片
   - 装裱照片
   - 其他 paper artifact

2. Artifact-to-Frame Ratio
   - 主体占画面比例
   - 是否通常较小
   - 是否存在大面积留白
   - 是否有填满画面的情况

3. Composition
   - 居中
   - 接近居中
   - 偏置
   - 轻微倾斜
   - 平放
   - 贴附
   - 叠放
   - 单件 / 多件组合

4. Background
   - 纸面
   - 墙面
   - 布料
   - 桌面
   - 中性平面
   - 是否低干扰

5. Surface / Material
   - 纸张纹理
   - 照片纸
   - 卡纸
   - 布面
   - 墙面
   - 纤维感
   - 粗糙度

6. Aging
   - 泛黄
   - 褪色
   - 折痕
   - 磨损
   - 撕裂
   - 边角卷曲
   - 污渍
   - 老化是否克制

7. Photograph Treatment
   - 黑白
   - 褪色彩色
   - 棕褐色
   - 低对比
   - 高对比
   - 是否保留真实旧照片感

8. Lighting
   - 自然光
   - 柔和侧光
   - 散射光
   - 平光
   - 阴影是否轻微
   - 是否戏剧化

9. Color Palette
   - 米白
   - 蓝灰
   - 暖灰
   - 棕色
   - 纸张黄
   - 中性色
   - 是否低饱和

10. Negative Space
    - 留白比例
    - 留白是否是核心特征
    - 留白是否服务静谧感

11. Visual Density
    - 单一纸本主体
    - 少量叠放
    - 多元素拼贴
    - 画面是否保持克制

12. Human Content Inside Artifact
    - 照片中是否有人物
    - 人物是否日常自然
    - 人物是否只是照片内容，而非现实画面主体

13. Emotional Tone
    - 安静
    - 克制
    - 怀旧
    - 私人记忆感
    - 孤独
    - 温柔
    - 历史感
    - 是否过度煽情

14. Archival vs Decorative
    - 更像档案遗物
    - 更像私人记忆物件
    - 更像设计拼贴
    - 更像复古装饰

15. Realism
    - 纸本物理感是否可信
    - 老化是否自然
    - 是否明显 AI
    - 是否过度做旧
    - 是否像人为设计出来的“假古董”

16. Typography Presence
    - 是否存在少量手写
    - 是否存在照片背书式文字
    - 文字是否仅作为物件痕迹
    - 是否有大量可读文字抢占主体
    - 是否会误导 Skill 走向 quote/document rendering

--------------------------------------------------
五、Reference 分组
--------------------------------------------------

请将全部 Reference 图片分为以下几类：

### A. Core References

最能代表未来 Skill 核心视觉语言的图片。

要求：

- 与大多数 Reference 共享主要视觉特征；
- 风格清楚；
- 不依赖极端特殊情况；
- 适合成为后续规则提取的主要依据；
- 能体现 paper artifact / archival / memory fragment 的核心气质。

---

### B. Supporting References

整体方向一致，但包含某种可接受变化。

例如：

- 不同背景色
- 不同纸本尺寸
- 单张与双张
- 黑白与褪色彩色
- 不同程度破损
- 不同摆放角度

这些图片可用于定义 Allowed Variation。

---

### C. Ambiguous References

不能立即判断是否应该保留。

需要说明：

- 它与核心风格哪里一致；
- 哪里又存在冲突；
- 是否建议后续继续保留观察。

---

### D. Outliers

明显偏离整体方向，可能污染后续分析的图片。

必须说明：

- 偏离在哪；
- 为什么可能误导后续规则；
- 建议删除、隔离还是仅作为反例保留。

--------------------------------------------------
六、子风格检查
--------------------------------------------------

请判断：

当前 Reference Set 是否其实包含多个明显子风格。

如果没有：

明确写：

Single coherent visual family.

如果存在：

请标记为：

Subtype A
Subtype B
Subtype C

并分别说明：

- 核心差异
- 是否仍属于同一个 Skill
- 是否只是 Allowed Variation
- 还是已经大到应该未来拆成不同 Skill

特别检查是否可能出现这些 subtype：

- single archival photograph
- stacked photographs
- torn / damaged paper artifact
- mounted photograph
- faded color print
- handwritten / labeled artifact

不要因为看到轻微差异就过度拆分。

只有当以下差异具有系统性时，才考虑 subtype：

- 构图体系持续不同
- 背景体系持续不同
- 老化程度持续不同
- paper artifact 类型持续不同
- 情绪气质持续不同
- archive 感与 scrapbook 感根本不同

--------------------------------------------------
七、频率判断
--------------------------------------------------

请对主要视觉特征进行粗略频率判断。

建议使用：

- Dominant
- Common
- Occasional
- Rare
- Single-instance

例如：

Single paper artifact — Dominant
Large negative space — Common
Black-and-white photograph — Common
Heavy tearing — Occasional
Handwritten caption — Rare

不要伪造精确百分比，除非你确实能够可靠统计。

--------------------------------------------------
八、输出文件
--------------------------------------------------

生成：

image-broll-document/reference_set_audit.md

建议结构：

# image-broll-document — Reference Set Audit

## 1. Audit Scope

## 2. Overall Assessment

说明：

- Reference 数量
- 整体一致性
- 是否足够用于下一阶段
- 是否存在明显污染

## 3. Reference Family Summary

概括当前 Reference Set 的视觉家族，但不要提前写完整 reference analysis。

## 4. Dominant Patterns

以表格形式列出：

| Visual Feature | Frequency | Confidence | Notes |

## 5. Variation Patterns

列出可以视为正常变化的特征。

## 6. Reference Classification

### 6.1 Core References

### 6.2 Supporting References

### 6.3 Ambiguous References

### 6.4 Outliers

必须引用具体图片文件名。

## 7. Subtype Check

判断是否存在多个子风格。

## 8. Potential Contamination Risks

重点检查：

- scrapbook
- collage
- retro graphic design
- fake antique styling
- excessive aging
- fake historical evidence
- AI text
- decorative vintage aesthetic

## 9. Missing Coverage

判断当前 Reference Set 是否缺少某些重要视觉变化。

注意：

这里只指出 Reference Set 覆盖是否不足。

不要自行去补图。
不要生成新图片。
不要搜索互联网。

## 10. Readiness for Reference Analysis

最终明确给出：

READY
或
READY WITH ISSUES
或
NOT READY

并解释原因。

## 11. Recommended Reference Set for Prompt 2

列出下一步 Reference Analysis 应该：

- 重点使用哪些图片
- 哪些图片作为 Supporting
- 哪些图片暂时排除
- 哪些图片作为 anti-reference / outlier 保存

--------------------------------------------------
九、重要限制
--------------------------------------------------

1. 不要修改或删除任何 Reference 图片。
2. 不要重命名图片。
3. 不要创建 SKILL.md。
4. 不要创建完整视觉规则。
5. 不要创建 prompt template。
6. 不要生成图片。
7. 不要使用互联网搜索补充参考。
8. 不要因为个人审美偏好而排除图片。
9. 所有 Outlier 判断必须给出视觉证据。
10. 如果图片不足以支持某个判断，明确写：

Insufficient evidence.

11. 不要把“这个 Skill 应该是什么样”倒推给 References。
12. 不要把此 Skill误定义为“真实文档文字生成 Skill”。
13. 不要把 quote、report、paper text rendering 等职责混入当前 Skill。
14. 当前任务只回答：

“这组 References 本身是否可靠，以及哪些图片应该成为下一阶段分析的主要证据。”

--------------------------------------------------
十、完成后的自检
--------------------------------------------------

提交前检查：

- 是否完整浏览了 References 中全部图片；
- 是否逐张考虑而不是只抽样；
- 是否区分了 Core / Supporting / Ambiguous / Outlier；
- 是否区分了高频特征和单例特征；
- 是否检查了 scrapbook / collage 污染；
- 是否检查了过度复古 / 过度做旧污染；
- 是否检查了假档案 / 假历史证据感；
- 是否检查了 AI text / typography 污染；
- 是否判断了 subtype；
- 是否没有提前编写 reference_analysis；
- 是否没有提前制定最终 Skill 规则；
- 是否没有把 Skill误解为 readable document generation；
- 是否没有修改任何 Reference 文件；
- 是否给出了 READY / READY WITH ISSUES / NOT READY；
- 是否输出了下一阶段推荐 Reference Set。

如果任何一项没有完成，请先补全再结束任务。
