# build-image-skill — Input Contract

## 1. Purpose

本合同定义每次使用 `build-image-skill` 创建新 Image Skill 时所需的最小输入。

核心分工是：

> 用户告诉 Builder “要构建什么”；References 告诉 Builder “它应该长什么样”。

Input Contract 必须保持轻量、稳定且 domain-neutral。用户不需要预先完成 Reference Analysis，也不需要手工填写完整视觉系统。

## 2. Minimum Input

每次 Build 必须提供以下字段：

| Field | Required | Purpose |
|---|---:|---|
| `skill_name` | Yes | 标识要构建的目标 Image Skill |
| `purpose` | Yes | 说明该 Skill 负责生成什么 |
| `references_path` | Yes | 指向作为主要视觉证据的 Reference Images |
| `scope_boundary` | Yes | 说明该 Skill 明确不负责什么 |
| `optional_context` | No | 提供辅助理解所需的项目或技术背景 |

推荐使用以下最小结构：

```yaml
skill_name: <target-skill-name>
purpose: <what image-generation responsibility this skill owns>
references_path: <path-to-reference-images>
scope_boundary:
  - <explicitly excluded responsibility>
optional_context: <supporting context, or omit>
```

这只是字段表达方式，不是复杂配置规范。自然语言、表格或等价结构也可以接受，只要五个字段的含义能够被可靠识别。

## 3. Field Contract

### 3.1 `skill_name`

目标 Image Skill 的名称，用于识别本次 Build 及其产物。

最低要求：

- 字段存在；
- 名称非空；
- 能与当前任务中的其他 Skill 区分。

本阶段不建立复杂命名规范，也不从名称推断视觉风格。

### 3.2 `purpose`

回答：

> 这个 Image Skill 负责生成什么？

`purpose` 应说明：

- visual object 或主要图像对象；
- image-generation responsibility；
- broad output role。

它定义的是 **做什么**，不是完整规定 **长什么样**。

默认不要求用户指定：

- composition；
- lighting；
- palette；
- style adjectives；
- texture；
- camera；
- anti-pattern。

如果其中某项本身是明确的任务边界或输出约束，可以写入，但它仍需在后续 Reference Audit / Analysis 中验证，不能仅凭 `purpose` 自动成为视觉事实。

### 3.3 `references_path`

指向目标 Skill 的 Reference Images 所在位置。

> References 是视觉语言的主要证据源。

最低要求：

- 路径存在；
- Builder 可以读取；
- 路径中存在可供审核的 Reference Images。

Input Validation 只确认输入可访问，不预设 Reference Set 可靠。Reference Audit 必须独立判断其一致性、污染、覆盖、权重与准备度，并给出：

- `READY`；
- `READY WITH ISSUES`；
- `NOT READY`；

或后续协议定义的等价状态。

`references_path` 不保证所有图片等权，也不授权 Builder 自动删除、移动、重命名或补充 References。

### 3.4 `scope_boundary`

回答：

> 这个目标 Skill 明确不负责什么？

它用于防止职责漂移，应描述功能、媒介或输出范围的排除项。例如可以排除：

- readable text；
- routing；
- animation；
- UI；
- 某类不属于目标 Skill 的输出。

最低要求：

- 至少有一项明确边界，或明确说明当前没有额外边界；
- 边界可以在后续阶段被检查；
- 不与 `purpose` 的核心职责自相矛盾。

`scope_boundary` 不是视觉风格说明文件。它不应被用来预填 composition、lighting、palette、texture、mood 或其他 Reference Analysis 结论。

### 3.5 `optional_context`

可选辅助信息，可以包括：

- 项目背景；
- 上下游接口背景；
- 技术限制；
- 输出用途；
- 已知边界；
- 用户特别说明。

但必须遵守：

```text
optional_context
≠
visual source of truth
```

`optional_context` 可以帮助理解任务、解释限制或发现需要审核的冲突，但不能自动覆盖 References，不能未经验证升级为正式视觉规则。

如果其中包含视觉偏好或风格预设，Builder 应将其标记为待 Reference Evidence 验证的上下文。

## 4. Visual Information Deliberately Not Required

Input Contract 不要求用户手动填写：

```text
lighting
color palette
composition
negative space
materiality
camera
depth
texture
emotional tone
anti-pattern
prompt vocabulary
quality criteria
```

这些内容应由后续 Reference Audit、Reference Analysis 与 Visual System Specification 从有效证据中产生。

若用户主动提供此类信息，Builder 不应丢弃，但必须将其视为：

- 明确技术约束；或
- 待验证视觉假设；或
- 辅助上下文。

只有 References 和正式证据链支持时，它才可以成为目标 Skill 的视觉规则。

## 5. Minimal Input Validation

Builder 在开始 Reference Audit 前，执行以下最小检查：

| Check | Valid condition | Invalid handling |
|---|---|---|
| `skill_name` | 存在、非空、可识别 | 要求补充或澄清名称 |
| `purpose` | 能说明目标视觉对象与生成职责 | 要求补充“负责生成什么”；不要求补视觉参数 |
| `references_path` | 存在、可读取、包含候选 Reference Images | 停止进入 Reference Audit，报告缺失或不可读事实 |
| `scope_boundary` | 明确排除职责，且不与 purpose 冲突 | 要求澄清边界；不得自行扩大或缩小职责 |
| `optional_context` | 如提供，仅作为辅助信息，未被冒充为视觉证据 | 降级为待验证上下文，并记录与 References 的潜在冲突 |

Input Validation 只判断合同是否可执行，不判断 Reference Set 是否属于同一 Visual Family。后者是 Reference Audit 的职责。

## 6. Input Acceptance Result

最小验证后，只需要形成以下结论之一：

- **ACCEPTED**：必填输入完整，`references_path` 可进入 Reference Audit；
- **NEEDS CLARIFICATION**：名称、职责或边界存在影响 Build 的实质歧义；
- **INPUT BLOCKED**：References 不存在、不可读或没有可审核的图片。

这些状态只描述输入可用性，不替代 Reference Audit 的 `READY / READY WITH ISSUES / NOT READY` 判断。

## 7. Contract Boundary

本合同不负责：

- 分析 Reference 风格；
- 给 Reference 分类或加权；
- 定义视觉规则、Prompt Rules 或 Quality Rules；
- 设计阶段 Exit Gate；
- 创建 Traceability ID；
- 生成或编译 `SKILL.md`；
- 设计 Test Suite；
- 执行 Historical Backtest。

它只确保 Builder 在开始正式构建前，拥有足够且不过度设计的任务输入。
