你现在要为 AI 图片 B-roll Skill：

image-broll-object

执行 Phase 3 的第二步：

Prompt 5 — Skill Consistency Audit

本任务的目标是：

对已经生成的：

image-broll-object/SKILL.md

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
10. 仍然能够作为真正的 execution-layer Skill 被稳定调用。

本 Prompt 的核心不是重新构建 Skill，

而是：

Audit
→ Identify Issues
→ Correct SKILL.md

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
7. image-broll-object/SKILL.md

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

但：

不要随意修改上游文件。

本 Prompt 默认只修正：

SKILL.md

--------------------------------------------------
### 2. 不重新发明风格

这不是第二次 Prompt 3。

不要：

- 重新设计 visual system
- 重新定义风格
- 引入新的摄影理论
- 引入新的色彩系统
- 引入新的构图策略
- 引入新的 materiality 规则
- 引入新的 aesthetic keywords

当前任务只判断：

SKILL.md 是否正确“编译”了既有系统。

--------------------------------------------------
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
4. Subject Construction
5. Composition
6. Environment / Background
7. Lighting
8. Color / Tonal Character
9. Materiality / Physical Realism
10. Depth / Focus
11. Allowed Variation
12. Prompt Construction
13. Prompt Language Guidance
14. Anti-patterns
15. Generation Checklist
16. Quality Check
17. Revision Guidance
18. Final Execution Rule

注意：

不要求标题必须逐字相同。

允许合并章节。

重点是：

对应执行能力是否存在。

如果两个高度相关模块被合理合并：

不要判错。

--------------------------------------------------
四、第二部分：Core Visual Identity 审计
--------------------------------------------------

对比：

reference_analysis.md
+
visual_rules.md
+
SKILL.md

检查：

SKILL.md 的 Core Visual Identity 是否准确保留了：

- 物件作为现实实体的存在感
- 材质真实性
- 生活痕迹 / lived-in character（如果上游支持）
- 克制构图
- 环境关系
- 光线气质
- 非商业产品摄影属性
- 非 CGI / 非过度 polished 属性

重点检查：

是否因为压缩变成了过于泛化的：

“quiet editorial still life”

如果只剩抽象形容词，
但失去“怎么呈现 object”的具体逻辑：

标记为问题。

--------------------------------------------------
五、第三部分：Invariant 一致性审计
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

- 强行固定背景
- 强行固定色调
- 强行固定视角
- 强行要求所有物件做旧
- 强行要求人物痕迹
- 强行要求大量留白

如果上游没有这么强的结论。

--------------------------------------------------
六、第四部分：Allowed Variation 审计
--------------------------------------------------

这是非常重要的一项。

对比：

reference_analysis.md / Allowed Variation
visual_rules.md / Allowed Variation
SKILL.md / Allowed Variation

检查：

1. 允许变化的维度是否都还在；
2. 有没有被 SKILL.md 写死；
3. 有没有把未被 References 支持的变化扩进去；
4. 有没有因为“保持一致性”而把 Skill 变得过于模板化。

重点检查可能包括：

- subject type
- object age
- background surface
- viewpoint
- object count
- prop count
- lighting variation
- depth variation
- color variation

最终目标：

Skill 应稳定，
但不能僵化成一个固定模板。

--------------------------------------------------
七、第五部分：Subject Construction 审计
--------------------------------------------------

检查 SKILL.md 是否正确表达：

- 主体明确
- object 是具体实体
- 单主体 / 多主体关系
- 辅助物关系
- 使用状态
- 物理状态
- object 与环境的关系

同时检查：

是否偷加入了“语义路由规则”。

例如：

“Use for consumerism”
“Use for memory”
“Use for work alienation”

这些不属于当前 Skill。

如果出现：

标记 Unsupported / Scope leakage。

--------------------------------------------------
八、第六部分：Composition 审计
--------------------------------------------------

对比：

reference_analysis.md
visual_rules.md
SKILL.md

检查：

- framing
- object-to-frame ratio
- negative space
- visual density
- viewpoint
- symmetry / asymmetry
- edge relation
- crop
- perspective

重点识别两类问题：

A. 过度模板化
例如：
“always centered”

B. 过度泛化
例如：
“compose naturally”

后者不可执行。

--------------------------------------------------
九、第七部分：Environment / Background 审计
--------------------------------------------------

检查：

SKILL.md 是否保留了：

- object 与现实表面的关系
- 背景低干扰
- 环境提供真实语境
- 背景不抢主体
- 避免广告棚拍化

特别检查：

是否错误引入：

- pure white studio
- luxury tabletop styling
- decorative set
- fashion editorial set

如果上游没有支持。

--------------------------------------------------
十、第八部分：Lighting 审计
--------------------------------------------------

检查：

- 光线方向
- 光线软硬
- 阴影
- 高光
- material visibility
- realism

是否准确继承上游。

警惕：

- dramatic cinematic light
- commercial product lighting
- luxury gloss
- neon
- theatrical spotlight

是否被错误加入。

同时检查：

SKILL.md 是否写入了上游不存在的：

- lens
- ISO
- aperture
- Kelvin
- exact light angle

如果有：

标记 Unsupported。

--------------------------------------------------
十一、第九部分：Color / Tonal Character 审计
--------------------------------------------------

检查：

- 是否正确表达色彩克制
- 是否正确表达 fixed vs non-fixed palette
- 是否把某些 Reference 的单张色彩误写成全局规则
- 是否强行加入固定 LUT / 色值

如果上游明确：

No fixed palette

则 SKILL.md 不得偷偷建立固定：

warm beige
brown
grey-green

之类硬规则。

--------------------------------------------------
十二、第十部分：Materiality / Physical Realism 审计
--------------------------------------------------

这是 image-broll-object 的最高优先审计模块之一。

检查 SKILL.md 是否充分保留：

- surface texture
- material difference
- wear
- reflections
- edge realism
- physical plausibility
- object geometry
- lived-in trace
- anti-CGI

重点判断：

Materiality 是否只是被写成一句：

“make it realistic”

如果是：

说明压缩过度。

SKILL.md 应至少保留足够的信息，让生成模型知道：

“真实”具体体现在哪里。

--------------------------------------------------
十三、第十一部分：Imperfection / Lived-in Character 审计
--------------------------------------------------

检查：

- 使用痕迹
- 磨损
- 指纹
- 折痕
- 划痕
- 轻微杂乱

是否被正确处理。

尤其检查：

是否从：

“allowed / common”

错误升级成：

“all objects must look old and worn”。

如果发生：

标记 Distorted。

--------------------------------------------------
十四、第十二部分：Depth / Focus 审计
--------------------------------------------------

检查：

- subject clarity
- background separation
- depth
- bokeh
- macro
- sharpness

是否与上游一致。

重点防止：

Skill 因为想显得“高级”而偷偷加入：

- extreme shallow depth
- creamy bokeh
- macro cinematic look

--------------------------------------------------
十五、第十三部分：Prompt Construction 审计
--------------------------------------------------

这是执行性审计的核心。

检查 SKILL.md 是否把 prompt_rules.md 有效压缩成：

可执行的 Prompt 构建流程。

至少确认：

Prompt 中能够表达：

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

如果 SKILL.md 只剩：

“write a detailed prompt based on the style”

则判定为严重不足。

--------------------------------------------------
十六、第十四部分：Prompt Vocabulary 审计
--------------------------------------------------

检查：

Preferred
Conditional
Risky
Avoid

是否被合理保留。

特别检查：

以下词汇如果在上游被标记为 risky，
SKILL.md 是否仍无条件使用：

- editorial
- minimal
- cinematic
- moody
- luxury
- polished
- dramatic
- vintage

同时检查：

是否为了简短而把“更安全替代词”全部删掉。

--------------------------------------------------
十七、第十五部分：Anti-pattern 审计
--------------------------------------------------

对比：

reference_analysis.md
visual_rules.md
quality_rules.md
SKILL.md

检查：

关键 anti-pattern 是否保留。

重点包括可能的：

- e-commerce product photography
- glossy advertising
- luxury product shot
- pure white catalog background
- neon technology aesthetic
- surreal object art
- decorative Pinterest still life
- high-density tabletop styling
- excessive cinematic dramatization
- sterile CGI

检查：

是否只是列名词，
但没有说明为什么错。

不要求长解释，
但至少应足够让执行模型理解偏差方向。

--------------------------------------------------
十八、第十六部分：Generation Checklist 审计
--------------------------------------------------

检查 Checklist 是否：

- 简短
- 可操作
- 不与 Quality Check 重复过多
- 不混入 Usage Contract

如果 Checklist 中出现：

“Is this the right moment to use object B-roll?”

删除。

因为那属于系统路由。

--------------------------------------------------
十九、第十七部分：Quality Check 审计
--------------------------------------------------

对比：

quality_rules.md
SKILL.md

检查：

是否保留关键 QA 维度：

- visual family consistency
- subject clarity
- composition
- material realism
- context plausibility
- commercial contamination
- CGI contamination
- AI artifact
- visual density
- lighting
- style drift

检查：

PASS / REVISE / FAIL

是否仍然有可执行意义。

--------------------------------------------------
二十、第十八部分：Revision Guidance 审计
--------------------------------------------------

检查：

是否覆盖最高频失败。

例如：

Too commercial
Too clean
Too decorative
Too CGI
Too cluttered
Too cinematic
Too generic

每一项是否存在：

Failure
→ Cause
→ Fix

如果只写：

“regenerate”

视为无效 Revision Guidance。

--------------------------------------------------
二十一、第十九部分：Scope Leakage Audit
--------------------------------------------------

检查 SKILL.md 是否出现不属于本 Skill 的内容：

- Usage Contract
- semantic trigger
- routing
- Visual Director decision
- Asset Agent decision
- MG routing
- quote routing
- document routing
- video editing
- B-roll duration
- Camera Motion
- LUT
- Transition
- pacing
- frequency

这些如存在：

标记 Unsupported / Scope leakage。

默认从 SKILL.md 删除。

--------------------------------------------------
二十二、第二十部分：Overengineering Audit
--------------------------------------------------

检查 SKILL.md 是否存在：

- 章节过多
- 同一规则重复 3 次以上
- 长篇理论解释
- 大量无意义术语
- 巨型词汇表
- 过于复杂评分
- 不必要的数值阈值
- 过度细化摄影参数

目标：

SKILL.md 必须是 execution layer。

不是知识百科。

--------------------------------------------------
二十三、第二十一部分：Under-specification Audit
--------------------------------------------------

反过来也检查是否压缩过度。

如果出现：

- “keep it realistic”
- “make it quiet”
- “use editorial style”
- “avoid commercial feel”

但没有可执行定义，

说明规则过于抽象。

重点检查：

Materiality
Composition
Prompt Construction
Anti-pattern
QA

这几个模块不能被压缩成空话。

--------------------------------------------------
二十四、生成审计报告
--------------------------------------------------

生成：

image-broll-object/skill_audit.md

推荐结构：

# image-broll-object — Skill Consistency Audit

## 1. Audit Scope

## 2. Overall Verdict

只能选择：

PASS
PASS WITH ISSUES
FAIL

并简要解释。

## 3. Structural Audit

## 4. Core Visual Identity Audit

## 5. Invariant Mapping

使用表格。

## 6. Allowed Variation Audit

## 7. Visual Rule Coverage

## 8. Prompt Rule Coverage

## 9. Quality Rule Coverage

## 10. Unsupported Additions

## 11. Distortions

## 12. Missing Rules

## 13. Redundancy / Overengineering

## 14. Scope Leakage

## 15. Priority Issues

按：

Critical
Major
Minor

分类。

## 16. Required Corrections

列出必须修改项。

## 17. Optional Improvements

只列非必要改进。

## 18. Final Recommendation

明确：

SKILL.md 是否可以进入 Prompt 6 测试阶段。

--------------------------------------------------
二十五、问题严重度标准
--------------------------------------------------

### Critical

会导致：

- 风格根本跑偏
- Skill 职责错误
- 主要 Invariant 丢失
- Prompt 无法稳定执行
- 变成产品广告 Skill
- 变成通用 still-life Skill

必须修复。

---

### Major

会导致：

- 稳定性下降
- Variation 被写死
- 某核心模块缺失
- QA 无法检查关键问题
- Prompt 表达不完整

应修复。

---

### Minor

例如：

- wording 冗余
- 小范围重复
- 顺序不理想
- 非关键描述模糊

可优化。

--------------------------------------------------
二十六、自动修正 SKILL.md
--------------------------------------------------

完成 skill_audit.md 后：

如果 Verdict 为：

PASS

不要修改 SKILL.md，
除非仅存在明确 typo。

如果 Verdict 为：

PASS WITH ISSUES

修复所有：

Critical
Major

问题。

Minor 问题：

只在不会造成无意义重写的情况下优化。

如果 Verdict 为：

FAIL

必须修复所有导致 Fail 的问题，
然后重新进行一次内部一致性检查。

--------------------------------------------------
二十七、修正原则
--------------------------------------------------

修改 SKILL.md 时：

1. 只修改有证据支持的问题。
2. 不修改上游 System 文件。
3. 不重新发明规则。
4. 不扩大 Skill 范围。
5. 不加入 Usage Contract。
6. 不开始测试。
7. 不加入具体 production prompts。
8. 不因为审计而显著膨胀文件。
9. 优先做最小必要修复。

目标是：

Correctness
>
Completeness inflation.

--------------------------------------------------
二十八、修正后的二次验证
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
- 无明显遗漏
- 无核心规则失真

如果仍存在：

继续修正。

直到至少达到：

PASS

或：

PASS WITH MINOR ISSUES

--------------------------------------------------
二十九、最终输出
--------------------------------------------------

本 Prompt 最终应得到：

image-broll-object/
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
三十、重要限制
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
17. 不要加入新的风格知识。
18. 不要把 Skill 重写成通用 still-life photography Skill。
19. 不要为了审计而重新搭建整个 Skill。
20. 优先执行最小必要修正。

--------------------------------------------------
三十一、完成后的自检
--------------------------------------------------

提交前检查：

- 是否完整读取全部输入；
- 是否生成 skill_audit.md；
- 是否给出 PASS / PASS WITH ISSUES / FAIL；
- 是否检查 Core Visual Identity；
- 是否完成 Invariant Mapping；
- 是否检查 Allowed Variation；
- 是否检查 Subject Construction；
- 是否检查 Composition；
- 是否检查 Environment / Background；
- 是否检查 Lighting；
- 是否检查 Color；
- 是否重点检查 Materiality；
- 是否检查 Imperfection / Lived-in；
- 是否检查 Depth / Focus；
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
