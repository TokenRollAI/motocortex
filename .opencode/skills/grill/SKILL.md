---
name: grill
description: >-
  Gather the project's context, then interview the user one question at a time
  about the decisions they may not realize are open, until every branch is
  settled and nothing is silently assumed. Prepares the ground for DOR. Use when
  a goal is still rough and needs pinning down before any work, or when another
  skill needs the context clarified.
---

先把 context 吃进来,再把没澄清的东西问干净。这一步是在为 DOR 备料——问得越透,后面的自动 agent 越不会跑偏。

## 先收集,别先问

提问之前先把能拿到的 context 读进来——仓库结构、既有文档、技术栈(package.json / 配置 / CI)、既有约定、git log 近期热点。**能从环境查到的事实,自己查,不问用户。** 读完把结论分成两堆:**已定型** 和 **还没定**。(若 `/start` 已经收集过,直接用它的结论,不重复读。)

已定型的技术栈或既有约定,记录并向用户一句话确认即可,不重新访谈。追问只花在悬空的决策上。

## 追问悬空的决策

对"还没定的"那一堆逐个追问。目标是提出**用户可能自己都没意识到**的问题——边界情况、失败路径、隐含前提、相互冲突的需求。

用 **AskUserQuestion** 承载:一次一个决策,推荐答案放第一个选项并标"(推荐)",其余放真实的替代分支。问之前先给一句话说清这个决策为什么悬空、为什么现在要定,让用户带着 context 选。无法枚举成选项的才退回散文提问。

决策交给用户;事实缺口自己去环境里补。

用户暂时不可达时不要卡死:取最贴合现有 context 的默认值,把假设显式记下来,继续往下,回头让用户一次性追认。

## 落盘,别只留在对话里

达成的共识不要只活在会话上下文里——那会被自动压缩冲掉,`/frame` 也就无从依赖。把澄清结论写进 `DECISIONS.md`:三段就够——**已定型**(现有栈/约定)、**已拍板**(逐条:决策 + 一句理由)、**记录在案的假设**(用户不在场时取的默认值,待追认)。`/frame` 读它来写 VISION 与 DOR,不必回放对话。

## Done when

frontier 清空:决策树每个分支都被走到,没有静默假设;`DECISIONS.md` 已落盘。在用户确认达成共识之前,不要往下写文档。交给 `/frame`。
