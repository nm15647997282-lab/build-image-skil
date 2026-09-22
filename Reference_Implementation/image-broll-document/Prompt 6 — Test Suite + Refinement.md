
你现在要为 AI 图片 B-roll Skill：

image-broll-document

执行 Phase 4：

Prompt 6 — Test Suite + Refinement

本任务的目标是：

对当前已经完成的：

image-broll-document/SKILL.md

进行真实测试，
验证它在不同 paper artifact、不同视觉变体和高风险场景下，
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
9. 检查 regression
10. 直到达到 v1 Freeze 标准

本 Prompt 是：

Test
→ Diagnose
→ Refine
→ Retest
→ Regression Check
→ Freeze

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
8. image-broll-document/skill_audit.md

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

“是否能偶尔生成一张好看的复古图”。

而是：

image-broll-document 是否具备：

1. Visual Consistency
2. Artifact Adaptability
3. Paper Physicality
4. Aging Realism
5. Composition Stability
6. Negative-space Stability
7. Typography Boundary Stability
8. Archive / Memory Character Stability
9. Anti-scrapbook Stability
10. Anti-fake-antique Stability
11. Prompt Robustness
12. Variation Tolerance
13. Failure Recoverability

最终目标是：

不同 paper artifact subject 变化时，
视觉语言保持稳定；

同时不会退化为：

- scrapbook
- moodboard collage
- retro poster
- journal spread
- decorative stationery
- fake antique
- fake historical document
- AI text-heavy image
- generic vintage aesthetic
- cinematic nostalgia
- digital mockup

--------------------------------------------------
三、不要测试 Usage Contract
--------------------------------------------------

本阶段不测试：

- 什么时候应该使用 document B-roll
- 是否应该选择 B-roll
- 与 quote 的路由
- 与真实档案素材的路由
- 与 object 的路由
- 与 MG 的路由
- Asset Agent 的决策
- 视频时间窗口
- Camera Motion
- LUT
- Transition
- 视频节奏
- 使用频率

这些不属于本 Skill。

测试只回答：

“当 image-broll-document 已经被调用时，
它能否稳定把一个 paper artifact 生成成正确视觉。”

--------------------------------------------------
四、建立 Tests 目录
--------------------------------------------------

如果不存在：

image-broll-document/Tests/

创建：

image-broll-document/Tests/

至少生成：

1. test_cases.md
2. expected_behavior.md
3. evaluation_rubric.md
4. test_results.md
5. refinement_log.md

最终还需要生成：

6. final_test_report.md

如果项目已有统一 Tests 结构：

优先遵循项目既有结构，

但必须保留以上信息。

--------------------------------------------------
五、Test Suite 设计原则
--------------------------------------------------

测试不能只用：

“单张黑白旧照片放在中性背景上”

这种最容易成功的 case。

必须覆盖：

A. Core Cases
B. Variation Cases
C. Stress Cases
D. Boundary Cases

建议总测试数：

12–18 个。

不要为了数量制造重复 case。

优先保证：

不同 artifact
+
不同物理状态
+
不同背景
+
不同 aging 程度
+
不同文字风险
+
不同构图风险

都被覆盖。

--------------------------------------------------
六、A 类：Core Cases
--------------------------------------------------

目标：

测试 Skill 在最典型 paper artifact 上是否成立。

请选择约 5–6 个。

建议候选：

- single black-and-white family photograph
- faded color photograph
- small mounted portrait photograph
- lightly creased old photograph
- torn photograph fragment
- two gently overlapping old photographs

具体 case 可以根据 References 调整。

要求：

这些 case 能测试：

- artifact clarity
- paper physicality
- negative space
- restrained aging
- archive / memory character
- low visual density

每个 Case 至少定义：

- Case ID
- Artifact Type
- Physical State
- Placement
- Background
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

- black-and-white vs faded color
- mounted vs loose
- intact vs lightly damaged
- single vs double artifact
- paper background vs fabric background
- centered vs slightly off-center
- flat vs lightly angled
- low vs moderate aging
- shallow vs moderate depth

建议候选：

- mounted photo on neutral card
- faded color print on muted fabric
- two overlapping prints on paper surface
- slightly curled photograph with subtle edge wear

必须确保：

变化来自 References / Allowed Variation。

不要为了测试而发明全新视觉方向。

--------------------------------------------------
八、C 类：Stress Cases
--------------------------------------------------

目标：

故意测试最容易让 Skill 跑偏的输入。

至少选择 4 个。

--------------------------------------------------
### Stress 1 — Scrapbook Risk
--------------------------------------------------

例如：

two or three photographs
+
paper fragments

风险：

模型容易自动加入：

- tape
- stickers
- stamps
- handwritten notes
- decorative layering
- collage layout

测试 Skill 是否能保持：

low density
restrained composition
non-decorative archive character。

--------------------------------------------------
### Stress 2 — Fake Antique Risk
--------------------------------------------------

例如：

very old photograph
或
damaged photograph

风险：

模型容易变成：

- heavy sepia
- ancient parchment
- grunge overlay
- excessive tearing
- severe yellowing
- theatrical decay

测试：

aging 是否仍然 restrained / physically plausible。

--------------------------------------------------
### Stress 3 — Typography Risk
--------------------------------------------------

例如：

photograph with a small handwritten date
或
small archival label

风险：

模型容易自动生成：

- gibberish
- large text
- fake caption
- fake document
- quote-card layout

测试：

文字是否仍然只是 incidental trace。

--------------------------------------------------
### Stress 4 — Nostalgia / Cinematic Risk
--------------------------------------------------

例如：

old family photograph
或
private memory artifact

风险：

模型容易加入：

- warm sepia glow
- dramatic vignette
- emotional cinematic lighting
- sentimental props
- flowers
- candles
- melancholic staging

测试：

archive / memory character 是否仍主要来自：

materiality
aging
scale
negative space
quiet presentation

而不是情绪化造景。

--------------------------------------------------
九、D 类：Boundary Cases
--------------------------------------------------

目标：

测试 Allowed Variation 的边缘，
而不是测试完全越界的方向。

建议 2–3 个。

例如：

- three related photographs with restrained overlap
- one artifact occupying more of the frame than usual
- slightly stronger physical damage but still plausible
- small amount of incidental handwriting
- richer support-surface texture
- photograph containing several people

必须确保：

这些边界是 References / Allowed Variation 已支持的。

不要测试：

- full scrapbook
- full readable report
- dense collage
- historical newspaper recreation

因为这些本来就不属于本 Skill。

--------------------------------------------------
十、建立 test_cases.md
--------------------------------------------------

生成：

image-broll-document/Tests/test_cases.md

建议格式：

# image-broll-document — Test Cases

## TC-01

Type:
Core

Artifact Type:

Physical State:

Placement:

Background:

Variation Dimension:

Primary Challenge:

Expected Visual Behavior:

Main Failure Risks:

--------------------------------------------------

每个 Case 都必须说明：

为什么测试它。

不要只写 artifact 名称清单。

--------------------------------------------------
十一、建立 expected_behavior.md
--------------------------------------------------

生成：

image-broll-document/Tests/expected_behavior.md

这个文件描述：

不同 Test Case 的成功标准。

不是：

指定唯一构图。

例如：

TC-01 single black-and-white photograph

Expected:
- photograph remains clearly a physical paper object
- paper edge and thickness feel plausible
- background remains quiet
- aging is subtle rather than theatrical
- negative space supports restrained presentation
- no scrapbook decoration
- no dominant text
- no fake antique styling

重点：

定义 visual-family behavior，
而不是 Reference copying。

--------------------------------------------------
十二、建立 evaluation_rubric.md
--------------------------------------------------

基于：

System/quality_rules.md

建立正式测试 Rubric。

至少包括：

1. Artifact Clarity
2. Paper Physicality
3. Composition
4. Artifact-to-frame Balance
5. Negative Space
6. Background Restraint
7. Lighting
8. Color / Tonal Restraint
9. Aging Realism
10. Damage Restraint
11. Materiality
12. Archive / Memory Character
13. Typography Non-dominance
14. Decorative Contamination
15. Fake-antique Contamination
16. Digital Mockup Risk
17. AI Artifact Risk
18. Style-family Consistency

可使用：

1–5

或：

PASS / MINOR / MAJOR / FAIL

不要建立不必要的复杂评分。

--------------------------------------------------
十三、建议采用双层判定
--------------------------------------------------

每张图先执行：

### Layer 1 — Hard Fail Check

只要出现以下关键错误：

直接 Fail：

- scrapbook layout
- dense decorative collage
- fake antique parchment
- obvious retro poster design
- fake historical document
- large AI gibberish text
- quote-card composition
- impossible paper geometry
- floating artifact
- severe digital mockup look
- excessive decorative styling
- artifact no longer visually primary

然后再执行：

### Layer 2 — Style Quality Check

判断：

- paper physicality
- composition
- negative space
- aging
- background
- lighting
- tonal character
- archive / memory character
- visual-family consistency

--------------------------------------------------
十四、为每个 Case 构建测试 Prompt
--------------------------------------------------

必须使用：

SKILL.md 的 Prompt Construction Logic

而不是绕过 Skill 自己重新设计 prompt。

测试 Prompt 应按照当前 SKILL.md 组织：

- artifact type
- physical state
- placement
- background
- composition / negative space
- lighting
- paper materiality
- aging / imperfection
- color / tonal character
- archive / memory character
- style guardrails

不同 Case 应尽量保持同一 Prompt 架构。

避免：

Case A 写得极度详细，
Case B 只写一句话。

否则测试不可比较。

--------------------------------------------------
十五、Physical-description First 测试原则
--------------------------------------------------

测试 Prompt 必须遵守当前 Skill 已建立的：

Physical-description First Principle。

优先表达：

- paper thickness
- matte photographic surface
- slight edge wear
- subtle fading
- natural crease
- realistic contact shadow
- gentle curl
- low-saturation print
- quiet neutral support surface

避免依赖：

- vintage
- retro
- antique
- nostalgic
- sepia
- old-fashioned

等抽象标签。

这些词如果使用：

必须符合当前 prompt_rules.md 中的 Conditional / Risky 规则。

--------------------------------------------------
十六、Prompt 测试原则
--------------------------------------------------

测试不是：

“用人工超强 Prompt 把结果救出来”。

而是验证：

SKILL.md 自己是否足够有效。

因此：

不要给某个失败 Case 临时加入大量手工风格补丁。

否则无法判断：

Skill 是否真的成立。

--------------------------------------------------
十七、生成测试
--------------------------------------------------

对每个 Test Case：

至少执行一次生成。

如果资源允许：

关键 Stress Case 建议生成：

2–3 个变体。

优先包括：

- Scrapbook Risk
- Fake Antique Risk
- Typography Risk
- Nostalgia / Cinematic Risk

目的是区分：

单次随机失败

vs

稳定系统性失败。

不要无限生成直到偶然成功。

--------------------------------------------------
十八、记录每次生成
--------------------------------------------------

在：

image-broll-document/Tests/test_results.md

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
十九、失败原因分类
--------------------------------------------------

每个失败都必须判断更可能属于：

A. Prompt Construction Failure

例如：

- 过度使用 vintage vocabulary
- aging 描述太强
- negative-space 约束不足
- paper materiality 描述不足
- typography guardrail 不够

B. SKILL.md Failure

例如：

- 关键 invariant 过于抽象
- scrapbook anti-pattern 太弱
- physical-description principle 不够明确
- typography 边界压缩丢失

C. System Rule Failure

例如：

- prompt_rules.md 本身有歧义
- visual_rules.md 对 aging 定义不足
- quality_rules.md 无法区分 natural aging / fake antique

D. Model Variance

例如：

- 偶发乱码
- 单次错误折痕
- 随机边缘畸变
- 第二次生成正常

E. Artifact-specific Difficulty

例如：

- 多张照片容易 collage 化
- handwritten label 容易引发大量乱码
- damaged photo 容易 fake-antique 化

不要把所有失败归因于：

模型随机性。

--------------------------------------------------
二十、建立 Failure Taxonomy
--------------------------------------------------

在 test_results.md 中汇总实际出现的高频失败。

可能包括：

F01 — Too Scrapbook-like
F02 — Too Collage-like
F03 — Too Fake-antique
F04 — Excessive Sepia
F05 — Excessive Damage
F06 — Too Text-heavy
F07 — AI Gibberish Text
F08 — Too Poster-like
F09 — Too Decorative
F10 — Too Cinematic
F11 — Too Sentimental
F12 — Too Generic Vintage
F13 — Weak Paper Physicality
F14 — Digital Mockup Look
F15 — Weak Negative Space
F16 — Artifact Too Small
F17 — Artifact Lost in Background
F18 — Impossible Paper Geometry
F19 — Floating Artifact
F20 — Archive Character Too Weak

但：

只保留实际测试中出现的类型。

不要预设所有失败都会发生。

--------------------------------------------------
二十一、判断是否为系统性失败
--------------------------------------------------

一个问题应视为系统性失败，如果：

- 出现在多个不同 Test Case
或
- 在同一 Stress Case 多次重复
或
- 明确由当前 Skill wording 导致
或
- 与 References 的核心视觉差距稳定存在

例如：

如果：

TC-03
TC-08
TC-11

都自动加入：

tape + stamps + layered paper

则：

“scrapbook contamination”

应视为系统性问题。

单张偶发乱码：

不要立即重写整个 typography system。

--------------------------------------------------
二十二、Refinement 优先级
--------------------------------------------------

发现问题后，按以下顺序修正：

1. SKILL.md
2. System/prompt_rules.md
3. System/visual_rules.md
4. System/quality_rules.md

原则：

优先修改离执行最近的层。

只有测试证明：

上游规则本身有缺陷，

才修改 System 文件。

不要轻易修改：

reference_analysis.md。

--------------------------------------------------
二十三、允许修改哪些文件
--------------------------------------------------

本 Prompt 可以根据测试证据修改：

- SKILL.md
- System/prompt_rules.md
- System/visual_rules.md
- System/quality_rules.md

但：

每一次修改必须有明确测试证据。

不要因为主观觉得：

“这样更有档案感”

就修改规则。

不要修改：

- References
- reference_set_audit.md
- reference_analysis.md

除非发现明显事实错误。

如发现：

只记录问题，
不要直接改。

--------------------------------------------------
二十四、Refinement 原则
--------------------------------------------------

每次修正规则时：

1. 说明 Failure
2. 说明 Evidence
3. 说明 Root Cause
4. 说明修改哪个文件
5. 说明修改哪条规则
6. 说明为什么这是最小修复
7. 说明可能副作用
8. 指定 Retest Cases

禁止：

“大改一轮再看看”。

必须使用：

small controlled revision。

--------------------------------------------------
二十五、建立 refinement_log.md
--------------------------------------------------

生成：

image-broll-document/Tests/refinement_log.md

建议结构：

# image-broll-document — Refinement Log

## Revision 1

### Trigger

TC-XX / Failure Type

### Evidence

### Root Cause

### Files Changed

### Before

### After

### Expected Effect

### Regression Risk

### Retest Cases

--------------------------------------------------
二十六、Retest
--------------------------------------------------

每次修改后：

不要立即重跑全部 Test Suite。

优先重跑：

1. 触发问题的 Case
2. 一个相关 Stress Case
3. 一个 Core Case

例如：

修复 scrapbook contamination 后：

Retest:
- 原 scrapbook stress case
- 一个双照片 variation case
- 一个 single-photo core case

用于检查：

修复成功
+
没有把所有图强制变成单主体。

只有重大规则修改：

才重新运行完整 Test Suite。

--------------------------------------------------
二十七、Regression Check
--------------------------------------------------

这是本 Skill 特别重要的一步。

例如：

为了避免 scrapbook：

你可能把 artifact 数量限制得太死，

导致：

合理的双照片 / 三照片 variation 也不能生成。

为了避免 fake antique：

你可能把 aging 压得太弱，

导致：

画面失去时间痕迹。

为了避免 AI text：

你可能完全禁止文字，

导致：

Reference 支持的少量日期 / 背书痕迹无法出现。

为了增加 negative space：

可能导致：

artifact 小到失去信息。

所以：

每次修复必须检查副作用。

--------------------------------------------------
二十八、特殊 Stress Test：Scrapbook Contamination
--------------------------------------------------

至少选择：

2–3 个多 artifact / paper-fragment 风险 Case。

检查是否出现：

- decorative tape
- stickers
- stamps
- flowers
- handwritten captions
- layered collage
- journaling aesthetic
- moodboard layout

如果这些反复出现：

优先修：

Prompt Vocabulary
+
Anti-pattern
+
Visual Density / Composition rules

而不是简单禁止：

multiple artifacts。

--------------------------------------------------
二十九、特殊 Stress Test：Natural Aging
--------------------------------------------------

至少测试三个 aging level：

- light
- moderate
- upper-bound allowed

检查：

是否仍保持：

physically plausible
restrained
non-theatrical

重点识别：

- uniform sepia
- grunge overlay
- artificial brown stain
- over-tearing
- burned edges
- parchment transformation

如果模型经常出现这些：

优先修 aging vocabulary。

--------------------------------------------------
三十、特殊 Stress Test：Paper Physicality
--------------------------------------------------

测试：

- loose photo
- mounted photo
- overlapping prints
- curled photo
- creased photograph

检查：

- paper thickness
- edge
- surface
- contact shadow
- overlap logic
- mounting logic
- gravity

如果所有 artifact 都像：

平面数字贴图

说明：

Paper Materiality system 不够有效。

--------------------------------------------------
三十一、特殊 Stress Test：Typography Boundary
--------------------------------------------------

至少测试：

1. no text requested
2. tiny handwritten date
3. small archival label

检查：

是否出现：

- 大段乱码
- fake quote
- headline
- report
- newspaper layout
- typography-led composition

目标不是：

完全没有文字，

而是：

text remains incidental when present。

--------------------------------------------------
三十二、特殊 Stress Test：Archive / Memory Character
--------------------------------------------------

至少选择：

- family photo
- faded anonymous photograph
- torn private snapshot

检查：

画面的 memory / archive 感是否主要来自：

- artifact materiality
- restrained aging
- scale
- negative space
- quiet support surface

而不是：

- sepia
- vignette
- candle
- flower
- emotional lighting
- cinematic melancholy

--------------------------------------------------
三十三、特殊 Stress Test：Variation Without Style Drift
--------------------------------------------------

至少选择三个明显不同 subtype：

例如：

1. single black-and-white photograph
2. faded color mounted print
3. two overlapping worn photographs

观察：

Artifact 形式明显变化时，

以下是否仍然稳定：

- paper physicality
- restrained composition
- negative-space logic
- aging realism
- low decorative density
- archive / memory character
- non-scrapbook feel

如果三者看起来像三个完全不同视觉体系：

说明 Skill 的风格核心不足。

--------------------------------------------------
三十四、特殊 Stress Test：Artifact Content vs Artifact Object
--------------------------------------------------

至少使用一张：

包含人物的旧照片

作为测试。

检查：

模型是否把画面错误扩展成：

“一个真实人物站在场景里”

或者：

“完整旧时代肖像摄影”。

正确结果应仍然保持：

photograph as physical paper artifact

而不是：

portrait as full-frame image。

--------------------------------------------------
三十五、不要追求 Reference Copying
--------------------------------------------------

测试通过标准不是：

“是否和某张 Pinterest Reference 一模一样”。

而是：

“是否属于同一个 visual family”。

避免：

- exact layout copying
- exact background copying
- exact tear-pattern copying
- exact subject-size copying

测试的是：

Style System

不是：

Reference imitation。

--------------------------------------------------
三十六、Freeze Criteria
--------------------------------------------------

当满足以下条件时，
可以冻结：

image-broll-document v1

建议至少达到：

### Core Cases

全部：

PASS
或
PASS WITH MINOR ISSUES

### Variation Cases

大多数 PASS，

无明显 template lock

无明显 style drift

### Stress Cases

没有稳定 Critical Failure Pattern。

尤其不能重复出现：

- scrapbook contamination
- fake-antique contamination
- typography domination
- paper physicality collapse
- generic vintage drift

### Boundary Cases

允许少量 REVISE，

但不能证明系统核心失效。

### System-wide

无重复出现的：

- dense collage
- severe sepia cliché
- digital mockup look
- fake document rendering
- sentimental cinematic styling
- impossible paper geometry

### Audit

SKILL.md 仍然：

- concise
- executable
- consistent
- non-readable-document
- no Usage Contract leakage

--------------------------------------------------
三十七、不要为了 100% 成功率无限迭代
--------------------------------------------------

生成模型存在随机性。

目标不是：

所有单次生成 100% 完美。

目标是：

Skill 对大多数典型输入稳定，
失败模式可预测，
且系统性失败已被控制。

不要为了追求 100%：

- 禁止所有多 artifact
- 禁止所有文字痕迹
- 禁止所有 aging
- 固定所有背景
- 固定所有构图
- 固定所有照片为黑白

否则 Skill 会过拟合。

--------------------------------------------------
三十八、Freeze 产物
--------------------------------------------------

测试完成后：

更新：

image-broll-document/Tests/test_results.md
image-broll-document/Tests/refinement_log.md

并生成：

image-broll-document/Tests/final_test_report.md

推荐结构：

# image-broll-document — Final Test Report

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

重点记录例如：

- handwriting remains high-risk
- multiple artifact layouts require stronger guardrails
- severe damage is less stable
- very small artifacts may lose physical detail

只能记录实际测试发现的问题。

## 12. Final Verdict

只能选择：

FREEZE V1
FREEZE V1 WITH KNOWN LIMITATIONS
NOT READY

## 13. Freeze Rationale

## 14. Recommended Future Tests

只记录未来方向。

不要继续扩当前 v1。

--------------------------------------------------
三十九、Freeze 后文件状态
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

此后不要继续做：

无测试证据的审美重写。

--------------------------------------------------
四十、推荐最终目录
--------------------------------------------------

最终至少应为：

image-broll-document/
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
四十一、重要限制
--------------------------------------------------

1. 不要修改 References。
2. 不要随意修改 reference_set_audit.md。
3. 不要随意修改 reference_analysis.md。
4. 不要加入 Usage Contract。
5. 不要测试语义路由。
6. 不要测试 quote routing。
7. 不要测试 real archive routing。
8. 不要测试 MG routing。
9. 不要加入视频剪辑规则。
10. 不要加入 Camera Motion。
11. 不要加入 LUT。
12. 不要加入 Transition。
13. 不要为了测试方便改变 Skill 职责。
14. 不要为了提高通过率把测试改得更容易。
15. 不要无限 regenerate 直到偶然成功。
16. 不要把单次随机 artifact 误判成系统问题。
17. 不要把系统性失败归因于随机性。
18. 不要为了避免 scrapbook 把所有多 artifact 禁掉。
19. 不要为了避免 AI text 把所有文字痕迹禁掉。
20. 不要为了避免 fake antique 把所有 aging 去掉。
21. 不要为了保证风格固定所有构图和背景。
22. 不要把 Skill 扩成通用 vintage photography system。
23. 不要把 Skill 扩成 archival graphic design system。
24. 不要把 Skill 扩成 readable document generation system。
25. 不要增加 References 未支持的新视觉方向。
26. 不要把测试目标改成“图片是否漂亮”。
27. 测试标准必须始终是：

Reference-derived visual family consistency。

--------------------------------------------------
四十二、完成后的最终自检
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
- 是否测试 Scrapbook Contamination；
- 是否测试 Fake Antique Risk；
- 是否测试 Paper Physicality；
- 是否测试 Typography Boundary；
- 是否测试 Archive / Memory Character；
- 是否测试 Artifact Content vs Artifact Object；
- 是否测试 Variation Without Style Drift；
- 是否按照 SKILL.md 构建 Prompt；
- 是否遵守 Physical-description First Principle；
- 是否没有手工过度优化单个 Test Prompt；
- 是否记录所有生成结果；
- 是否建立 Failure Taxonomy；
- 是否区分系统性失败与随机失败；
- 是否定位 Root Cause；
- 是否只做最小必要修正；
- 是否记录 refinement_log；
- 是否进行 Retest；
- 是否进行 Regression Check；
- 是否没有因修 scrapbook 问题而写死 artifact 数量；
- 是否没有因修 aging 问题而消除所有时间痕迹；
- 是否没有因修 text 问题而禁止所有 incidental typography；
- 是否生成 final_test_report.md；
- 是否给出：
  FREEZE V1
  / FREEZE V1 WITH KNOWN LIMITATIONS
  / NOT READY；
- 是否没有加入 Usage Contract；
- 是否没有修改 Skill 的系统边界；
- 是否没有为了测试通过而过拟合。

如果任何一项未完成，请先补全再结束任务。
