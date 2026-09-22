你现在要为 AI 图片 B-roll Skill：

image-broll-object

执行 Phase 4：

Prompt 6 — Test Suite + Refinement

本任务的目标是：

对当前已经完成的：

image-broll-object/SKILL.md

进行真实测试，
验证它在不同 object subject、不同构图变体和高风险场景下，
是否能够稳定生成属于同一个视觉家族的图片。

你需要完成：

1. 建立正式 Test Suite
2. 为测试案例构建 prompts
3. 执行生成测试
4. 对生成结果进行视觉评估
5. 识别稳定失败模式
6. 判断问题来自：
   - prompt
   - SKILL.md
   - System Rules
   - 单次生成随机性
7. 做最小必要修正
8. 重新测试
9. 直到达到 v1 Freeze 标准

本 Prompt 是：

Test
→ Diagnose
→ Refine
→ Retest
→ Freeze

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
8. image-broll-object/skill_audit.md

如果：

skill_audit.md

仍然存在未解决的 Critical 或 Major 问题，

不要直接进入正式 Test Suite。

先修复这些问题，
并保证当前 SKILL.md 至少达到：

PASS
或
PASS WITH MINOR ISSUES

再开始测试。

--------------------------------------------------
二、测试目标
--------------------------------------------------

本阶段需要验证的不是：

“是否能偶尔生成一张漂亮图”。

而是：

image-broll-object 是否具备：

1. Visual Consistency
2. Subject Adaptability
3. Material Realism
4. Composition Stability
5. Context Plausibility
6. Anti-commercial Stability
7. Prompt Robustness
8. Variation Tolerance
9. Failure Recoverability

最终目标是：

不同 object subject 变化时，
视觉语言保持稳定；

同时不会退化为：

- product photography
- advertising
- CGI
- decorative still life
- surreal AI art
- generic Pinterest aesthetic

--------------------------------------------------
三、不要测试 Usage Contract
--------------------------------------------------

本阶段不测试：

- 什么时候应该使用 object B-roll
- 是否应该选择 B-roll
- 与 MG 的路由
- 与 document 的路由
- 与 quote 的路由
- Asset Agent 的决策
- 视频时间窗口
- Camera Motion
- LUT
- Transition
- 视频节奏

这些不属于本 Skill。

测试只回答：

“当 image-broll-object 已经被调用时，
它能否稳定把一个具体 object 生成成正确视觉。”

--------------------------------------------------
四、建立 Tests 目录
--------------------------------------------------

如果不存在：

image-broll-object/Tests/

创建：

image-broll-object/Tests/

至少生成：

1. test_cases.md
2. expected_behavior.md
3. evaluation_rubric.md
4. test_results.md
5. refinement_log.md

如果项目已有统一 Tests 结构：

优先遵循项目既有结构，

但必须保留以上信息。

--------------------------------------------------
五、Test Suite 设计原则
--------------------------------------------------

测试不能只使用最容易生成的 subject。

必须覆盖：

A. Core Cases
B. Variation Cases
C. Stress Cases
D. Boundary Cases

建议总测试数：

12–18 个。

不要为了数量制造重复 case。

优先保证覆盖面。

--------------------------------------------------
六、A 类：Core Cases
--------------------------------------------------

目标：

测试 Skill 在最典型 object 上是否成立。

请选择约 5–6 个。

建议候选：

- reading glasses
- old alarm clock
- smartphone
- keys
- notebook and pen
- employee badge

具体 case 可以根据 References 调整。

要求：

这些 subject：

- 物理结构清楚
- 材质差异明显
- 适合测试基础视觉语言

每个 Case 应至少定义：

- Case ID
- Subject
- Physical state
- Context
- Key visual challenge
- Expected behavior
- Major risks

--------------------------------------------------
七、B 类：Variation Cases
--------------------------------------------------

目标：

测试同一个视觉系统能否容纳变化，
而不变成固定模板。

请选择约 3–4 个。

重点变化维度：

- material
- color
- background
- viewpoint
- object count
- condition
- age
- depth

建议候选：

- ceramic cup
- metal desk clock
- plastic access card
- leather wallet
- headphones
- medicine bottle

但：

不得为了测试而刻意选择 References 完全不支持的极端物件。

--------------------------------------------------
八、C 类：Stress Cases
--------------------------------------------------

目标：

故意测试最容易把 Skill 带偏的 object。

建议至少 3–4 个。

重点风险：

### 1. Commercial-risk object
例如：
smartphone
credit card
headphones
watch

容易生成：

产品广告。

### 2. Luxury-risk object
例如：
glasses
watch
pen
wallet

容易生成：

奢侈品静物。

### 3. CGI-risk object
例如：
transparent bottle
metal object
electronics

容易生成：

3D render / impossible reflection。

### 4. Over-styling risk
例如：
book + coffee + glasses

容易变成：

Pinterest lifestyle flatlay。

测试必须故意覆盖这些风险。

--------------------------------------------------
九、D 类：Boundary Cases
--------------------------------------------------

目标：

测试 Skill 在允许变化边界上是否仍稳定。

建议 2–3 个。

例如：

- two related objects instead of one
- hand partially interacting with object
- object in slightly richer environment
- unusually worn object
- near frame-filling composition

只选择 References / Allowed Variation 支持的边界。

不要测试系统从未允许的视觉方向。

--------------------------------------------------
十、建立 test_cases.md
--------------------------------------------------

生成：

image-broll-object/Tests/test_cases.md

建议格式：

# image-broll-object — Test Cases

## TC-01
Type:
Core

Subject:

Physical State:

Context:

Variation Dimension:

Primary Challenge:

Expected Visual Behavior:

Main Failure Risks:

--------------------------------------------------

每个 Case 都必须有：

为什么测试它。

不要只写 subject 清单。

--------------------------------------------------
十一、建立 expected_behavior.md
--------------------------------------------------

生成：

image-broll-object/Tests/expected_behavior.md

这个文件描述：

不同 Test Case 的成功标准。

不是：

给出唯一正确构图。

应该定义：

“生成结果应该属于什么 visual family”。

例如：

TC-01 reading glasses

Expected:
- glasses clearly remain primary object
- surface and material feel physically real
- restrained composition
- context quiet and plausible
- no luxury eyewear advertising feel
- no sterile studio hero shot

不要要求：

必须与某张 Reference 构图完全一样。

--------------------------------------------------
十二、建立 evaluation_rubric.md
--------------------------------------------------

基于：

System/quality_rules.md

建立正式 Test Rubric。

至少包括：

1. Subject Clarity
2. Composition
3. Context
4. Lighting
5. Color / Tonal Restraint
6. Materiality
7. Imperfection / Lived-in Character
8. Physical Realism
9. Visual Density
10. Negative Space
11. Emotional Tone
12. Commercial Contamination
13. CGI / AI Artifact
14. Style-family Consistency

每项可以使用：

1–5

或：

PASS / MINOR / MAJOR / FAIL

但不要制造过度复杂评分。

--------------------------------------------------
十三、建议采用双层判定
--------------------------------------------------

每张图先做：

### Layer 1 — Hard Fail Check

只要出现以下关键错误：

直接 Fail：

- obvious product advertisement
- luxury campaign look
- sterile CGI
- impossible object geometry
- severe material artifact
- surreal concept art
- unrelated decorative still life
- heavy catalog styling

然后再做：

### Layer 2 — Style Quality Check

判断：

- composition
- materiality
- lighting
- context
- lived-in quality
- restraint
- visual-family consistency

这样比单纯平均分更合理。

--------------------------------------------------
十四、为每个 Case 构建测试 Prompt
--------------------------------------------------

必须使用：

SKILL.md 的 Prompt Construction Logic

而不是绕过 Skill 自己重写 prompt。

测试 Prompt 应完整体现：

- subject
- physical state
- context
- composition
- lighting
- materiality
- tonal character
- depth
- mood
- style guardrails

但：

不同 Test Case 的 Prompt 应尽量保持同一结构，

避免因为 Prompt 写法差异太大，
污染测试结果。

--------------------------------------------------
十五、Prompt 测试原则
--------------------------------------------------

测试不是：

“用最强人工 Prompt 把图救出来”。

而是验证：

SKILL.md 自己是否能稳定生成。

因此：

不要给每个 Case 额外加入大量手工风格补丁。

否则无法判断：

Skill 是否真的有效。

--------------------------------------------------
十六、生成测试
--------------------------------------------------

对每个 Test Case：

至少执行一次生成。

如果资源允许：

关键 Stress Case 建议生成 2–3 个变体，

以区分：

单次随机失败

与：

系统性失败。

但：

不要无限生成直到“碰巧成功”。

测试目的是发现系统问题。

--------------------------------------------------
十七、记录每次生成
--------------------------------------------------

在：

image-broll-object/Tests/test_results.md

记录：

- Case ID
- Prompt
- Output reference / filename
- Hard Fail
- Rubric result
- Overall verdict
- Main issue
- Confidence

建议 Verdict：

PASS
PASS WITH MINOR ISSUES
REVISE
FAIL

--------------------------------------------------
十八、失败原因分类
--------------------------------------------------

每个失败都必须判断更可能属于：

A. Prompt Construction Failure

例如：

- 描述太抽象
- risky vocabulary
- style guardrails 不够
- materiality 表达不足

B. SKILL.md Failure

例如：

- 执行规则不够明确
- 关键 invariant 遗漏
- anti-pattern 约束太弱

C. System Rule Failure

例如：

- visual_rules.md 本身缺少重要规律
- prompt_rules.md 本身不完整
- quality_rules.md 无法检测某类错误

D. Model Variance

例如：

- 单次 malformed geometry
- 随机错误
- 第二次生成正常

E. Subject-specific Difficulty

例如：

- electronics 极易产品广告化
- reflective metal 极易 CGI 化

不要把所有失败都归因于：

“模型随机性”。

--------------------------------------------------
十九、建立 Failure Taxonomy
--------------------------------------------------

在 test_results.md 中汇总高频失败类型。

例如：

F01 — Too Commercial
F02 — Too Polished
F03 — Too Decorative
F04 — Too CGI
F05 — Too Clean
F06 — Too Cluttered
F07 — Too Cinematic
F08 — Weak Materiality
F09 — Weak Context
F10 — Object Geometry Artifact
F11 — Generic Pinterest Styling
F12 — Excessive Bokeh
F13 — Over-aged
F14 — Subject Lost in Props

但：

只保留实际测试中出现的类型。

不要预设所有失败一定会发生。

--------------------------------------------------
二十、判断是否为系统性失败
--------------------------------------------------

一个问题应视为系统性失败，如果：

- 出现在多个不同 Test Case
或
- 在同一 Stress Case 多次重复
或
- 明确由当前 Skill wording 导致
或
- 与 References 的核心视觉差距稳定存在

单张偶发错误：

不要立刻修改整个 Skill。

--------------------------------------------------
二十一、Refinement 优先级
--------------------------------------------------

发现问题后，按以下顺序修正：

1. SKILL.md
2. prompt_rules.md
3. visual_rules.md
4. quality_rules.md

原则：

优先修最靠近执行层的地方。

只有当测试证明：

上游规则本身有缺陷，

才修改 System 文件。

不要轻易重写 reference_analysis.md。

--------------------------------------------------
二十二、允许修改哪些文件
--------------------------------------------------

本 Prompt 可以根据测试证据修改：

- SKILL.md
- System/prompt_rules.md
- System/visual_rules.md
- System/quality_rules.md

但：

必须满足：

有明确测试证据。

不要因为主观觉得“这样更好”就修改。

不要修改：

- References
- reference_set_audit.md
- reference_analysis.md

除非发现明显事实错误。

如发现明显事实错误：

只记录，
不要直接改。

--------------------------------------------------
二十三、Refinement 原则
--------------------------------------------------

每次修正规则时：

1. 说明 Failure
2. 说明 Evidence
3. 说明 Root Cause
4. 说明修改哪个文件
5. 说明修改哪条规则
6. 说明为什么这是最小修复
7. 说明可能副作用

禁止：

“大改一轮再看看”。

必须使用：

small controlled revision。

--------------------------------------------------
二十四、建立 refinement_log.md
--------------------------------------------------

生成：

image-broll-object/Tests/refinement_log.md

建议结构：

# image-broll-object — Refinement Log

## Revision 1

### Trigger
TC-XX / Failure type

### Evidence

### Root Cause

### Files Changed

### Before

### After

### Expected Effect

### Regression Risk

### Retest Cases

--------------------------------------------------
二十五、Retest
--------------------------------------------------

每次修改后：

不要重跑全部 Test Suite。

优先重跑：

1. 触发问题的 Case
2. 相邻 Stress Case
3. 一个 Core Case

用于检查：

修复是否成功
+
是否产生 regression。

只有重大规则修改：

才重新运行完整 Test Suite。

--------------------------------------------------
二十六、Regression Check
--------------------------------------------------

重点检查：

修复某个问题时，
是否破坏其他优点。

例如：

为了避免 product-ad look，
加入太多磨损，

可能导致：

所有物件都变旧。

为了避免 CGI，
加入过多纹理，

可能导致：

过度 gritty。

为了增加 context，

可能导致：

画面变 cluttered。

所以每次修正必须检查副作用。

--------------------------------------------------
二十七、特殊 Stress Test：Commercial Contamination
--------------------------------------------------

image-broll-object 必须特别测试：

commercial contamination。

至少选择：

2–3 个商业风险较高 object：

例如：

- smartphone
- headphones
- glasses
- watch
- credit card

检查是否出现：

- centered hero shot
- glossy surface
- pristine studio
- brand-campaign feel
- luxury lighting
- advertising composition

如果这些 subject 经常失败：

必须优先修 Prompt / Skill。

--------------------------------------------------
二十八、特殊 Stress Test：Materiality
--------------------------------------------------

至少选择不同材料：

- metal
- plastic
- paper
- glass
- ceramic
- leather / fabric

测试：

Skill 是否能稳定呈现材质差异。

如果所有对象都被生成成：

同一种过度光滑、过度精致表面，

说明 materiality system 不够有效。

--------------------------------------------------
二十九、特殊 Stress Test：Context
--------------------------------------------------

测试：

object 是否真的存在于可信现实空间。

检查：

- contact shadow
- surface relation
- scale
- surrounding context
- gravity
- placement logic

防止：

floating object
studio isolation
meaningless decorative surface。

--------------------------------------------------
三十、特殊 Stress Test：Variation Without Style Drift
--------------------------------------------------

至少测试：

三种明显不同的 object：

例如：

reading glasses
employee badge
smartphone

观察：

Subject 可以完全变化，

但以下是否仍然稳定：

- restraint
- material realism
- context plausibility
- lighting character
- visual density
- non-commercial feel

如果三个 Case 看起来像三个不同视觉品牌：

说明风格系统不足。

--------------------------------------------------
三十一、不要追求 Reference Copying
--------------------------------------------------

测试通过标准不是：

“是不是像某张 Pinterest 图”。

而是：

“是不是属于同一个 visual family”。

避免：

- literal layout copying
- exact object placement copying
- exact background copying

测试的是：

Style System

不是：

Reference imitation。

--------------------------------------------------
三十二、Freeze Criteria
--------------------------------------------------

当满足以下条件时，
可以冻结：

image-broll-object v1

建议至少达到：

### Core Cases
全部 PASS
或
PASS WITH MINOR ISSUES

### Variation Cases
大多数 PASS，
无明显 style drift

### Stress Cases
没有稳定的 Critical Failure Pattern

### Boundary Cases
允许少量 REVISE，
但不能证明系统核心失效

### System-wide
无重复出现的：

- product-ad contamination
- CGI contamination
- decorative styling drift
- severe material failure
- composition collapse

### Audit
SKILL.md 仍然：

- concise
- executable
- consistent
- no Usage Contract leakage

--------------------------------------------------
三十三、不要为了 100% 成功率无限迭代
--------------------------------------------------

生成模型本身存在随机性。

目标不是：

所有单次生成 100% 完美。

目标是：

Skill 对大多数典型输入稳定，
失败模式可预测，
并且可通过一次合理 revision 修正。

如果：

90% 视觉稳定

通常已经比：

为了追求 100%
把 Skill 写得极其僵硬

更好。

不要制造过拟合。

--------------------------------------------------
三十四、Freeze 产物
--------------------------------------------------

测试完成后：

更新：

image-broll-object/Tests/test_results.md
image-broll-object/Tests/refinement_log.md

并生成：

image-broll-object/Tests/final_test_report.md

推荐结构：

# image-broll-object — Final Test Report

## 1. Test Scope

## 2. Test Cases Summary

## 3. Pass Rate Summary

不要伪造统计。

## 4. Core Case Results

## 5. Variation Results

## 6. Stress Test Results

## 7. Boundary Results

## 8. Failure Taxonomy

## 9. Refinements Performed

## 10. Regression Checks

## 11. Remaining Known Limitations

## 12. Final Verdict

只能选择：

FREEZE V1
FREEZE V1 WITH KNOWN LIMITATIONS
NOT READY

## 13. Freeze Rationale

## 14. Recommended Future Tests

只记录未来可测试方向，
不要继续扩展当前 v1。

--------------------------------------------------
三十五、Freeze 后文件状态
--------------------------------------------------

如果 Final Verdict 为：

FREEZE V1

或：

FREEZE V1 WITH KNOWN LIMITATIONS

确保：

SKILL.md
System/visual_rules.md
System/prompt_rules.md
System/quality_rules.md

均处于最终经过测试的版本。

不要再进行无证据重写。

--------------------------------------------------
三十六、推荐最终目录
--------------------------------------------------

最终至少应为：

image-broll-object/
│
├── References/
│
├── reference_set_audit.md
├── reference_analysis.md
│
├── System/
│   ├── visual_rules.md
│   ├── prompt_rules.md
│   └── quality_rules.md
│
├── Tests/
│   ├── test_cases.md
│   ├── expected_behavior.md
│   ├── evaluation_rubric.md
│   ├── test_results.md
│   ├── refinement_log.md
│   └── final_test_report.md
│
├── skill_audit.md
│
└── SKILL.md

--------------------------------------------------
三十七、重要限制
--------------------------------------------------

1. 不要修改 References。
2. 不要随意修改 reference_set_audit.md。
3. 不要随意修改 reference_analysis.md。
4. 不要加入 Usage Contract。
5. 不要测试语义路由。
6. 不要测试 MG routing。
7. 不要加入视频剪辑规则。
8. 不要加入 Camera Motion。
9. 不要加入 LUT。
10. 不要加入 Transition。
11. 不要为了测试方便改变 Skill 职责。
12. 不要为了提高通过率把测试改得更容易。
13. 不要无限 regenerate 直到偶然成功。
14. 不要把单次随机 artifact 误判成系统问题。
15. 不要把系统性失败归因于随机性。
16. 不要为了修一个 case 导致整个 Skill 过拟合。
17. 不要把 Skill 扩成通用 still-life photography system。
18. 不要增加 References 未支持的新视觉方向。
19. 不要把测试目标改成“图片是否漂亮”。
20. 测试标准必须始终是：
   Reference-derived visual family consistency。

--------------------------------------------------
三十八、完成后的最终自检
--------------------------------------------------

提交前检查：

- 是否读取全部上游文件；
- 是否确认 Prompt 5 已无 Critical / Major 问题；
- 是否建立 Tests 目录；
- 是否创建 test_cases.md；
- 是否创建 expected_behavior.md；
- 是否创建 evaluation_rubric.md；
- 是否覆盖 Core Cases；
- 是否覆盖 Variation Cases；
- 是否覆盖 Stress Cases；
- 是否覆盖 Boundary Cases；
- 是否测试 commercial contamination；
- 是否测试 materiality；
- 是否测试 context plausibility；
- 是否测试 variation without style drift；
- 是否按照 SKILL.md 生成 Prompt；
- 是否没有手工过度优化单个 Test Prompt；
- 是否记录所有生成结果；
- 是否建立 Failure Taxonomy；
- 是否区分系统性失败和随机失败；
- 是否定位 Root Cause；
- 是否只做最小必要修正；
- 是否记录 refinement_log；
- 是否进行 retest；
- 是否进行 regression check；
- 是否生成 final_test_report.md；
- 是否给出 FREEZE V1 / FREEZE V1 WITH KNOWN LIMITATIONS / NOT READY；
- 是否没有加入 Usage Contract；
- 是否没有修改 Skill 的系统边界；
- 是否没有为了测试通过而过拟合。

如果任何一项未完成，请先补全再结束任务。
