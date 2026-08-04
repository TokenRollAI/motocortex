# motocortex

> all skill you need for agent coding.

**motocortex 是 [TokenRoll](https://github.com/TokenRollAI) 面向开发的通用 skill/plugin。** 它不绑定任何具体产品——把它放进任意仓库,就能把一个粗糙的想法变成一套可以直接交给自动 agent 运行的文档。

其它语言:[English](./README.md)

## 它做什么

你只需要跑一条命令 `/start`,剩下的它带着你走:先把项目现状读进来,再就你**没意识到**的关键问题逐个追问,最后落下五份文档——`VISION.md` / `DOR.md` / `DOD.md` / `LOOP.md` / `PROGRESS.md`。之后 `/goal` 驱动仓库一轮接一轮跑:agent 挑一个未勾选项,用可复现证据验证,勾掉它,继续,直到全部完成或只剩 blocker。

## 流程

```
/start                                   ← 生成阶段:你唯一要记的命令
  1. 收集 context   (读 repo、既有约定、已定型的技术栈)
  2. /grill         ← 追问澄清,直到没有静默假设 → 落成 DECISIONS.md
  3. /frame         ← 产出 VISION.md(要做什么)+ DOR.md(开工前的就绪风险清单)
  4. /loop          ← 从 goal 生成 DOD.md(什么算完成)
                      + LOOP.md(每轮怎么干)+ PROGRESS.md(进度账本)

/goal                                    ← 执行阶段:驱动仓库自主跑
  按 LOOP.md 的状态机一轮接一轮:啃一个 DoD 项 → 可复现证据验证 → 勾选
  直到全部完成,或只剩 blocker 时停下把清单留给你
  (没装成命令?把 LOOP.md 顶部"如何启动"那段粘进任意 agent 会话)
```

## skills

| skill | 触发 | 职责 | 产物 |
|---|---|---|---|
| `start` | 人手动 | 编排入口:把下面几步串起来 | 全部五份文档 |
| `grill` | 模型自动 | 收集 context + 追问未澄清的高质量问题,直到边界清空 | `DECISIONS.md` |
| `frame` | 模型自动 | 把 DECISIONS 写成需求真源与就绪清单 | `VISION.md` `DOR.md` |
| `loop` | 模型自动 | 从 goal 生成自动执行引擎 | `DOD.md` `LOOP.md` `PROGRESS.md` |
| `goal` | 人手动 | 驱动已备好的仓库,按 LOOP 状态机跑到完成或只剩 blocker | 追加 `PROGRESS.md` |

两层结构:`start`/`goal` 负责**编排**(人手动触发),`grill`/`frame`/`loop` 是**可复用纪律**(被 `start` 拉入)。

## 设计原则

- **事实自己查,决策交给你**:能从环境查到的,不问;真正要你拍板的,一次一个、每问附推荐答案。
- **不追问已定型的**:项目已有成熟技术栈或既有约定,记录并确认,不重新访谈。
- **勾选靠证据**:`DOD.md` 里每一项的勾选依据,是可复现的证据(命令及其输出),不是"我觉得写完了"。

## 安装

作为 Claude 插件安装(v0.0.1):

```
/plugin marketplace add TokenRollAI/motocortex
/plugin install motocortex
```

或把 `skills/` 下的目录软链到你的 skills 目录(如 `~/.claude/skills`)。

### 其他 runtime(Codex / OpenCode / Cursor / Antigravity / pi)

本仓库只发布 Claude 格式。source of truth 是 `skills/` + `.claude-plugin/`;其余 runtime 的格式不进仓库,而是用 [acplugin](https://github.com/tokenRollAI/acplugin) 按需现转。可以直接从 GitHub 转到你本地:

```
# 目标平台自选:codex,opencode,cursor,antigravity,pi
npx -y acplugin convert TokenRollAI/motocortex --to cursor -o ~/某目录 --all
```

转完把对应 runtime 指向生成目录即可(Cursor、Codex 还会带一份 `marketplace.json`)。转之前可先 `npx -y acplugin scan TokenRollAI/motocortex` 确认五个 skill 都被扫到。
