---
name: loop
description: >-
  Generate the autonomous execution engine from a goal and VISION.md — DOD.md
  (what counts as done), LOOP.md (how each round runs), and PROGRESS.md (the
  ledger) — so any agent can pick it up and drive the project round by round.
  Use when the requirements are written and need turning into an auto-runnable
  development flow, or when start reaches the engine-generation step.
---

你要生成三份文档。它们合起来是一台引擎:一个从没见过这个项目的 agent,读完就能自己开跑,每轮啃一个目标,直到全部完成。

三份的分工不能混:**DOD 是法官(什么算完成),LOOP 是工头(每轮怎么干),PROGRESS 是账本(干到哪了)。**

骨架分别在 `templates/DOD.md`、`templates/LOOP.md`、`templates/PROGRESS.md`。`LOOP.md` 几乎可以照抄,`DOD.md` 要你按项目切 Phase,`PROGRESS.md` 只是初始化。下面讲照抄骨架之外要动脑的地方。

输入是 goal 与 `VISION.md`(尤其它的成功标准和 User Case)。

## DOD 要动脑的地方

把项目切成**有序的 Phase**——每个 Phase 结束能拿到一个可验证的东西,后一个依赖前一个。最后一个 Phase 是 E2E,**对应 VISION 每个 User Case,一个都不能漏**。

每个 DoD 项旁边直接写出**能验证它的那条可重跑命令**。写不出命令的项还太模糊,拆细或改写。证据式勾选的纪律写在 DOD 模板顶部,那是它的使用点。

## PROGRESS 要动脑的地方

把 `DOR.md` 的 Blockers 逐条搬进 PROGRESS 初始状态。那是 agent 第一轮要面对的现实,漏搬就会被当成已就绪。

## Done when

三份文档落地且自洽:DOD 的 Phase 覆盖 VISION 全部成功标准与 User Case;LOOP 的每轮循环指向 DOD;PROGRESS 已初始化并继承了 DOR 的 blocker。此时这套引擎可以交给任意 agent 自主运行。
