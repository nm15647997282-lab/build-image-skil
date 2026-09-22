# build-image-skill

> A reference-driven compiler for building reliable AI image-generation Skills.

`build-image-skill` 是一个用于构建 AI 图片生成 Skill 的元 Skill。它不直接生成某一种固定风格的图片，而是把一组参考图逐步转化为可执行、可审计、可测试、可回归并最终冻结的 Image Generation Skill。

## 核心流程

```text
Reference Images
→ Reference Set Audit
→ Reference Analysis
→ Visual System Specification
→ Skill Compilation
→ Consistency Audit
→ Real Generation Test
→ Refinement + Regression
→ Freeze
```

目标不是偶然生成一张相似图片，而是在不同主体、内容和合法变化下，仍能稳定生成属于同一视觉家族的结果。

## 六阶段架构

| 阶段 | 作用 | 主要产物 |
| --- | --- | --- |
| Phase 1A | 审核参考图集合的可靠性 | Reference Set Audit |
| Phase 1B | 提取共享视觉语言 | Reference Analysis |
| Phase 2 | 将分析编译为执行规则 | Visual / Prompt / Quality Rules |
| Phase 3A | 编译目标图片 Skill | Candidate `SKILL.md` |
| Phase 3B | 独立检查一致性和可追溯性 | Skill Audit |
| Phase 4 | 真实生成、修正、回归和冻结 | Test Report + Freeze State |

正常流程不允许跳阶段。上游证据发生变化时，系统会回滚到最近的责任阶段，并重新执行所有失效的下游检查。

## 设计原则

- 先审核完整 Reference Set，再分析或构建。
- 按证据强度区分核心参考、辅助参考、歧义项和离群项。
- 不补写参考图没有支持的视觉风格。
- 明确区分不变量、允许变化、偶然细节和反模式。
- 将描述性分析与可执行规则分开。
- 保持目标 `SKILL.md` 简洁，只承载运行时需要的内容。
- 在真实生成测试前进行独立静态审计。
- 通过真实生成、最小修正、重测和回归后才能 Freeze。

## 必需输入

一次新 Build 至少需要：

```yaml
skill_name: target-image-skill
purpose: 目标 Skill 负责生成什么
references_path: 参考图所在路径
scope_boundary: 目标 Skill 负责与不负责的范围
optional_context: 可选背景信息
```

字段定义及验收规则见 [`input_contract.md`](input_contract.md)。视觉事实以参考图为最高依据，文字输入只定义任务责任和边界。

## 项目结构

```text
.
├── SKILL.md                 # Builder 的执行与状态机入口
├── project_brief.md         # 项目目标、原则和成功标准
├── input_contract.md        # 最小输入契约
├── System/                  # 各阶段协议、编译器和测试规则
├── Templates/               # Manifest、Traceability、审计和测试模板
├── Reference_Implementation/# 两套历史六 Prompt 实现
└── Tests/                   # Builder 一致性审计记录
```

## 使用方式

1. 准备目标 Skill 的参考图集合。
2. 按 [`input_contract.md`](input_contract.md) 提供最小输入。
3. 从根目录 [`SKILL.md`](SKILL.md) 启动新 Build，或通过已有 `build_manifest.md` 恢复 Build。
4. 严格按状态机完成六个阶段和各自 Exit Gate。
5. 只有真实测试、重测和回归全部通过后，才将目标 Skill 标记为 Frozen。

构建期间会逐步生成 Manifest、Traceability、Reference Audit、Reference Analysis、三层规则、目标 Skill、静态审计和测试报告。文件存在本身不代表阶段完成，Exit Gate 才是正式判定。

## 当前状态

- Builder 静态一致性审计：`PASS`
- Critical / Major / Minor：`0 / 0 / 0`
- 当前结论：`READY FOR HISTORICAL BACKTEST`
- 尚未执行：历史回测、真实图片生成、Builder Freeze

完整审计记录见 [`Tests/builder_consistency_audit.md`](Tests/builder_consistency_audit.md)。

## 参考实现

项目保留两套已经验证过的 V1 六 Prompt 流程作为回归基准：

- `image-broll-document`
- `image-broll-object`

它们用于检验通用 Builder 是否保留了原流程的高复现机制，不是新的 Source of Truth。

## 文档入口

- [Project Brief](project_brief.md)
- [Input Contract](input_contract.md)
- [Builder Skill](SKILL.md)
- [System Protocols](System/)
- [Artifact Templates](Templates/)
- [Consistency Audit](Tests/builder_consistency_audit.md)

## License

本项目暂未声明开源许可证。在许可证明确前，默认保留所有权利。
