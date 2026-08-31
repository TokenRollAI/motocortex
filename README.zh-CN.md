# motocortex

> 把粗糙目标变成可执行计划，做好架构与性能决策，再把脆弱 prompt 变成可靠契约的一组 agent skills。

**motocortex 是一套面向 agent 开发的纯 skills 集合。** 八个可组合的 skill 帮你澄清想法、定义并执行可验收项目、做好架构与性能决策，或独立优化 prompt，不绑定任何特定 agent 或 runtime。

其它语言：[English](./README.md)

## 快速开始

使用开放的 [`skills` CLI](https://github.com/vercel-labs/skills) 直接从 GitHub 安装：

```bash
npx skills add TokenRollAI/motocortex
```

安装器会直接发现仓库中的 `SKILL.md`，再让你选择需要的 skills、目标 agents 和安装范围。motocortex 不需要 npm package，也不需要任何 runtime 专用适配层。

常用变体：

```bash
# 预览全部八个 skills
npx skills add TokenRollAI/motocortex --list

# 只安装两个编排 skills
npx skills add TokenRollAI/motocortex --skill start --skill goal

# 安装到用户级，而不是当前项目
npx skills add TokenRollAI/motocortex --global
```

## 工作流

motocortex 包含五个彼此独立的入口：

```text
粗糙的项目目标
└── start
    ├── grill  → DECISIONS.md
    ├── frame  → VISION.md + DOR.md
    └── loop   → DOD.md + LOOP.md + PROGRESS.md

准备好的项目
└── goal       → 运行 LOOP 状态机，直到完成或只剩 blocker

架构决策、审查或演进
└── architecture-design → 有理由的结构、技术栈、边界与取舍

性能目标、规模风险或回归
└── performance-optimization → 有证据的设计、诊断或优化

粗糙或已有的 prompt
└── better-prompt → 可复制 prompt + runtime 建议 + 最小评测
```

`DECISIONS.md` 保存澄清阶段的交接信息。五份执行文档——`VISION.md`、`DOR.md`、`DOD.md`、`LOOP.md`、`PROGRESS.md`——组成另一位 agent 拿到即可运行的完整包。

## Skills

| skill | 触发方式 | 职责 | 产物 |
|---|---|---|---|
| `start` | 用户触发 | 编排目标澄清、需求定型和循环生成 | 全部五份执行文档 |
| `grill` | 模型触发 | 检查 context，拍板所有会影响结果的开放决策 | `DECISIONS.md` |
| `frame` | 模型触发 | 把已定决策写成需求真源和就绪风险清单 | `VISION.md`、`DOR.md` |
| `loop` | 模型触发 | 把目标变成可验证的自主执行引擎 | `DOD.md`、`LOOP.md`、`PROGRESS.md` |
| `goal` | 用户触发 | 驱动准备好的仓库，跑到完成或只剩 blocker | 更新 `PROGRESS.md` |
| `architecture-design` | 模型触发 | 设计或审查架构、技术选型、边界与演进，避免推测性复杂度 | 按任务交付决策、设计或审查 |
| `performance-optimization` | 模型触发 | 从负载目标与证据出发设计、诊断、优化或审查性能 | 按任务交付策略、诊断或已验证改动 |
| `better-prompt` | 模型触发 | 用聚焦的领域指南生成、诊断或优化 prompt | 优化后的 prompt、runtime 建议、最小评测 |

`start` 和 `goal` 是用户触发的编排 skill。`grill`、`frame`、`loop` 是由 `start` 组合起来的可复用纪律。`architecture-design`、`performance-optimization` 与 `better-prompt` 是彼此独立的模型触发纪律；任务确实需要时，模型根据 description 选择它们，它们之间没有调用或依赖。

## 怎么使用

安装后，把一个粗糙项目目标交给 agent，并明确让它使用 `start`：

```text
使用 start，把这个目标变成可以自主执行的计划：<你的目标>
```

有些宿主会把用户触发的 skill 显示成斜杠命令，此时同一个动作可能显示为 `/start`。回答决策问题、检查生成的文档，然后调用 `goal` 开始执行：

```text
使用 goal 驱动这个仓库，直到 Definition of Done 全部完成或只剩 blocker。
```

处理 prompt 时，把粗糙意图或已有 prompt 交给 `better-prompt`。它只加载当前任务相关的领域指南，不会把每个 prompt 都扩成同一个万能模板。

当系统或重大功能需要结构决策、技术选型、架构审查或演进路径时，直接提出架构问题：

```text
审查这个服务边界，并推荐满足这些质量要求的最简单架构。
```

当任务存在性能目标、瓶颈信号或可信的规模风险时再做性能工作。该 skill 会区分新系统的负载推演与已有系统的实测优化：

```text
诊断这次延迟回归，建立有代表性的基线，只保留证据支持的优化。
```

## 设计原则

- **事实自己查，决策交给用户。** 能发现的 context 由 agent 检查；真正影响结果的判断一次提出一个，并附推荐答案。
- **不重新争论已定选择。** 既有技术栈和约定直接记录并复用。
- **勾选必须有证据。** 每个 Definition of Done 条目都要有可复现命令或 User Case，不能只靠“我觉得完成了”。
- **架构从作用力出发，不从模式出发。** 让业务结果、质量场景、约束、现有 context 与可信变化决定结构和技术；每一层与每个扩展点都要证明自己的代价值得。
- **性能是负载下的行为。** 先定义负载与目标、找到真实限制，再按证据选择异步、批式、流式、并发、缓存或局部优化，并承担相应取舍。
- **Prompt 是契约，不是咒语。** 可移植核心保持精简，只加入会改变行为的指南，并用代表性样例验证。
- **用文件承载状态。** 决策、就绪风险、完成标准、执行规则和进度可以跨 agent、跨 context window 延续。

## 仓库结构

```text
skills/
├── start/
├── grill/
├── frame/
├── loop/
├── goal/
├── architecture-design/
├── performance-optimization/
└── better-prompt/
```

`skills/` 是唯一的分发真源。每个 skill 在 `SKILL.md` 中保留判断纪律，把需要照抄的产物骨架放在自己的 `templates/` 目录中。

增删 skill 时，同步更新两份 README 的 skills 表，并在本地验证发现结果：

```bash
npx -y skills add . --list
```
