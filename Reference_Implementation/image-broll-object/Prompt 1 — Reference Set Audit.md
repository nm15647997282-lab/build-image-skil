你现在要为新的 AI 图片 B-roll Skill：

image-broll-object

执行 Phase 1 的第一步：

Prompt 1 — Reference Set Audit

目标不是分析完整视觉风格，也不是编写 SKILL.md，而是先审核当前 References 集合本身是否足够一致、可靠、可用于后续视觉规则提取。

--------------------------------------------------
一、任务目标
--------------------------------------------------

请检查：

image-broll-object/References/

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
二、关于 image-broll-object 的当前任务边界
--------------------------------------------------

image-broll-object 是一个“图片型 B-roll 视觉生成 Skill”。

它未来负责生成：

以具体实体物件为视觉主体的 B-roll 图片。

这里的“object”指：

- 真实世界中的具体物件；
- 日常生活、工作、阅读、消费、制度、记忆等场景中的实体对象；
- 能承载内容语义的物件，而不是纯装饰性静物。

例如可能包括但不限于：

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
- 具有社会、心理、生活语义的具体物件

但：

不要因为这些例子就自行假设最终风格。

最终视觉风格必须由 References 决定。

--------------------------------------------------
三、必须遵守的分析原则
--------------------------------------------------

### 1. Reference-first

所有判断必须优先来自实际 References。

不要因为你认为“object B-roll 应该怎样”，就把外部摄影知识强加给 Reference Set。

必须区分：

A. References 明确支持的规律
B. 你根据图片做出的合理推断
C. 外部摄影常识

本 Prompt 中应尽量只使用 A 和必要的 B。

不要把 C 写成既定风格规则。

---

### 2. 不要把偶然特征误判为规则

如果只有 1–2 张图片出现：

- 特殊背景
- 特殊颜色
- 特殊焦段
- 特殊道具组合
- 特殊构图
- 特殊光线
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

不同 Reference 里的物件可能完全不同。

例如：

手机、书、眼镜、闹钟、钥匙。

这本身不代表风格不一致。

你真正要比较的是：

- 摄影方式
- 构图逻辑
- 主体比例
- 空间关系
- 光线
- 色彩
- 材质感
- 背景
- 景深
- 留白
- 视觉密度
- 情绪温度
- 物件是否有使用痕迹
- 是否偏产品展示
- 是否偏生活观察
- 是否偏编辑摄影
- 是否偏概念艺术

---

### 4. 特别警惕以下污染方向

请检查当前 References 是否混入以下视觉语言：

- 电商产品摄影
- 奢侈品广告摄影
- 极端极简棚拍
- 纯白背景商品图
- 高饱和商业广告
- 霓虹科技风
- 超现实 AI 概念艺术
- 过度电影化静物
- 纯装饰性 Pinterest aesthetic
- 无语义的漂亮摆拍
- 高密度 tabletop styling
- 时尚杂志产品大片
- 社交媒体“氛围感静物”
- 与具体内容无关的通用空镜

如果存在，不要直接删除。
请标记并说明为什么它可能不适合作为核心 Reference。

--------------------------------------------------
四、审核维度
--------------------------------------------------

请至少从以下维度审核整个 Reference Set：

1. Subject Type
   - 单一物件 / 多物件
   - 日常物件 / 专业物件 / 私人物件
   - 主体是否明确

2. Object-to-Frame Ratio
   - 物件占画面比例
   - 是否常有大面积留白
   - 是否填满画面

3. Composition
   - 居中
   - 偏置
   - 对角线
   - 桌面构图
   - 空间局部
   - 平视 / 俯视 / 斜俯视

4. Context
   - 纯背景
   - 桌面
   - 工作空间
   - 生活空间
   - 环境是否提供语义

5. Lighting
   - 自然光
   - 侧光
   - 柔光
   - 硬光
   - 室内灯
   - 戏剧化灯光

6. Color
   - 黑白
   - 暖色
   - 冷色
   - 中性色
   - 低饱和
   - 高饱和

7. Materiality
   - 木
   - 金属
   - 纸
   - 玻璃
   - 塑料
   - 布料
   - 表面使用痕迹

8. Depth / Focus
   - 全清晰
   - 浅景深
   - 中等景深
   - 背景虚化程度

9. Texture
   - 光滑
   - 粗糙
   - 老化
   - 磨损
   - 真实使用感

10. Visual Density
   - 单一主体
   - 少量辅助物
   - 多物件堆叠
   - 杂乱程度

11. Human Presence
   - 完全无人
   - 手部
   - 身体局部
   - 人物模糊存在
   - 人是否抢主体

12. Emotional Tone
   - 安静
   - 克制
   - 温暖
   - 冷静
   - 孤独
   - 怀旧
   - 商业
   - 戏剧化

13. Editorial vs Commercial
   - 更像人文编辑摄影
   - 更像纪录静物
   - 更像商品摄影
   - 更像广告摄影

14. Realism
   - 是否真实可信
   - 是否有明显 AI 艺术感
   - 是否过度理想化

15. Negative Space
   - 留白是否是稳定特征
   - 留白如何分布
   - 是否存在模板化布局

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
- 适合成为后续规则提取的主要依据。

---

### B. Supporting References

整体方向一致，但包含某种可接受变化。

例如：

- 不同背景
- 不同焦段
- 不同物件数量
- 不同构图
- 不同色温
- 不同景深

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

不要因为看到轻微差异就过度拆分。

只有当以下差异具有系统性时，才考虑 subtype：

- 摄影方式持续不同
- 构图体系持续不同
- 光线体系持续不同
- 背景体系持续不同
- 情绪气质持续不同
- 商业感 / 纪录感根本不同

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

Natural side lighting — Dominant
Neutral backgrounds — Common
Hands entering frame — Occasional
Pure white studio background — Rare

不要伪造精确百分比，除非你确实能够可靠统计。

--------------------------------------------------
八、输出文件
--------------------------------------------------

生成：

image-broll-object/reference_set_audit.md

建议结构：

# image-broll-object — Reference Set Audit

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

- commercial product photography
- advertising
- overly aesthetic styling
- surrealism
- AI-art look
- decorative still life

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
12. 当前任务只回答：

“这组 References 本身是否可靠，以及哪些图片应该成为下一阶段分析的主要证据。”

--------------------------------------------------
十、完成后的自检
--------------------------------------------------

提交前检查：

- 是否完整浏览了 References 中全部图片；
- 是否逐张考虑而不是只抽样；
- 是否区分了 Core / Supporting / Ambiguous / Outlier；
- 是否区分了高频特征和单例特征；
- 是否检查了商业产品摄影污染；
- 是否检查了装饰性静物污染；
- 是否检查了 AI-art / surreal 风格污染；
- 是否判断了 subtype；
- 是否没有提前编写 reference_analysis；
- 是否没有提前制定最终 Skill 规则；
- 是否没有修改任何 Reference 文件；
- 是否给出了 READY / READY WITH ISSUES / NOT READY；
- 是否输出了下一阶段推荐 Reference Set。

如果任何一项没有完成，请先补全再结束任务。

