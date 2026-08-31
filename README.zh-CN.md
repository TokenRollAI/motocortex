# motocortex

> TokenRollAI 自用的 agent skills：把一个粗糙目标盘问到没有静默假设，驱动它跑到有证据的完成，并在过程中做好架构、性能与 prompt 决策。

**motocortex 是 TokenRollAI 为自己的 agent 开发实践构建的 skills 集合。** 它是公开的，欢迎任何人安装，但它记录的是我们自己的工作方式，而不是试图适配所有工作流：有主张的默认值、证据门控的进度推进、用文件（而不是会话记忆）承载全部状态。它会随我们的实践演进，包括不兼容的改动。

其它语言：[English](./README.md)

## 快速开始

使用开放的 [`skills` CLI](https://github.com/vercel-labs/skills) 直接从 GitHub 安装：

```bash
npx skills add TokenRollAI/motocortex
```

安装器会直接发现仓库中的 `SKILL.md`，再让你选择需要的 skills、目标 agents 和安装范围。不需要 npm package，也不需要任何 runtime 专用适配层。

常用变体：

```bash
# 预览可用的 skills
npx skills add TokenRollAI/motocortex --list

# 安装到用户级，而不是当前项目
npx skills add TokenRollAI/motocortex --global
```

## Skills

| skill | 触发方式 | 职责 | 产物 |
|---|---|---|---|
| `start-a-goal` | 用户触发 | 端到端接管一个目标：澄清、生成执行文档、驱动循环直到完成或只剩 blocker | `VISION.md`、`DOR.md`、`DOD.md`、`LOOP.md`、`PROGRESS.md` |
| `grill` | 模型触发 | 检查 context，然后一次一个决策地追问用户，直到没有静默假设 | `DECISIONS.md` |
| `architecture-design` | 模型触发 | 设计或审查架构、技术选型、边界与演进，排除推测性复杂度 | 按任务交付决策、设计或审查 |
| `performance-optimization` | 模型触发 | 从负载目标与证据出发设计、诊断、优化或审查性能 | 按任务交付策略、诊断或已验证改动 |
| `better-prompt` | 模型触发 | 用聚焦的领域指南生成、诊断或优化 prompt | 优化后的 prompt、runtime 建议、最小评测 |

`start-a-goal` 是唯一的用户触发入口。其余四个是模型触发的纪律：`grill` 被 `start-a-goal` 在澄清阶段拉入，也可以在任务太模糊时单独使用；`architecture-design`、`performance-optimization` 与 `better-prompt` 彼此独立——任务确实需要时，模型根据 description 选择它们，它们之间没有调用或依赖。

## start-a-goal 如何工作

```text
粗糙目标
└── start-a-goal
    ├── 澄清 → grill → DECISIONS.md
    ├── 定型 → VISION.md + DOR.md
    ├── 引擎 → DOD.md + LOOP.md + PROGRESS.md
    └── 驱动 → 运行 LOOP 状态机，直到完成或只剩 blocker
```

对已经有执行文档的仓库，`start-a-goal` 跳过生成，直接进入驱动。五份执行文档组成一个任意 agent 拿到即可运行的包：`VISION.md`（要做什么、成功标准）、`DOR.md`（就绪风险）、`DOD.md`（什么算完成）、`LOOP.md`（每轮怎么干）、`PROGRESS.md`（进度账本）。

## 怎么使用

安装后，把一个粗糙目标交给 agent：

```text
使用 start-a-goal 把这个目标做到完成：<你的目标>
```

有些宿主会把用户触发的 skill 显示成斜杠命令，此时同一个动作可能显示为 `/start-a-goal`。回答澄清问题、检查生成的文档，然后让 agent 驱动执行。一次只跑一轮的宿主需要重入（手动"继续"、脚本或外层 loop）才能跑到终止条件。

模型触发的纪律会在任务匹配 description 时自动生效，也可以直接点名：

```text
使用 grill，在动手之前把这个想法里还悬空的决策问清楚。

审查这个服务边界，并推荐满足这些质量要求的最简单架构。

诊断这次延迟回归，建立有代表性的基线，只保留证据支持的优化。

把这份 prompt 重写成最小任务契约，并给出能证明改进的评测。
```

## 设计原则

- **事实自己查，决策交给用户。** 能发现的 context 由 agent 检查；真正影响结果的判断一次提出一个，并附推荐答案。
- **不重新争论已定选择。** 既有技术栈和约定直接记录并复用。
- **勾选必须有证据。** 每个 Definition of Done 条目都要有可复现命令或 User Case，不能只靠"我觉得完成了"。
- **架构从作用力出发，不从模式出发。** 让业务结果、质量场景、约束与可信变化决定结构和技术；每一层与每个扩展点都要证明自己的代价值得。
- **性能是负载下的行为。** 先定义负载与目标、找到真实限制，再选择取舍与证据相符的变换。
- **Prompt 是契约，不是咒语。** 可移植核心保持精简，只加入会改变行为的指南，并用代表性样例验证。
- **用文件承载状态。** 决策、就绪风险、完成标准、执行规则和进度可以跨 agent、跨 context window 延续。

## 仓库结构

```text
skills/
├── start-a-goal/
│   ├── SKILL.md      # 编排与驱动纪律
│   └── templates/    # VISION、DOR、DOD、LOOP、PROGRESS 骨架
├── grill/
├── architecture-design/
├── performance-optimization/
└── better-prompt/
    ├── references/   # 领域指南、模型适配、评测
    └── templates/    # prompt 交付骨架
```

`skills/` 是唯一的分发真源。每个 skill 在 `SKILL.md` 中保留判断纪律，把需要照抄的产物骨架放在 `templates/`，把按需加载的深度指南放在 `references/`。所有 skill 内容用英文书写。

增删 skill 时，同步更新两份 README 的 skills 表，并在本地验证发现结果：

```bash
npx -y skills add . --list
```
