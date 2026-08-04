---
name: frame
description: >-
  Synthesize the decisions grill captured into VISION.md (what to build, success
  criteria) and DOR.md (the readiness checklist before work starts). Use when
  the context is already clarified and needs writing up as the source of truth
  and readiness list, or when start reaches the drafting step.
---

`/grill` 已经把共识落进 `DECISIONS.md`。读它,把它综合成两份文档——**不要重新访谈**。(`DECISIONS.md` 是权威来源,不要只凭会话记忆写,那可能已被压缩。)

骨架分别在 `templates/VISION.md` 与 `templates/DOR.md`,照它填,每一节都填满。下面讲的是骨架填不出来的那部分——判断力。

## VISION 的两个着力点

写"要做什么",不写"怎么做"。重点在两处,它们是 DOD 的输入:

- **成功标准**:每条都要能被一条命令或一个 User Case 检验。验收不了的成功标准,改锐或删掉。
- **User Case**:把成功标准拆成具体场景("用户做了什么 → 得到什么"),后面一一对应 DOD 的 E2E 验收项。

## DOR 的着力点

DOR 是开工前的**就绪风险清单**,不是硬门槛。列动手前该就绪的 context 输入,按项目实际填成具体条目。已满足的勾上,缺的**标 blocker**——这些 blocker 会被 `/loop` 继承进 PROGRESS,缩小 agent 本次能推进的范围(依赖它的项被跳过),而不是让整件事停摆。漏写就丢。

技术栈结论落在 DOR 的"技术就绪":已定型的记录并勾上,新选的写明理由。

## Done when

`VISION.md` 与 `DOR.md` 都落地;VISION 的每条成功标准都可验收;DOR 的每一项要么已勾、要么标了 blocker。交给 `/loop`。
