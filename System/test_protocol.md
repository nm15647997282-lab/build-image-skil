# build-image-skill — Test + Refinement + Regression Protocol

## 1. Purpose

本文件定义 `Phase 4 — Test + Refine + Freeze` 的通用测试、诊断、最小修订、复测、回归与冻结协议。

Phase 3B 只证明当前 `SKILL.md` Candidate 在静态意义上正确编译了上游系统；Phase 4 必须进一步用真实生成证据回答：

> 目标 Skill 在不同合法输入、合法变化与已知风险下，是否仍能稳定生成属于同一 Reference-derived Visual Family 的结果？

正式验证链固定为：

```text
Test
↓
Diagnose
↓
Minimal Fix
↓
Retest
↓
Regression
↓
Freeze Decision
```

本 Protocol 只定义未来 Phase 4 应如何执行。它不在当前 Builder 建设阶段创建具体 Test Case、运行图片生成、修改目标 Skill 或签发真实 Freeze Verdict。

## 2. Test Philosophy

测试目标不是判断某次生成是否“好看”，也不是逐像素复制 Reference。正式目标是共同验证：

```text
Visual-family consistency
+ Variation tolerance
+ Anti-pattern resistance
+ Prompt robustness
+ Quality-rule validity
+ Revision stability
```

判断标准必须来自当前目标 Skill 的 References、Analysis、Visual System、Traceability 与已审计 Candidate。Builder 只规定测试方法，不预置具体 subject、构图、光线、材质、文字风险、风格词或失败方向。

一个单次成功结果不能证明 Skill 已成立；一个单次失败结果也不能自动证明整个系统失效。Phase 4 必须区分稳定行为、系统性失败、孤立偏差与输入特定难度。

## 3. Test Preconditions

正式测试只能在以下条件全部满足后开始：

- Target Skill Brief、Reference Set、Reference Audit 与 Reference Analysis 可读取；
- Visual、Prompt、Quality Rules 已通过 Phase 2 Gate；
- `SKILL.md` Candidate 已通过 Phase 3A；
- Phase 3B Static Audit Artifact 已完成；
- Phase 3B Verdict 为 `PASS`，或只含 Minor 的 `PASS WITH ISSUES`；
- `Critical = 0` 且 `Major = 0`；
- 当前 Candidate、System Rules 与 Traceability 是被该 Audit 实际覆盖的版本；
- Pending Test Coverage 已交付给 Phase 4；
- 不存在未解决的上游 Gate 失效、关键 Broken Link 或 Required Input 缺失。

禁止以下路径：

```text
Build Skill v1
→ skip Static Audit
→ Test
```

测试前还必须记录最小 Test Environment Snapshot：使用的生成模型或服务、可识别的版本、影响结果的主要设置、执行日期，以及已知无法固定的环境因素。无法获得的字段明确写 `unavailable`，不得伪造。

## 4. Formal Test Mapping

Test Suite 必须从当前 Build 的 active Traceability Entity 产生：

```text
INV          → Core Case
VAR          → Variation Case
ANTI         → Stress Case
VAR Boundary → Boundary Case
```

核心 SK 需要通过以上 Case 获得 execution coverage。一个 TC 可以验证多个相关 Entity，一个 Entity 也可以由多个 TC 覆盖，但不能为了提高数量制造同义 Case。

每个正式 TC 至少必须明确：

- 测试什么；
- 为什么需要该 Case；
- 验证哪些 active INV、VAR、ANTI 或 SK；
- 通过哪个 SK → VR / PR / QR 路径执行或判断；
- 哪种观察将构成成功、偏差、失败或阻塞；
- 失败将对哪一层提出诊断问题。

没有明确上游验证目标的 Case 不得进入正式 Suite。

## 5. Core Cases

Core Case 主要验证 active core / identity-critical INV 在典型、合法输入下能否稳定成立。

每个 Core Case 应覆盖一个或多个相关：

```text
INV
SK
VR
```

并检查：

- Core Visual Identity；
- identity-critical Invariant；
- 核心 Prompt Construction；
- 核心 QR 是否能正确判断；
- 是否发生重要 Style Drift 或 Scope Violation。

Core Case 不应只选择最容易成功的输入，也不应故意引入与核心验证无关的极端困难。Case 集合应能证明核心身份跨有意义的合法输入仍然存在，而不是只在一个示例中偶然成立。

## 6. Variation Cases

Variation Case 主要验证 active VAR：

> 当 Reference-supported 视觉变量变化时，Skill 是否仍保持同一 Visual Family？

Variation Case 必须说明：

- 被改变的 VAR 与支持范围；
- 变化时仍需保持的 INV；
- 选取该输入的覆盖目的；
- 越过何种边界会构成 Style Drift；
- 相关 SK、VR、PR 与 QR。

优先一次改变一个主要 Variation；若多个变化在 References 中本来就共同出现，可以做受控组合，但必须能解释各自作用。具体变化类型完全由当前 VAR 决定，Builder 不预置固定变化清单。

Variation Case 的目标是证明：

```text
Stable ≠ Template Locked
```

重复同一模板、只替换表面 subject，不自动构成有效 Variation Coverage，除非 subject diversity 本身就是被追踪的 VAR。

## 7. Stress Cases

Stress Case 主要验证 active core / important ANTI 以及正式记录的 contamination risk、prompt risk 或稳定 generation failure pattern。

它回答：

> 当一个仍在 Scope 内的输入容易把模型推向错误方向时，目标 Skill 能否抵抗已证实的 Style Drift？

Stress Case 必须：

- 连接一个或多个 active ANTI 或相关 SK；
- 使用当前系统真实存在的风险，不使用 Builder 固定清单；
- 保持输入仍属于目标 Skill 职责，不通过完全越界任务制造必然失败；
- 预先说明希望 Guardrail 抵抗什么，以及不能误伤哪些邻近 VAR；
- 对高风险 Case 使用预先声明、数量有限的重复生成，以区分偶发与系统性行为。

重复次数在执行前确定并记录。不得失败后无限 regenerate，直到出现一次偶然成功。

## 8. Boundary Cases

Boundary Case 主要验证 active VAR 的合法边缘与越界判据，回答：

> 合法 Variation 到什么程度开始离开目标 Visual Family？

Expected Behavior 应区分：

```text
Still valid
Borderline
Outside visual family
```

Boundary Case 用于发现两种相反问题：

- Variation 太窄，合法变化被误判或被 Guardrail 禁止；
- Variation 太宽，明显漂移仍被判为合格。

Case 应优先落在 Reference-supported 边缘。若使用 outside comparator，只用于校准边界，不代表扩展目标 Scope，也不能用一个完全无关任务替代真实边界测试。

## 9. Test Case Design and Deduplication

Test Suite 以覆盖为目标，不以 Case 数量为目标。每个 Case 应包含或能关联：

- TC ID；
- Case Type；
- upstream verification targets；
- input scenario；
- test purpose；
- primary challenge；
- Expected Behavior；
- main failure risks；
- generation plan，包括预先声明的 attempt 数量；
- applicable Prompt / Quality path。

若多个 Case 的上游目标、风险、Expected Behavior 与诊断价值相同，只是无关内容不同，应合并或删除。只有当输入多样性本身验证适应性、系统性失败或合法 Variation 时，才保留相似 Case。

Suite 最终应覆盖：

- Core Identity 与 Invariants；
- Allowed Variations；
- Anti-patterns；
- Variation Boundaries；
- Prompt Construction；
- Quality Evaluation；
- Scope Boundary；
- Audit 交付的 Known Risks 与 Pending Test Coverage。

## 10. Traceability Requirements

Phase 4 正式完成：

```text
INV / VAR / ANTI
↓
SK
↓
TC
```

Traceability YAML 继续遵守 `traceability_spec.md`，不建立第二套 Schema。每个 TC 使用规范中的：

- `id`；
- `title`；
- `case_type`；
- `verifies`；
- `status`；
- `location`；
- `notes`。

Prompt 中概念性的 `tests` 与 `source_rules` 由现有 `verifies` 关系和完整追溯路径表达，不在本阶段增加重复字段。`verifies` 至少包含一个 active INV、VAR、ANTI 或 SK；相关 VR 通过被验证 SK 的 `source_rules` 和上游链核验，详细路径保留在正式 Test Artifact。

关系必须双向同步：

- INV / VAR / ANTI / SK 的 `downstream.test_cases` 包含 TC ID；
- TC 的 `verifies` 包含对应上游 ID；
- location 指向实际 Test Case；
- deprecated / rejected ID 不被 active TC 无说明依赖；
- TC 的 case type 与主要验证目的相容。

## 11. Test Prompt Construction

每次测试的最终生成 Prompt 必须由目标 `SKILL.md` 自身的 Prompt Construction Logic 产生。测试输入可以指定合法 subject、scenario、Context 或 Variation 条件，但不能由测试人员另写一套更强的视觉系统。

测试记录必须同时保留：

- 原始测试输入；
- Candidate 按自身逻辑形成的实际 generation prompt；
- 使用的 SK / PR / VR；
- 与通用 Prompt 架构的任何有理由偏离。

同类 Case 应使用一致的构建过程和相近的信息完整度。Case A 被人工写得极度详细、Case B 只输入一句话，会污染比较，除非信息量差异本身就是正式测试目标。

### Prompt Rescue Prohibition

Case 失败后，禁止：

```text
add untracked manual detail
→ regenerate
→ declare PASS
```

如果稳定成功依赖额外描述、排序、词汇或 Guardrail，应把它诊断为 Prompt Construction Failure、SKILL.md Failure 或 System Rule Failure，并在正确责任层修复。任何临时诊断 Prompt 都必须明确标记为 diagnostic-only，不能计入正式 PASS，也不能替代修订后的 Retest。

## 12. Expected Behavior

每个 TC 的 Expected Behavior 必须在第一次生成前冻结，并基于对应 INV、VAR、ANTI、VR、SK 与 QR 说明：

- 必须成立的核心行为；
- 允许出现的变化；
- Borderline 与 Outside 的边界；
- 构成 Hard Fail 的已定义条件；
- 非 Hard Fail 的偏差如何判断；
- 哪些孤立现象可能属于 Model Variance；
- 失败将对哪些上游关系提出疑问。

Expected Behavior 定义 Visual-family behavior，不规定唯一构图或 Reference copying。

不得在看到输出后降低标准以制造通过。若新证据证明 Expected Behavior 自身错误，必须记录原因，回到其责任规则进行修订，使旧结果失效，并用修订后的标准重新执行相关 Case。

## 13. Evaluation Model

每次生成采用两层评价。

### 13.1 Layer 1 — Hard Failure

先检查当前 VR / QR 明确定义的：

- Core Invariant Violation；
- Critical Anti-pattern；
- Major Scope Violation；
- 当前 Visual System 相关的 Structural / Physical Failure；
- Severe Style Drift。

出现任一 Hard Fail，当前 attempt 直接失败，其他优点不能抵消。Hard Fail 必须连接具体 QR → VR 与 INV / ANTI / Scope，不得由测试人员临时发明。

### 13.2 Layer 2 — Visual-family Quality

没有 Hard Fail 时，再检查：

- Core Identity；
- Invariant Compliance；
- Variation Validity；
- Anti-pattern contamination；
- Prompt Rule effectiveness；
- Quality Rule consistency；
- Overall visual-family fit；
- Case-specific Expected Behavior。

可以使用辅助等级或分项评分帮助比较，但不能用单一总分掩盖 Hard Fail。`7.8 / 10` 不能覆盖一个 Critical Violation。

### 13.3 Quality Rule Calibration

真实结果同时验证 QR 是否有效。若 QR 持续误判、过严、过松、不可观察，或无法区分合法 VAR 与 Style Drift，标记 `Quality Rule Failure`，作为 System Rule Failure 的一种，并按 Root Cause 进入 Phase 2 修订，而不是临时改变测试结论。

## 14. Test Result Status

每个生成 attempt 与聚合后的 Test Case 使用：

```text
PASS
PASS WITH VARIANCE
FAIL
BLOCKED
```

### PASS

满足预先定义的 Expected Behavior，无 Hard Fail，核心要求与适用 Variation 成立。

### PASS WITH VARIANCE

存在非系统性偏差，但无 Hard Fail，Visual Family 与核心要求仍成立；偏差已记录，且没有证据表明它是稳定规则问题。

### FAIL

存在 Hard Fail、明确的系统或 Skill 问题，或多项偏差共同使 Expected Behavior / Visual Family 失效。

### BLOCKED

Case 无法有效执行或评价，例如必要输入、工具、模型访问、输出证据或评估条件缺失。`BLOCKED` 不是 PASS，也不得被排除后假装 Suite 完整。

Case 有多个 attempt 时必须保留每次结果，不能只展示最佳结果。聚合状态应考虑预先声明的重复计划与失败模式，不按挑选的单张结果决定。

## 15. Failure Attribution

每个 FAIL 或需要解释的重复偏差，必须优先归入以下来源之一；证据不足时使用 `Mixed / Unresolved`，不得猜测。

### 15.1 Prompt Construction Failure

Visual System 与 Candidate 已包含必要逻辑，但实际 Prompt 没有正确表达，例如遗漏重要描述、顺序错误、词汇误导、Guardrail 未表达或 VAR 选择表达错误。

诊断时必须区分：

- 单次测试执行没有遵守 Candidate；
- Candidate 的 Prompt Construction Logic 不够明确；
- 上游 PR 本身有缺陷。

修复位置由这一区分决定，不能把手工 Prompt Rescue 当作修复。

### 15.2 SKILL.md Failure

上游 Visual System 正确，但 Candidate 在编译时发生 Dropped Invariant、Variation Collapse、Missing Guardrail、Strength Distortion、Under-specification 或其他执行层遗漏 / 失真。

优先修复 Candidate 与相应 SK Traceability，不修改正确的上游视觉含义。

### 15.3 System Rule Failure

失败来自 `visual_rules.md`、`prompt_rules.md` 或 `quality_rules.md` 本身不足、冲突、错误、不可执行或不可评估。只有重复或因果证据明确指向系统规则时，才能采用此归因。

System Rule Failure 必须回到 Phase 2 Owner，而不是在 Phase 4 静默修改 System。

### 15.4 Model Variance

Prompt、Candidate 与 System 没有明显问题，偏差不能稳定复现，其他同类结果成立，且没有清楚的规则原因。

一次失败不足以证明 Model Variance。必须通过预先界定的重复或相关 Case 比较，排除稳定模式后才能采用。

### 15.5 Subject-specific Difficulty

某个特定 subject / scenario 对当前模型特别困难，而其他覆盖同一规则的 Case 稳定成立。它可以成为 Known Limitation 或未来专门测试方向，但不能为污染整个 Skill 而自动增加全局硬规则。

如果相同困难跨多个不同输入重复，必须重新评估是否已成为系统性 Prompt、Skill 或 Rule Failure。

### 15.6 Mixed / Unresolved

多个层级共同影响，或现有证据无法可靠区分。此状态要求补充有诊断价值的受控比较；不得在根因不清时大规模修改多个文件。

## 16. Systematic vs Isolated Failure

### 16.1 Systematic Failure

以下任一类证据可以支持 Systematic Failure：

- 相同失败跨多个相关 Case 出现；
- 同一 Case 在预先声明的重复生成中反复出现；
- 相同失败跨不同合法输入或 subject 出现；
- 通过受控比较能把失败清楚连接到某条 Rule、wording 或缺失机制；
- 与 Core Identity 的差距稳定存在。

系统性判断必须记录失败频率的实际观察与比较范围，不伪造统计。只有足够稳定或具有清楚因果证据的失败，才驱动较高层级系统修改。

### 16.2 Isolated Failure

如果失败只出现一次、不能在既定复核中稳定复现、其他同类 Case 通过且没有明确规则原因，先标记为 `possible model variance`。

Isolated 不等于忽略。它仍保留在 Test Results 与 Known Risks 中；若后续出现相同模式，应重新归类为 systematic candidate。

禁止两个相反捷径：

```text
one failure → rewrite system
all failures → blame model variance
```

## 17. Root Cause Diagnosis

每个失败按 Traceability 逐层定位：

```text
Observed Failure
↓
Relevant TC and Expected Behavior
↓
Relevant SK and actual generated Prompt
↓
Relevant PR / QR / VR
↓
Relevant INV / VAR / ANTI
↓
OBS / REF when upstream meaning is in doubt
↓
Root Cause
```

诊断至少回答：

1. 输出具体违反了什么预定义行为？
2. 这是单次、重复、跨 Case 还是跨输入模式？
3. 实际 Prompt 是否正确实现 SK？
4. SK 是否正确编译 PR / QR / VR？
5. 上游 Rule 是否可执行、无冲突且强度合理？
6. 失败是否只属于某个 subject / environment？
7. 最接近的责任层是哪一层？
8. 哪项最小修改可以证伪或验证当前 Root Cause？

“感觉 Prompt 不够好”或“模型不稳定”不是充分 Root Cause。

## 18. Refinement Priority and Phase Ownership

常见检查顺序是：

```text
1. SKILL.md
2. Prompt Rules
3. Visual Rules
4. Quality Rules
```

它只是从执行端向上定位的诊断顺序，不是无条件修改优先级。正式原则是：

> Fix the closest responsible layer.

按 `phase_contracts.md` 处理：

- 测试执行未遵守 Candidate：修正测试执行并重跑，不修改正式规则；
- Candidate 的局部执行措辞错误：Phase 4 可做有证据的局部修订，但 Candidate 一经修改，Phase 3B Gate 立即失效，必须重新 Static Audit 后才能恢复正式 Test；
- Candidate 的编译结构或覆盖错误：回到 Phase 3A，再经过 Phase 3B；
- PR / VR / QR 错误：回到 Phase 2，由 Owner Phase 修订并重新通过 Phase 2、3A、3B；
- 描述性分析错误：回到 Phase 1B，再通过全部受影响 Gate；
- Reference classification 或 Evidence 问题：回到 Phase 1A；
- 原始 Reference Set 不足：停止并等待受授权的证据补充。

测试失败本身不授权修改 Reference-derived Visual Identity。

## 19. Minimal Fix Principle

每次正式 Refinement 必须：

```text
Small
Controlled
Evidence-based
Traceable
Reversible
Testable
```

修订应尽量只处理一个主要 Root Cause。若必须同时修改多个互相依赖的规则，应说明为什么无法拆分、每项修改的作用及共同 Regression Risk。

禁止：

- 整体重写 Skill 后“再试试看”；
- 仅凭个人审美增强规则；
- 为一个 TC 添加大量 case-specific wording；
- 通过削弱 Expected Behavior 或降低测试难度制造 PASS；
- 用更强 Guardrail 消灭整类合法 VAR；
- 因单次失败直接修改 Analysis 或 Reference 结论。

## 20. Refinement Logging

每次 Refinement 至少记录：

- Revision ID；
- Triggering Failure / TC；
- Evidence；
- Failure Attribution；
- Root Cause；
- Owner Phase；
- Files Changed；
- Rules / Entity IDs Changed；
- Before；
- After；
- Why this is the minimal fix；
- Expected Effect；
- Regression Risk；
- Gate invalidation and revalidation；
- Retest Cases；
- Regression Cases；
- Outcome；
- rollback path if ineffective。

规则或 Entity 发生实质变化时，同步更新 Traceability 与 Revision Record。旧 ID 的处理、successor、status 与双向链接遵守 `traceability_spec.md`，不得无声改写历史。

## 21. Retest

任何修改完成后，不能直接宣布问题解决。必须先重过被修改层要求的上游 / Static Gate，再执行受影响 Case 的 Retest。

Retest 回答：

> 原失败是否被当前修复解决？

最小 Retest Set 通常包括：

- 触发失败的 TC；
- 一个能检验同一风险是否仍存在的相关 Case；
- 一个确认核心身份未被局部修复破坏的 Core Case。

若修复涉及 INV，至少包含受影响 Core Case 与相关 Variation / Stress Case；涉及 VAR 时包含相邻 Boundary；涉及 ANTI 时包含对应 Stress 与邻近合法 VAR。

Retest 必须使用修订后的正式 Candidate / System 与相同可比条件。只跑一个经过额外 Prompt Rescue 的结果不能关闭 Issue。

## 22. Regression Check

Retest 只回答原失败是否修复；Regression 回答：

> 修复是否破坏了原本正确的行为？

正式顺序必须是：

```text
Fix
↓
Revalidate affected gates
↓
Retest
↓
Regression
↓
Freeze Decision
```

任何正式修订没有完成 Regression，都不能进入 Freeze。

### 22.1 Local Change

局部、低影响修改可以运行：

- affected TC；
- related Core TC；
- related Variation / Stress / Boundary TC；
- Traceability impact path 指向的其他 Case。

### 22.2 Broad Change

修改 Core Visual Rule、Rule Strength、Major Prompt Construction、important INV / VAR / ANTI、共享 Guardrail 或多个 SK 时，应扩大 Regression，必要时运行完整 Suite。

Regression Scope 由受影响 Traceability 图和行为范围决定，不以“只改了一行”判断。小文本改动也可能改变所有 Prompt。

## 23. Variation and Anti-pattern Regression

任何修改 INV、ANTI、MUST、DO NOT 或共享 Prompt Construction 后，都必须特别检查合法 VAR 是否被压缩。

Variation Regression 至少检查：

- 原先通过的不同合法表现仍可生成；
- 默认值没有变成唯一值；
- Strengthening 没有造成 Template Lock；
- QR 仍能区分合法变化与漂移；
- Case-specific fix 没有成为全局限制。

修复 Anti-pattern 时，必须比较：

```text
ANTI
vs
legitimate nearby VAR
```

Guardrail 只能限制已证实的错误方向，不能简单禁止与其相邻的全部视觉元素或变化。Anti-pattern Stress Case 通过而邻近 Variation Case 失败，不能视为成功修复。

## 24. Test Iteration and Stop Conditions

允许：

```text
Test → Refine → Retest → Refine → Retest
```

但每轮必须有新 Evidence、明确 Root Cause、记录的修改和有限 Retest / Regression。不得无限迭代或无限生成直到偶然成功。

出现以下任一情况时，停止局部修补并升级 Diagnosis：

- 同一失败经过多轮 Minimal Fix 仍稳定出现；
- 修复一个问题持续破坏另一项合法行为；
- Root Cause 在多个层之间反复漂移且证据不足；
- 需要大量 case-specific 条款才能维持通过；
- 当前模型能力或输入条件使测试无法可靠执行；
- 剩余问题已达到 Core / Scope / System-level 风险。

升级后重新检查 Rule、Evidence、Scope 与模型限制；若仍无法形成可验证修复，Final Verdict 必须是 `NOT READY`，不能继续消耗生成次数追求偶然成功。

## 25. Test Overfitting Protection

以下信号表明可能发生 Test Overfitting：

- 修改只让一个 TC 通过，无法解释更广泛行为；
- 增加大量 subject-specific 或 case-specific wording；
- 修复没有对应 Reference / Rule Evidence；
- 原有 Core、Variation 或邻近风险 Case 退化；
- 测试 Prompt 变成 Candidate 之外的定制 Prompt；
- 为提高通过率删除困难但合法的 Case；
- 通过固定构图、输入或 Variation 获得表面一致性。

Overfit 修订不得进入最终基线。应撤回或缩小修订，恢复可比较版本，并重新定位 Root Cause。

## 26. Test Coverage Gate

Phase 4 结束前必须形成 Coverage Matrix，能够回答：

- 哪些 active core INV 已被 Core TC 覆盖；
- 哪些 active core / important VAR 已被 Variation 或 Boundary TC 覆盖；
- 哪些 active core / important ANTI 已被 Stress TC 覆盖；
- 哪些核心 SK 已获得 execution coverage；
- 哪些核心 VR / PR / QR 已通过 SK 与 TC 路径被实际实现或校准；
- Prompt Construction、Quality Evaluation、Scope Boundary 与 Known Risks 由哪些 Case 覆盖；
- 哪些 Entity 仍未测试，原因与影响是什么。

Phase 3B 的 Pending Test Coverage 必须在 Phase 4 被解决、转为正式 TC，或被明确记录为 `currently untestable`。

active core / identity-critical INV 没有正式 TC Coverage 时不得 Freeze。若某项 important 但非身份决定性要求当前不可测试，只有在原因、影响、接受者与未来触发条件均被记录，且不会使核心稳定性无法证明时，才可考虑 `FREEZE V1 WITH KNOWN LIMITATIONS`。无法验证核心身份或主要职责时必须 `NOT READY`。

## 27. Test Suite Status

完整 Suite 的正式状态为：

```text
PASS
PASS WITH ISSUES
FAIL
```

### PASS

Required Coverage 完成，无未解决 Critical / Major system failure，所有正式修订完成 Retest 与 Regression，只有可忽略的非系统性 variance。

### PASS WITH ISSUES

核心与必需 Coverage 成立，无未解决 Critical Failure 或 Systematic Major Failure，但存在已记录、非阻断的 variance、subject-specific difficulty 或可接受 limitation。

### FAIL

存在未解决 Core Failure、Systematic Stress Failure、阻断性 Variation / Boundary Failure、Regression、Scope Leakage、关键 Coverage Gap 或无法控制的系统性问题。

若存在 required TC 为 `BLOCKED`，Suite 保持 incomplete，不能签发 PASS 或 PASS WITH ISSUES；Final Freeze Decision 为 `NOT READY`，直到阻塞解决或按 Known Limitation 规则正式处理。Suite Verdict 不能只由通过率或平均分决定。

## 28. Freeze Criteria

Final Freeze Decision 只能是：

```text
FREEZE V1
FREEZE V1 WITH KNOWN LIMITATIONS
NOT READY
```

只有同时满足以下核心条件，才允许 Freeze：

### Core Stability

Core Cases 在预先定义的测试范围内稳定通过；不存在未解决的 core INV violation。

### Variation Tolerance

有代表性的合法 VAR 保持 Visual Family，没有明显 Style Drift 或 Template Lock。

### Stress Resistance

不存在稳定重复的 Critical Stress Failure；重要 ANTI Guardrail 的表现可解释且不依赖 Prompt Rescue。

### Boundary Control

重要 VAR Boundary 能区分 Still valid、Borderline 与 Outside，既不过窄也不过宽。

### Traceability Coverage

核心 INV、重要 VAR、重要 ANTI 与核心 SK 获得合理 TC Coverage，Pending Test Coverage 已解决或按限制规则处理。

### Evidence-based Refinement

所有进入最终基线的重要修订都有 Test Evidence、Root Cause、最小改动记录与 Traceability Revision。

### Retest and Regression

最新版本的所有受影响修订均完成 Retest 与适当范围的 Regression，且相关 Phase 2 / 3A / 3B Gate 已重新通过。

### Scope Integrity

测试与修订没有引入新的 Scope Leakage，没有用路由、用途决策或其他外部职责补偿生成问题。

### Artifact and Version Integrity

Test Artifacts、Final Test Report、Candidate 与 System Rules 指向同一最终受测版本；没有选择性遗漏失败结果或伪造统计。

### Known Limitations

剩余限制已明确记录其证据、影响、适用范围与未来 Unfreeze Trigger，并且不破坏目标 Skill 的核心职责。

`FREEZE V1` 表示没有影响正式使用的已知阻断问题。`FREEZE V1 WITH KNOWN LIMITATIONS` 只允许非阻断且已接受的限制；它不能掩盖 core failure、systematic critical pattern、required blocked test 或失败的 Regression。

Freeze 不要求 `100% single-generation perfection`。它表示在当前模型、当前测试范围、当前 Visual System 与已记录限制下，目标 Skill 已达到稳定、可解释、可重复使用的质量水平。单次成功生成永远不足以 Freeze。

## 29. Unfreeze Principle

以下变化可以触发 Unfreeze：

- 生成模型或关键生成环境发生实质变化；
- 发现新的系统性 Failure 或 Regression；
- Reference Set 显著变化；
- Purpose / Scope 改变；
- Visual System、Rule Strength、核心 SK 或重要 Guardrail 大幅修改；
- Known Limitation 的风险升级。

正式路径为：

```text
Unfreeze reason
↓
Closest responsible phase
↓
Re-run affected upstream gates
↓
Static Audit
↓
Test / Retest
↓
Regression
↓
New Freeze Decision
```

本 Protocol 只定义原则，不建立版本管理系统。Frozen 状态不得被无记录修改。

## 30. Required Test Artifacts

Phase 4 至少需要支持以下逻辑 Artifact。具体文件名、目录、Schema 与模板由 Prompt 8 定义；不得因未来合并文件而丢失职责。

### 30.1 `test_cases`

定义 TC ID、Case Type、upstream targets、input scenario、test purpose、challenge、generation plan 与 Traceability location。

### 30.2 `expected_behavior`

在生成前定义必须成立、允许变化、边界、Hard Fail、非系统性 variance 与失败含义。

### 30.3 `evaluation_rubric`

从 active QR 构建两层评估方式，记录 Hard Fail 与可观察的 Visual-family checks，不新增视觉标准。

### 30.4 `test_results`

记录每个 attempt 的 Case ID、原始输入、实际 Prompt、环境、输出引用、Hard Fail、Rubric 结果、状态、主要问题、Failure Attribution、Confidence 与证据。所有尝试均保留，不只保留最佳结果。

### 30.5 `refinement_log`

记录：

```text
Failure
→ Diagnosis
→ Minimal Fix
→ Gate Revalidation
→ Retest
→ Regression
```

并满足第 20 节的完整字段责任。

### 30.6 `final_test_report`

汇总 Test Scope、环境、Case 与 attempt 结果、Coverage、Failure Taxonomy、Systematic / Isolated 判断、Refinements、Retest、Regression、Remaining Known Limitations、Suite Verdict、Freeze Decision 与 Freeze Rationale。

Pass rate 可以作为描述性信息，但不得伪造，也不能替代 Hard Fail、Coverage、Regression 与 Freeze Criteria。

## 31. Static Audit and Phase Boundary

必须保持：

```text
Static Audit ≠ Generation Test
```

- Phase 3B 检查 Candidate 是否正确编译上游系统；
- Phase 4 检查真实生成行为是否成立。

因此 `Static Audit PASS` 与 `Generation Test FAIL` 可以同时成立；后者触发诊断，而不是否定 Static Audit 的职责。

Phase 4 可以：

- 创建 TC 与 Test Artifacts；
- 执行有界的真实生成与评价；
- 基于实际证据诊断失败；
- 对 Candidate 做合同允许的局部修订；
- 发起 Minimal Upstream Rollback；
- 完成 Retest、Regression 与 Freeze Decision。

Phase 4 不得：

- 修改或重排 Reference Set 以提高通过率；
- 静默修改 Reference Audit、Analysis 或 Phase 2 System Rules；
- 绕过失效的 Phase 2 / 3A / 3B Gate；
- 用人工超强 Prompt 救援 Candidate；
- 无限生成直到偶然成功；
- 将单次 Model Variance 直接视为系统性失败；
- 将系统性失败归咎于随机性；
- 通过删除合法 VAR、降低 Rubric 或删减困难 Case 制造通过；
- 创建新的视觉方向或扩大 Scope；
- 在 Retest、Regression 或当前 Static Audit 未通过时 Freeze；
- 无证据修改 Frozen Skill。

## 32. Protocol Completion Check

Phase 4 只有在以下事实均有真实 Artifact 证明时才可结束：

- 四类 Case 已按 active INV / VAR / ANTI / Boundary 生成；
- 每个 TC 有明确 Traceability 与预先定义的 Expected Behavior；
- Prompt 来自 Candidate，未使用 Prompt Rescue；
- 所有实际生成均被记录并完成两层评价；
- FAIL 与重复偏差已完成 Failure Attribution 与 Root Cause Diagnosis；
- 系统性与孤立失败已区分；
- 每项正式修订符合 Minimal Fix 并有 Refinement Log；
- 被修改层的 Gates 已重新验证；
- Retest 与 Regression 已完成；
- Variation / Anti-pattern Regression 没有显示 Template Lock；
- Coverage Matrix 已完成，Untested Invariant 已处理；
- required BLOCKED Case 已解决或 Final Decision 为 NOT READY；
- Remaining Known Limitations 已记录；
- Final Test Report 与 Freeze Decision 已完成；
- 没有执行任何 Phase 4 Forbidden Mutation。

如果任一事实缺失，不得用计划、推测或历史成功记录替代当前 Build 的实证结果。

## 33. Protocol Boundary

本文件不负责：

- 创建 `Templates/build_manifest.md`；
- 创建 `Templates/test_suite_template.md`；
- 创建 Builder 自身或任何目标 Image Skill 的 `SKILL.md`；
- 为具体 Image Skill 创建真实 TC；
- 创建或写入 `Tests/*`；
- 运行图片生成、真实测试或 Historical Backtest；
- 修改历史成功 Skill；
- 预设任何领域专属测试对象、视觉风险、风格词或 Rubric；
- 重新设计 Traceability Schema；
- 在没有真实 Phase 4 Evidence 时签发 Freeze。

