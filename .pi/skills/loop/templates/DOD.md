# DOD 模板

产出 `DOD.md` 时照这个骨架填。Phase 数量与内容按项目定;最后一个 Phase 固定是 E2E,对应 VISION 的每个 User Case。

<dod-template>
# DOD(Definition of Done)

> 勾选纪律:一项能被勾上,当且仅当有一条可重跑的命令、且它的输出证明了这一项。
> 不是"我觉得写完了"。规格真源见 VISION.md。

## 全局完成定义

整个项目 Done = 以下同时成立:
1. 每个 Phase 的 DoD 清单全部勾选,依据是可重跑命令。
2. 最后一个 Phase 的 E2E 全部通过(对应 VISION 每个 User Case)。
3. <项目特有的全局条件,如"一键构建绿">

## Phase 0 — <名字>

**目标**:<这个 Phase 结束时拿到什么>
**DoD**:
- [ ] <可验收项,附能验证它的命令>
- [ ] ...

## Phase 1 — <名字>

**目标**:...
**DoD**:
- [ ] ...

## Phase N — E2E 验收

> 每条 E2E 对应 VISION 的一个 User Case,脚本化、可重跑。用复选框承载状态,遵守顶部的勾选纪律。

- [ ] **E2E-1** <Case 1>:<可重跑命令 + 期望输出>
- [ ] **E2E-2** <Case 2>:...
</dod-template>
