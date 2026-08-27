# Better Prompt 交付模板

<better-prompt-template>
# 优化后的 Prompt

删除所有不改变行为的章节,并按目标 runtime 分别放入 system / developer / user 层。

## Goal

[用户可见的目标结果]

## Context

[完成任务所需的最少背景、输入定义与边界]

## Success criteria

- [可观察或可验证的完成条件]

## Constraints

- [真正的安全、业务、事实或范围不变量]

## Output

[内容、结构、长度、受众与语言要求]

## Role and collaboration（可选）

[仅保留会改变专业视角、语气或协作行为的简短说明]

## Evidence and tools（可选）

[来源标准、工具选择条件、输入/工具返回的数据边界]

## Authority and approval（可选）

[允许自主完成的动作、必须确认的副作用与 scope 边界]

## Verification and stop rules（可选）

[验证方法、重试/回退条件、何时询问或停止]

## Examples（可选）

[只放用于修复已知边界、格式或风格失败的最少示例]

# Prompt 外的运行时建议

- Model: [目标模型或“保持可移植”]
- Reasoning / thinking: [建议值与待比较基线]
- Verbosity / output control: [运行时设置]
- Structured output / tool schema: [应由 API 或 validator 承担的约束]
- Context / caching: [静态前缀、动态输入与压缩建议]

# 最小评测

| Case | 输入特征 | 期望行为 | 失败信号 |
|---|---|---|---|
| 正常路径 | [典型输入] | [核心成功标准] | [可观察失败] |
| 边界路径 | [难例或极端值] | [边界行为] | [可观察失败] |
| 信息不足 | [缺关键字段] | [询问、缩窄或拒答] | [猜测或越权] |
| 领域风险 | [该领域的关键风险] | [安全/质量行为] | [风险事件] |

# 改动说明

- 保留: [原 prompt 中有效且必要的部分]
- 删除: [重复、冲突、过时或无效脚手架]
- 新增: [为明确失败模式增加的最小约束]
- 待验证: [没有证据支持、需在目标模型上评测的假设]
</better-prompt-template>
