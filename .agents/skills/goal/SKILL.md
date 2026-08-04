---
name: goal
description: >-
  Drive a repo that already has LOOP.md / DOD.md / PROGRESS.md — run the LOOP
  state machine round after round until everything is done or only blockers
  remain.
disable-model-invocation: true
---

这个仓库应该已经有 `LOOP.md`、`DOD.md`、`PROGRESS.md`(没有就先跑 `/start`)。你的活是照 `LOOP.md` 把它跑起来。

读 `LOOP.md` 与 `PROGRESS.md`,按 `LOOP.md` 的状态机一轮接一轮地跑,直到命中它定义的终止条件:

- 每轮结束把可复现证据(命令 + 输出)与勾选写进 `PROGRESS.md`。
- 你被授权自动编辑文件;commit 与其它外向动作按 `LOOP.md` 的纪律与宿主惯例判断。
- 全部 DoD(含 E2E)勾完 → 报告完成。
- 只剩 blocker、无项可推进 → 把 blocker 清单留在 `PROGRESS.md` 顶部,停下交给用户。

`LOOP.md` 是唯一权威,本 skill 不重复它的规则——照它跑。宿主一次只跑一轮时,重入本 skill 继续下一轮。
