你现在要为 AI 图片 B-roll Skill：

image-broll-document

执行 Phase 3 的第二步：

Prompt 5 — Skill Consistency Audit

本任务的目标是：

对已经生成的：

image-broll-document/SKILL.md

进行一次系统性的静态一致性审计，

检查它是否：

1. 忠实继承 References 与 Reference Analysis；
2. 正确压缩并表达 Visual System Specification；
3. 没有遗漏关键视觉规则；
4. 没有加入来源不存在的新规则；
5. 没有把 Allowed Variation 写成硬性规则；
6. 没有把偶然特征写成核心 Invariant；
7. 没有出现内部规则冲突；
8. 没有因为压缩过度而失去可执行性；
9. 没有因为写得过长而重新变成“分析文档”；
10. 没有把 Skill 写偏成 readable document / quote / fake archive generator；
11. 没有滑向 scrapbook / collage / retro graphic design；
12. 仍然能够作为真正的 execution-layer Skill 被稳定调用。

本 Prompt 的核心不是重新构建 Skill，

而是：

Audit
→ Identify Issues
→ Correct SKILL.md

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
7. image-broll-document/SKILL.md

其中：

References
= 原始视觉证据

reference_set_audit.md
= Reference 权重与离群判断

reference_analysis.md
= 视觉语言描述层

visual_rules.md
= 视觉执行规则

prompt_rules.md
= Prompt 构建规则

quality_rules.md
= 质量评估规则

SKILL.md
= 当前待审计的执行层

--------------------------------------------------
二、审计原则
--------------------------------------------------

### 1. Evidence hierarchy

审计时遵守：

References
↓
reference_set_audit.md
↓
reference_analysis.md
↓
System/*.md
↓
SKILL.md

如果 SKILL.md 与上游冲突：

默认视为 SKILL.md 问题。

不要随意修改上游文件。

本 Prompt 默认只修正：

SKILL.md

---

### 2. 不重新发明风格

这不是第二次 Prompt 3。

不要：

- 重新设计 visual system
- 重新定义 archival aesthetic
- 引入新的 vintage language
- 引入新的 scrapbook / collage 语言
- 引入新的色彩体系
- 引入新的老化体系
- 引入新的档案摄影理论
- 引入新的摄影参数

当前任务只判断：

SKILL.md 是否正确“编译”了既有系统。

---

### 3. 区分四类问题

所有发现的问题请归入：

A. Missing
B. Distorted
C. Unsupported
D. Redundant

定义：

Missing
= 上游明确存在的重要规则，在 SKILL.md 中缺失。

Distorted
= 上游规则被误解、写死、弱化或改变了含义。

Unsupported
= SKILL.md 新增了上游没有依据的规则。

Redundant
= SKILL.md 出现大量重复、同义反复或不必要说明。

--------------------------------------------------
三、第一部分：结构完整性审计
--------------------------------------------------

检查 SKILL.md 是否包含必要执行模块。

至少检查：

1. Purpose
2. Core Visual Identity
3. Core Invariants
4. Artifact Construction
5. Artifact Treatment
6. Composition
7. Negative Space
8. Background / Support Surface
9. Paper Materiality / Physical Realism
10. Aging / Imperfection
11. Photograph Treatment
12. Lighting
13. Color / Tonal Character
14. Typography Presence
15. Human Content Inside Artifact
16. Allowed Variation
17. Prompt Construction
18. Prompt Language Guidance
19. Physical-description First Principle
20. Anti-patterns
21. Generation Checklist
22. Quality Check
23. Revision Guidance
24. Final Execution Rule

注意：

不要求标题逐字相同。

允许合理合并章节。

重点检查：

对应执行能力是否存在。

--------------------------------------------------
四、第二部分：职责边界审计
--------------------------------------------------

这是 image-broll-document 的首要审计项之一。

检查 SKILL.md 是否明确保持：

paper artifact as physical object

而不是：

document as readable text

确认它没有偷偷变成：

- quotation renderer
- report renderer
- historical evidence renderer
- newspaper renderer
- academic paper renderer
- exact text generator
- fake source generator

如果 SKILL.md 中出现：

- 大段真实文字生成
- 精确文献内容
- 原文重现
- 真实报道排版
- source verification
- readable paragraph generation

标记为：

Critical Scope Distortion

并修正。

--------------------------------------------------
五、第三部分：Core Visual Identity 审计
--------------------------------------------------

对比：

reference_analysis.md
+
visual_rules.md
+
SKILL.md

检查 Core Visual Identity 是否准确保留：

- paper artifact physicality
- old photograph / paper fragment character
- restrained presentation
- negative space
- material realism
- natural aging
- archival / memory character
- low visual density
- decorative restraint
- typography non-dominance

重点检查：

是否因为压缩变成过于泛化的：

“quiet vintage archival aesthetic”

如果只剩：

vintage
nostalgic
archival
old

等抽象词，

但失去：

纸张厚度、边缘、接触关系、老化、留白、物理存在感

则标记为严重 under-specification。

--------------------------------------------------
六、第四部分：Invariant 一致性审计
--------------------------------------------------

逐条对比：

visual_rules.md 中的 Invariants

与：

SKILL.md 中的 Core Invariants

建立映射。

输出表格：

| Upstream Invariant | Present in SKILL | Accurate | Severity | Notes |

检查：

- 是否遗漏
- 是否改写失真
- 是否把 SHOULD 写成 MUST
- 是否把 MAY 写成 SHOULD
- 是否把偶然特征升级成 invariant

特别警惕：

- 强行所有图片必须撕裂
- 强行所有纸张必须泛黄
- 强行所有照片必须黑白
- 强行所有背景必须米色
- 强行所有构图必须居中
- 强行必须大面积留白
- 强行必须有手写字
- 强行必须有胶带
- 强行必须有 sepia

如果上游没有这么强的结论。

--------------------------------------------------
七、第五部分：Allowed Variation 审计
--------------------------------------------------

对比：

reference_analysis.md / Allowed Variation
visual_rules.md / Allowed Variation
SKILL.md / Allowed Variation

检查：

1. 允许变化的维度是否都还在；
2. 有没有被 SKILL.md 写死；
3. 有没有把未被 References 支持的变化扩进去；
4. 有没有因为“保持一致性”而把 Skill 变成固定模板。

重点可能包括：

- artifact type
- single / double artifact
- mounted / loose
- torn / intact
- black-and-white / faded color
- background surface
- aging intensity
- placement angle
- visual density
- depth / focus
- tonal variation

最终目标：

Skill 应稳定，
但不能僵化成：

“一个旧照片居中摆在米色背景上”。

--------------------------------------------------
八、第六部分：Artifact Construction 审计
--------------------------------------------------

检查 SKILL.md 是否正确表达：

- artifact 是真实纸本物件
- 单一或少量组合
- 主体明确
- artifact 有物理厚度
- 与背景有接触关系
- 可存在 mounted / loose / stacked 等变化
- artifact 不作为设计版式元素使用

特别检查：

是否滑向：

- floating digital layer
- moodboard element
- graphic-design card
- poster element
- flat Photoshop mockup

--------------------------------------------------
九、第七部分：Artifact Treatment 审计
--------------------------------------------------

检查：

- flat
- mounted
- attached
- overlapping
- angled
- torn
- creased
- curled
- worn

是否被正确分成：

Default
Allowed Variation
Avoid

重点检查：

damage 是否被过度升级。

例如：

上游只是：

torn edge — Occasional

SKILL.md 却写：

“All paper artifacts should show tearing.”

这是 Distorted。

--------------------------------------------------
十、第八部分：Composition 审计
--------------------------------------------------

检查：

- placement
- artifact-to-frame ratio
- edge relation
- orientation
- density
- symmetry
- negative-space interaction

重点识别：

A. 过度模板化

例如：

always centered
always small
always vertical

B. 过度泛化

例如：

compose elegantly
make it balanced

后者不可执行。

--------------------------------------------------
十一、第九部分：Negative Space 审计
--------------------------------------------------

这是 image-broll-document 的最高优先审计模块之一。

检查 SKILL.md 是否保留：

- 留白的重要性
- 留白与 artifact 的关系
- 低视觉密度
- visual breathing room
- archival restraint
- memory isolation

同时检查：

是否把留白误写成：

纯极简设计原则。

特别识别：

- poster-like empty space
- subject too small for aesthetic effect
- decorative minimalism
- arbitrary whitespace

如果 SKILL.md 只写：

“use lots of negative space”

但没有说明其作用和边界，

标记为 under-specification。

--------------------------------------------------
十二、第十部分：Background / Support Surface 审计
--------------------------------------------------

检查：

SKILL.md 是否正确保留：

- low-interference support surface
- tactile background
- realistic contact
- neutral / restrained support
- background not competing with artifact

检查是否错误引入：

- elaborate vintage desk scene
- decorative stationery setup
- scrapbook background
- heavy props
- ornate historical set

--------------------------------------------------
十三、第十一部分：Paper Materiality / Physical Realism 审计
--------------------------------------------------

这是本 Skill 的最高优先审计模块之一。

检查 SKILL.md 是否充分保留：

- paper thickness
- edge realism
- surface texture
- fibers
- photographic paper character
- folds
- curl
- realistic contact shadow
- mounting relation
- physical geometry
- background contact

重点判断：

Materiality 是否被压缩成一句：

“make the paper look realistic”

如果是：

说明压缩过度。

必须保留足够具体的物理线索，让模型知道：

“真实纸本”究竟体现在哪里。

--------------------------------------------------
十四、第十二部分：Aging / Imperfection 审计
--------------------------------------------------

检查：

- fading
- yellowing
- edge wear
- crease
- stain
- scratch
- tear
- curl
- surface degradation

是否与上游一致。

重点区分：

natural aging
vs
aesthetic distressing

检查 SKILL.md 是否错误使用：

- heavy grunge
- dramatic decay
- antique parchment
- severe damage
- over-yellowing
- uniform sepia

如果这些没有 Reference 支持：

标记 Unsupported / Distorted。

--------------------------------------------------
十五、第十三部分：Photograph Treatment 审计
--------------------------------------------------

如果主体是旧照片：

检查 SKILL.md 是否正确处理：

- black-and-white
- faded color
- print border
- white margin
- low saturation
- tonal softness
- print grain

同时确认：

“照片作为纸本物件”

仍然优先于：

“照片里的内容”。

如果 Skill 开始主要描述：

人物长相
服装
肖像摄影
历史人物身份

而弱化纸本对象：

标记 Scope Drift。

--------------------------------------------------
十六、第十四部分：Lighting 审计
--------------------------------------------------

检查：

- 光线是否帮助呈现纸张厚度
- 是否帮助看见边缘
- 是否帮助看见折痕
- 是否帮助看见贴附 / 叠放关系
- 阴影是否真实
- 高光是否克制

重点警惕：

- cinematic spotlight
- museum spotlight
- dramatic chiaroscuro
- glossy studio light
- luxury product lighting

如果上游没有支持。

同时检查：

是否写入不存在的：

- lens
- ISO
- aperture
- exact Kelvin
- exact light angle

若有：

Unsupported。

--------------------------------------------------
十七、第十五部分：Color / Tonal Character 审计
--------------------------------------------------

检查：

- 是否准确表达低干扰色彩
- 是否保留黑白 / 褪色彩色等变化
- 是否错误固定 palette
- 是否把 sepia 偷偷变成默认
- 是否把暖米色背景写成硬规则

如果上游明确：

No fixed color palette

则 SKILL.md 不得创建固定：

beige
brown
sepia

体系。

--------------------------------------------------
十八、第十六部分：Typography Presence 审计
--------------------------------------------------

这是本 Skill 的关键边界项。

检查 SKILL.md 是否保持：

text = incidental trace

而不是：

text = semantic primary content

检查：

- 日期
- 编号
- 背书
- 标签
- 少量手写

是否只是辅助。

如果 SKILL.md 允许：

- 大段可读文字
- quote composition
- fake newspaper
- fake report
- fake academic text
- headline-led layout

标记 Critical / Major。

同时检查：

是否明确防止：

AI gibberish text dominating image。

--------------------------------------------------
十九、第十七部分：Human Content Inside Artifact 审计
--------------------------------------------------

检查：

如果纸本照片里有人物，

SKILL.md 是否仍然明确：

paper artifact is primary visual object.

防止 Skill 漂移为：

- portrait generator
- historical person generator
- family-photo reconstruction Skill

人物内容可以存在，

但不能改变视觉主体定义。

--------------------------------------------------
二十、第十八部分：Archive / Memory Character 审计
--------------------------------------------------

检查：

SKILL.md 是否正确表达：

archive / memory character 应主要来自：

- material aging
- paper physicality
- restrained scale
- negative space
- quiet presentation
- physical trace

而不是来自：

- sepia filter
- fake stamp
- vintage font
- fake handwriting
- retro border
- emotional copy
- cinematic nostalgia

如果后者成为主要风格实现：

标记 Distorted。

--------------------------------------------------
二十一、第十九部分：Physical-description First Principle 审计
--------------------------------------------------

检查 SKILL.md 是否保留：

优先通过物理描述构造“旧感”。

例如：

- faded surface
- natural edge wear
- slight curl
- matte photographic paper
- subtle crease
- realistic paper thickness

而不是堆叠：

vintage
retro
antique
nostalgic
old-fashioned
aged

如果 SKILL.md 过度依赖抽象词：

标记 Prompt-risk。

--------------------------------------------------
二十二、第二十部分：Prompt Construction 审计
--------------------------------------------------

检查 SKILL.md 是否把 prompt_rules.md 有效压缩成可执行流程。

至少确认 Prompt 能表达：

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

如果只剩：

“Create an archival vintage photograph.”

判定为严重不足。

--------------------------------------------------
二十三、第二十一部分：Prompt Vocabulary 审计
--------------------------------------------------

检查：

Preferred
Conditional
Risky
Avoid

是否被合理保留。

特别检查这些高风险词：

- vintage
- retro
- nostalgic
- antique
- archival
- ephemera
- cinematic
- moody
- historical
- distressed

如果上游将它们标记为 risky / conditional，

SKILL.md 不得无条件堆叠。

同时检查：

是否保留了更安全的物理描述替代方案。

--------------------------------------------------
二十四、第二十二部分：Anti-pattern 审计
--------------------------------------------------

检查关键 anti-pattern 是否保留。

重点包括：

- scrapbook
- moodboard collage
- memory board
- retro poster
- vintage graphic design
- journal spread
- decorative stationery
- excessive tape / sticker styling
- fake antique parchment
- exaggerated distressed texture
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

检查：

是否只是列名词，
但缺少最简短的偏差说明。

--------------------------------------------------
二十五、第二十三部分：Generation Checklist 审计
--------------------------------------------------

检查 Checklist 是否：

- 简短
- 可执行
- 不与 QA 重复过多
- 不混入 Usage Contract

至少应关注：

- artifact 是否明确
- paper 是否真实
- aging 是否克制
- negative space 是否合理
- background 是否低干扰
- visual density 是否低
- typography 是否退居辅助
- 是否避免 scrapbook
- 是否避免 fake antique
- 是否避免 generic vintage styling

如果出现：

“Should this B-roll be used here?”

删除。

这属于系统路由。

--------------------------------------------------
二十六、第二十四部分：Quality Check 审计
--------------------------------------------------

对比：

quality_rules.md
SKILL.md

检查是否保留：

- artifact clarity
- paper physicality
- composition
- negative space
- aging realism
- background restraint
- typography non-dominance
- archive / memory character
- decorative contamination
- AI artifact
- style-family consistency

检查：

PASS
REVISE
FAIL

是否有可执行意义。

--------------------------------------------------
二十七、第二十五部分：Revision Guidance 审计
--------------------------------------------------

检查是否覆盖高频失败：

- Too scrapbook-like
- Too fake-antique
- Too text-heavy
- Too digital / mockup-like
- Too sentimental
- Too cinematic
- Too dense
- Too poster-like
- Too generic-vintage

每项是否有：

Failure
→ Cause
→ Fix

如果只写：

“regenerate”

视为无效。

--------------------------------------------------
二十八、第二十六部分：Scope Leakage Audit
--------------------------------------------------

检查 SKILL.md 是否出现：

- Usage Contract
- semantic trigger
- routing
- Visual Director decision
- Asset Agent decision
- quote routing
- real archive routing
- object routing
- MG routing
- video editing
- B-roll duration
- Camera Motion
- LUT
- Transition
- pacing
- usage frequency

这些不属于本 Skill。

如果存在：

标记 Unsupported / Scope leakage。

默认删除。

--------------------------------------------------
二十九、第二十七部分：Overengineering Audit
--------------------------------------------------

检查 SKILL.md 是否存在：

- 章节过多
- 同一规则重复三次以上
- 长篇档案理论
- 大量复古术语
- 巨型词汇表
- 复杂评分系统
- 不必要数值
- 无 Reference 支持的精细参数

目标：

SKILL.md 必须是 execution layer。

不是：

archive aesthetics encyclopedia。

--------------------------------------------------
三十、第二十八部分：Under-specification Audit
--------------------------------------------------

反过来检查是否压缩过度。

如果出现：

- “make it archival”
- “make it nostalgic”
- “make paper realistic”
- “use negative space”
- “avoid scrapbook”

但没有具体执行逻辑，

说明规则过于抽象。

重点检查：

Paper Materiality
Aging
Negative Space
Typography
Prompt Construction
Anti-patterns
QA

不能被压缩成空话。

--------------------------------------------------
三十一、生成审计报告
--------------------------------------------------

生成：

image-broll-document/skill_audit.md

推荐结构：

# image-broll-document — Skill Consistency Audit

## 1. Audit Scope

## 2. Overall Verdict

只能选择：

PASS
PASS WITH ISSUES
FAIL

并简要解释。

## 3. Structural Audit

## 4. Scope Boundary Audit

重点回答：

是否仍然是：

paper artifact visual-generation Skill

而不是：

readable document / fake evidence generator。

## 5. Core Visual Identity Audit

## 6. Invariant Mapping

使用表格。

## 7. Allowed Variation Audit

## 8. Artifact Construction Audit

## 9. Negative Space Audit

## 10. Paper Materiality Audit

## 11. Aging / Imperfection Audit

## 12. Typography Boundary Audit

## 13. Archive / Memory Character Audit

## 14. Visual Rule Coverage

## 15. Prompt Rule Coverage

## 16. Quality Rule Coverage

## 17. Unsupported Additions

## 18. Distortions

## 19. Missing Rules

## 20. Redundancy / Overengineering

## 21. Scope Leakage

## 22. Priority Issues

按：

Critical
Major
Minor

分类。

## 23. Required Corrections

列出必须修改项。

## 24. Optional Improvements

只列非必要优化。

## 25. Final Recommendation

明确：

SKILL.md 是否可以进入 Prompt 6 测试阶段。

--------------------------------------------------
三十二、问题严重度标准
--------------------------------------------------

### Critical

会导致：

- Skill 职责错误
- 变成 readable document generator
- 变成 fake historical evidence generator
- 变成 scrapbook / collage Skill
- 主要 Invariant 丢失
- paper physicality 丢失
- Prompt 无法稳定执行

必须修复。

---

### Major

会导致：

- visual stability 明显下降
- negative space 被误解
- natural aging 被写偏
- typography 越界
- variation 被写死
- QA 无法检查关键问题

应修复。

---

### Minor

例如：

- wording 冗余
- 局部重复
- 顺序不佳
- 非关键描述模糊

可优化。

--------------------------------------------------
三十三、自动修正 SKILL.md
--------------------------------------------------

完成 skill_audit.md 后：

如果 Verdict 为：

PASS

不要修改 SKILL.md，
除非只有明确 typo。

如果 Verdict 为：

PASS WITH ISSUES

修复所有：

Critical
Major

问题。

Minor：

只在不会造成无意义重写时优化。

如果 Verdict 为：

FAIL

必须修复所有导致 Fail 的问题，

然后重新进行一次内部一致性检查。

--------------------------------------------------
三十四、修正原则
--------------------------------------------------

修改 SKILL.md 时：

1. 只修改有证据支持的问题。
2. 不修改上游 System 文件。
3. 不重新发明风格。
4. 不扩大 Skill 范围。
5. 不加入 Usage Contract。
6. 不开始测试。
7. 不加入具体 production prompts。
8. 不因为审计而显著膨胀文件。
9. 优先做最小必要修复。
10. 保持 paper artifact physicality 为核心。
11. 保持 readable text 非核心。
12. 保持 natural aging 而非 fake vintage styling。

目标：

Correctness
>
Completeness inflation.

--------------------------------------------------
三十五、修正后的二次验证
--------------------------------------------------

修正 SKILL.md 后，再次快速检查：

References
↓
Reference Analysis
↓
System Rules
↓
SKILL.md

确认：

- 无 Critical issue
- 无 Major inconsistency
- 无 unsupported rule
- 无 scope leakage
- 无 readable-document drift
- 无 scrapbook / collage drift
- 无 generic-vintage drift
- 无明显遗漏
- 无核心规则失真

如果仍存在：

继续修正。

直到至少达到：

PASS

或：

PASS WITH MINOR ISSUES

--------------------------------------------------
三十六、最终输出
--------------------------------------------------

本 Prompt 最终应得到：

image-broll-document/
│
├── References/
├── reference_set_audit.md
├── reference_analysis.md
├── System/
│   ├── visual_rules.md
│   ├── prompt_rules.md
│   └── quality_rules.md
├── skill_audit.md
└── SKILL.md

其中：

SKILL.md

可能根据 Audit 被修订。

不要创建 Tests。

--------------------------------------------------
三十七、重要限制
--------------------------------------------------

1. 不要修改 References。
2. 不要修改 reference_set_audit.md。
3. 不要修改 reference_analysis.md。
4. 不要修改 visual_rules.md。
5. 不要修改 prompt_rules.md。
6. 不要修改 quality_rules.md。
7. 不要联网搜索。
8. 不要生成图片。
9. 不要开始 Test Suite。
10. 不要执行 Refinement Loop。
11. 不要加入 Usage Contract。
12. 不要加入系统路由规则。
13. 不要加入视频剪辑规则。
14. 不要加入 Camera Motion。
15. 不要加入 LUT。
16. 不要加入 Transition。
17. 不要加入新的 visual style。
18. 不要把 Skill 重写成通用 vintage photography Skill。
19. 不要把 Skill 重写成 archival graphic design Skill。
20. 不要把 Skill 重写成 scrapbook / collage Skill。
21. 不要把 Skill 重写成 readable document generation Skill。
22. 不要把 sepia 设为默认。
23. 不要把重度破损设为默认。
24. 不要把大段文字设为默认。
25. 不要为了审计而重新搭建整个 Skill。
26. 优先执行最小必要修正。

--------------------------------------------------
三十八、完成后的自检
--------------------------------------------------

提交前检查：

- 是否完整读取全部输入；
- 是否生成 skill_audit.md；
- 是否给出 PASS / PASS WITH ISSUES / FAIL；
- 是否检查职责边界；
- 是否检查 Core Visual Identity；
- 是否完成 Invariant Mapping；
- 是否检查 Allowed Variation；
- 是否检查 Artifact Construction；
- 是否检查 Artifact Treatment；
- 是否检查 Composition；
- 是否重点检查 Negative Space；
- 是否重点检查 Paper Materiality；
- 是否重点检查 Aging / Imperfection；
- 是否检查 Photograph Treatment；
- 是否检查 Lighting；
- 是否检查 Color；
- 是否重点检查 Typography Presence；
- 是否检查 Human Content Inside Artifact；
- 是否检查 Archive / Memory Character；
- 是否检查 Physical-description First Principle；
- 是否检查 Prompt Construction；
- 是否检查 Prompt Vocabulary；
- 是否检查 Anti-patterns；
- 是否检查 Generation Checklist；
- 是否检查 Quality Check；
- 是否检查 Revision Guidance；
- 是否检查 Scope Leakage；
- 是否检查 Overengineering；
- 是否检查 Under-specification；
- 是否识别 Unsupported Additions；
- 是否识别 Distorted Rules；
- 是否识别 Missing Rules；
- 是否识别 Redundant Rules；
- 是否按 Critical / Major / Minor 分类；
- 是否完成必要的 SKILL.md 修正；
- 是否在修正后再次验证；
- 是否没有修改任何上游分析 / System 文件；
- 是否没有加入 Usage Contract；
- 是否没有开始 Prompt 6 测试。

如果任何一项未完成，请先补全再结束任务。
