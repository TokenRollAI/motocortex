# motocortex

> TokenRollAI 自用的 agent skills：澄清关键选择，把目标推进到有证据的完成，并解释架构、性能与 prompt 决策背后的判断依据。

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
| `start-a-goal` | 用户触发 | 通过可恢复的执行文档与证据，把目标推进到验证完成 | `VISION.md`、`DOR.md`、`DOD.md`、`LOOP.md`、`PROGRESS.md` |
| `grill` | 模型触发 | 澄清影响结果的开放决策，记录假设与延后处理的问题 | `DECISIONS.md` |
| `architecture-design` | 模型触发 | 设计或审查架构、技术选型、边界与演进，排除推测性复杂度 | 按任务交付决策、设计或审查 |
| `performance-optimization` | 模型触发 | 从负载目标与证据出发设计、诊断、优化或审查性能 | 按任务交付策略、诊断或已验证改动 |
| `better-prompt` | 模型触发 | 用聚焦的领域指南生成、诊断或优化 prompt | 优化后的 prompt、runtime 建议、最小评测 |
| `interaction-design` | 模型触发 | 从用户目标、心智模型与每个动作的完整生命周期出发设计、审查或实现交互 | 按任务交付流程设计、标注证据类型的审查、已验证的 UI 改动或交互规格 |
| `study-codebase` | 模型触发 | 根据源码证据解释项目用途、架构、依赖、核心实现与可迁移的设计经验 | 学习笔记、小型实现练习提案、按需发布的 GitHub Gist |

`start-a-goal` 是唯一的用户触发入口。其余六个是模型触发的纪律：`grill` 在关键决策需要澄清时由 `start-a-goal` 拉入，也可以在不确定性妨碍有效推进时单独使用；`architecture-design`、`performance-optimization`、`better-prompt`、`interaction-design` 与 `study-codebase` 彼此独立——任务确实需要时，模型根据 description 选择它们，它们之间没有调用或依赖。

## start-a-goal 如何工作

```text
当前目标
└── start-a-goal
    ├── 核对当前意图与已有执行状态
    ├── 按需澄清关键选择 → grill → DECISIONS.md
    ├── 维护文档包 → VISION + DOR + DOD + LOOP + PROGRESS
    └── 推进已授权工作 → 验证结果或说明阻塞
```

复用已有文档前，先核对它们与当前目标和项目状态是否一致。匹配的文档包可以恢复；缺失或过时的部分依据已确定的决策修复；无关目标放在独立目录。五份执行文档分别保存 `VISION.md`（结果与范围）、`DOR.md`（就绪缺口与依赖）、`DOD.md`（验收与证据）、`LOOP.md`（执行判断与完成条件）、`PROGRESS.md`（当前状态与证据历史）。

这些是职责，不是必须依次通过的阶段。Agent 按实际依赖和反馈选择工作，及时记录决策，通过命令、可重复的用户操作流程或明确的人工验收验证结果。最终状态的必需回归必须通过才能完成；因阻塞交接仍属于未完成的工作。

## 怎么使用

安装后，把一个粗糙目标交给 agent：

```text
使用 start-a-goal 把这个目标做到完成：<你的目标>
```

有些宿主会把用户触发的 skill 显示成斜杠命令，此时同一个动作可能显示为 `/start-a-goal`。在需要时回答关键澄清问题，然后让 agent 持续推进；已有决策与授权直接复用。如果宿主在完成前结束执行，通过它支持的继续机制恢复，文档包会保存当前状态。

模型触发的纪律会在任务匹配 description 时自动生效，也可以直接点名：

```text
使用 grill，在对这个想法作出承诺前，把影响结果的关键决策问清楚。

审查这个服务边界，并推荐满足这些质量要求的最简单架构。

诊断这次延迟回归，建立有代表性的基线，只保留证据支持的优化。

围绕意图、原因和判断依据重写这份 prompt，并给出检验行为是否改善的具体用例。

审查这个结账流程的交互：缺失的状态、错误恢复、撤销、键盘可达性与专家快捷方式。

使用 study-codebase 调研 <仓库 URL 或本地路径>，解释核心设计，并把学习笔记发布为 GitHub Gist。
```

## study-codebase 如何工作

调研从一个具体用户行为出发，沿确定版本的源码追踪，解释项目用途、架构与关键依赖、核心实现，以及值得学习的设计。正文用自然语言和具体例子讲解，不打开源码链接也能理解；大部分证据集中在文末的源码阅读附录，仅在需要即时核验的关键处保留少量行内引用。设计动机的推断与未经验证的行为明确标注。最后给出一条精简的源码阅读路线和一个小型实现练习提案，帮助读者把理解转化为实践；真正实现练习属于后续任务。

产物是一份使用用户语言的独立 Markdown 笔记。用户要求 Gist 时，skill 发布完整笔记并核对上传内容与可见性。优先沿用指定的可见性，否则使用 secret Gist：不公开列出，但持有链接的人都能读取。发布需要已认证的 GitHub 工具或 CLI；不可用时保留完整本地笔记，并明确说明发布阻塞。仅要求调研时，交付保留在本地。

## 设计原则

- **解释原因，留出判断空间。** 说清意图、因果取舍与可观察的完成条件；仅在正确性、授权、可复现性或用户指定流程确实要求顺序时固定步骤。
- **事实自己查，关键选择交给用户。** 检查相关 context，只追问会改变工作的选择；普通可逆决策在已有意图与授权范围内自行处理。
- **不重新争论已定选择。** 既有技术栈和约定直接记录并复用。
- **勾选必须有证据。** 验收依据是命令、可重复的用户操作流程或明确人工审查的实际结果。必需回归失败就不能完成，也不能通过降低目标让实现变得正确。
- **架构从作用力出发，不从模式出发。** 让业务结果、质量场景、约束与可信变化决定结构和技术；每一层与每个扩展点都要证明自己的代价值得。
- **性能是负载下的行为。** 先定义负载与目标、找到真实限制，再选择取舍与证据相符的变换。
- **Prompt 是契约，不是咒语。** 可移植核心保持精简，只加入会改变行为的指南，并用代表性样例验证。
- **交互是为了降低认知成本。** 从用户、任务与证据出发；按频率、风险、可逆性与熟练度权衡互相冲突的原则；把每个动作设计成恢复成本低的完整状态生命周期；通过实际走流程评判界面，而不是看截图。
- **学习沿着机制展开。** 用源码追踪具体行为，同时解释设计收益与代价，再提炼一个能检验理解的小型练习。
- **用文件承载状态。** 决策、就绪风险、完成标准、执行规则和进度可以跨 agent、跨 context window 延续。

## 仓库结构

```text
skills/
├── start-a-goal/
│   ├── SKILL.md      # 目标负责与执行判断
│   └── templates/    # VISION、DOR、DOD、LOOP、PROGRESS 骨架
├── grill/
│   └── templates/    # 持久化决策记录
├── architecture-design/
├── performance-optimization/
├── better-prompt/
│   ├── references/   # 领域指南、模型适配、评测
│   └── templates/    # prompt 交付骨架
├── interaction-design/
│   ├── references/   # 交互模式、可用性评估、CLI、文案与本地化、AI 与 agent
│   └── templates/    # 交互规格与审查骨架
└── study-codebase/
    ├── references/   # Gist 发布与核验
    └── templates/    # 有源码证据的学习笔记与实现练习
```

`skills/` 是唯一的分发真源。每个 skill 在 `SKILL.md` 中保留判断纪律，把需要照抄的产物骨架放在 `templates/`，把按需加载的深度指南放在 `references/`。所有 skill 内容用英文书写。

增删 skill 时，同步更新两份 README 的 skills 表，并在本地验证发现结果：

```bash
npx -y skills add . --list
```
