---
name: better-prompt
description: >-
  Draft, diagnose, or optimize prompts for current high-performance models
  across direct response, reasoning, research, creative, coding/artifact, and
  tool-using agent work. Use when the prompt itself is the artifact or subject
  of diagnosis: a prompt is missing, bloated, brittle, legacy, model-specific,
  underperforming, or needs migration, simplification, or evaluation.
---

把 prompt 当成**任务契约**,不是激发模型能力的咒语。优化的目标不是让文字更长、更像规范,而是让目标模型以更少的歧义、冲突和无效约束,稳定交付用户真正要的结果。

## 先守住原意

输入可以是一份现有 prompt,也可以只是粗糙目标。先还原它的真实意图、受众、输入、交付物、成功标准与运行位置。区分稳定的 system/developer 规则、当前 user 任务、外部数据与工具返回;不同优先级的内容不要粗暴揉成一段。

能从现有 prompt、调用代码、工具 schema、评测或上下文查到的事实自己查。只追问会实质改变契约的决策;其余用最保守的合理假设推进,并把假设列在 prompt 外供用户确认。

若用户给的是现有 prompt,先保留其有效行为与授权边界,再做最小而有解释力的改动。若只有粗糙目标,先生成最小可用版本,不要预防尚未观察到的所有失败。

## 按任务形态路由

先判定主要任务形态,只读取相关领域指南。一个 prompt 同时包含多种形态时,读取必要的几份并明确主次,不要把全部领域规则堆进去。

| 任务形态 | 何时读取 |
|---|---|
| 直接回答与文本变换 | 问答、解释、摘要、提取、分类、改写、翻译:读 [direct-response.md](references/domains/direct-response.md) |
| 推理与决策 | 数学、分析、规划、比较、推荐、诊断:读 [reasoning-and-decisions.md](references/domains/reasoning-and-decisions.md) |
| 调研与综合 | 搜索、查证、引用、文献或竞品综合:读 [research-and-synthesis.md](references/domains/research-and-synthesis.md) |
| 编码与制品 | 代码、网站、文档、表格、演示或其它可验证制品:读 [coding-and-artifacts.md](references/domains/coding-and-artifacts.md) |
| 工具型 agent | 会调用工具、改变状态、长期运行或处理不可信外部内容:读 [tool-using-agents.md](references/domains/tool-using-agents.md) |
| 创意工作 | 构思、文案、故事、视觉方向、开放式设计:读 [creative-work.md](references/domains/creative-work.md) |

用户指定模型、要求迁移,或优化依赖模型当前能力时,再读 [model-adaptation.md](references/model-adaptation.md),并核对该模型当前官方指南。需要证明优化有效或设计回归集时,读 [evaluation.md](references/evaluation.md)。

## 先诊断,再改写

寻找真正会改变行为的问题:

- 目标、输入、完成标准或受众含糊;
- 指令重复、相互冲突,或所有要求都被写成最高优先级;
- 规定了与目标无关的步骤,压窄模型本可选择的有效路径;
- 只有“认真”“专业”“不要幻觉”等不可验收要求;
- 上下文堆积、来源不明,或数据与指令边界混淆;
- few-shot 示例没有修复已知失败,反而锚定错误模式;
- 把推理深度、verbosity、temperature 或 schema 等运行时控制伪装成通用自然语言技巧;
- 对工具、权限、副作用、证据、验证、重试与停止条件交代不足;
- 期待 prompt 单独解决权限隔离、结构约束或 prompt injection。

分清根因。若问题属于工具设计、权限、检索、模型选择、运行时参数、schema、服务端校验或缺少评测,明确指出并把它移到正确层;不要用更多 prompt 文字掩盖系统问题。

## 重写成最小任务契约

优先保留目标、必要 context、成功标准、硬约束与交付格式。只有在会改变行为时才加入角色、个性、固定流程、工具路由、授权、停止规则或示例。

- 描述目的地,让高性能模型自行选择普通推理与执行路径。路径本身涉及合规、可复现、授权或业务流程时,才固定步骤。
- 每条规则只写一次。绝对词留给真正不变量;判断题写成条件与决策标准。
- 用正面、可观察的行为描述期望结果。必要禁令说明替代行为。
- XML、Markdown 标题或分隔符只负责边界清晰;选择一种一致结构,不把格式当性能秘诀。
- 示例只用于难以文字定义的标签边界、风格、格式或反复出现的失败;使用最少、真实且互不矛盾的示例。
- 不要求模型复述完整隐藏思维链。要求关键假设、证据、计算、验证结果或简洁理由即可。
- 默认生成可移植核心;厂商特有参数、API schema 和缓存建议放在 prompt 外。

需要完整交付时,照 [templates/PROMPT.md](templates/PROMPT.md) 组织。删除所有空的可选模块;模板不是要求每份 prompt 都变成长文。默认在对话中返回可复制结果,只有用户要求时才写入文件或替换现有 prompt。

## 用失败模式验证

不要仅凭“读起来更专业”宣称优化成功。已有评测时,用相同模型、运行时参数与样例建立前后基线;没有评测时,至少给出覆盖正常输入、边界输入、信息不足与一项领域特有风险的最小测试集。

每次只改变一个有意义的模块,比较任务成功、事实与约束正确性、格式、成本、延迟、工具次数和失败类型。模型自评可帮助发现问题,但不能替代测试、validator、来源核验或人的偏好判断。

## Done when

交付物保留了用户原意与授权边界;核心 prompt 可直接使用、没有重复或冲突、只含会改变行为的模块;领域特有风险已处理;运行时配置与 prompt 分开;并提供足以验证改动的最小评测建议。若没有在目标模型上跑过评测,明确写成“待验证”,不声称它已经更好。
