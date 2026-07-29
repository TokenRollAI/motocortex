---
name: start
description: >-
  Turn a rough goal into a set of documents an autonomous agent can run on its
  own — gather context, grill for the unasked questions, then produce VISION,
  DOR, DOD, LOOP, and PROGRESS.
disable-model-invocation: true
---

你的任务是把用户手上一个还很粗糙的目标,变成一套**别的 agent 拿着就能自己跑**的文档。你负责编排,不亲自写每一份文档的正文——那是被你拉入的纪律 skill 的活。

从用户已经说的话里提取 goal。goal 不清楚就先问一句它,不要往下走。

**先查是否已有产物**。看仓库里是否已存在 `VISION.md` / `DOR.md` / `DOD.md` / `LOOP.md` / `PROGRESS.md`。若有,不要盲目覆盖——问用户走哪条:
- **续跑**:这些文档已就绪,跳过生成,直接 `/goal` 推进(或看 PROGRESS 定位到哪了)。
- **修订**:基于现有内容改(比如 goal 变了),把这次结论合并进已有文档,而不是重写。
- **另起**:确实要全新一套,写到带命名空间的路径(如 `<slug>/VISION.md`)或先归档旧的,别原地覆盖。
只有确认是全新项目、无同名文档时,才直接往下生成到默认路径。

按顺序走这四步,**中途不要 compact 或清空 context**——四步建立在同一份思考上。(注:自动压缩不受提示词控制;若中途被压缩,后续 skill 应回读已落盘的文档而非依赖记忆。)

1. **收集 context**。把项目现状读进来:仓库结构、既有约定、已定型的技术栈、README / 现有文档。分成"已定"和"未定"两堆。这一步的产出直接喂给下一步的 `/grill`,不必重复收集。

2. **追问澄清**。运行 `/grill`(带上步的 context)。它会就用户**可能没意识到**的关键问题逐个追问,直到没有静默假设。这一步是在为 DOR 备料。

3. **写需求与就绪清单**。运行 `/frame`,把澄清后的共识写成 `VISION.md`(要做什么、成功标准)与 `DOR.md`(开工前必须就绪的 context 输入)。

4. **生成自动执行引擎**。运行 `/loop`,从 goal 与 `VISION.md` 生成 `DOD.md`(什么算完成)、`LOOP.md`(每轮怎么干)、`PROGRESS.md`(进度账本)。

**Done when**:五份文档都落地。收尾时告诉用户五个文件路径,并给出启动方式——两种任选:

- 若 motocortex 已作为命令装进宿主:直接 `/goal`。
- 否则:把 `LOOP.md` 顶部"如何启动"那段提示词粘进任意 agent 会话。

并提醒一句:一次能连跑几轮取决于宿主,有的 harness 一次只跑一轮,需要反复重入才能跑到终止条件。
