# CLAUDE.md — 改 motocortex 这个仓库时的契约

这里是一个纯 skills 仓库。改它时维持下面的不变量。

`AGENTS.md` 是指向本文件的软链接（`ln -s CLAUDE.md AGENTS.md`），给不读 `CLAUDE.md` 的 runtime 用。两者永远是同一份内容：只改本文件，不要把 `AGENTS.md` 变成独立副本。

## 分层：SKILL.md 只讲怎么想，模板单独放

每个 `SKILL.md` 只写 **discipline（纪律与判断力）**——怎么想、怎么判定、边界在哪。要照抄的交付物骨架不写进 `SKILL.md`，而是放进该 skill 的 `templates/` 子目录（一个产物一个文件，如 `templates/VISION.md`）；`SKILL.md` 用一句话指向它。

判据（branch test）：`SKILL.md` 里每个分支都需要的内容 inline；只有产出文件时才照抄的骨架放进 `templates/`。这样 `SKILL.md` 保持可读，模板改动也不会搅动纪律。

模板文件里，把要照抄的骨架用 `<xxx-template>` XML tag 包起来，标记“这是照抄的结构，不是散文”。分节一律用 Markdown 标题，XML tag 只用于包模板。

## 两层 invocation

- **user-invoked**（`disable-model-invocation: true`）：负责编排，由人明确触发。目前是 `start-a-goal`。
- **model-invoked**（默认）：提供可复用纪律，由上层 skill 或模型按任务拉入。目前是 `grill`、`architecture-design`、`performance-optimization`、`better-prompt`。
- 硬约束：user-invoked 可以调用 model-invoked，永远不调用另一个 user-invoked。

## 语言

skill 的全部内容——`SKILL.md`、`templates/`、`references/`——一律用英文写，不出现中文（含全角标点）。中文只出现在 `README.zh-CN.md` 和本文件。

## Frontmatter

只使用 `name`、`description`；user-invoked 额外加入 `disable-model-invocation: true`。

model-invoked 的 `description` 保留丰富的触发措辞（“Use when …”）；user-invoked 的描述写成给人看的单行摘要。

## 写法

- 使用祈使句，散文优先：先讲为什么，再给规则；标题保持浅层。
- 正面提示优先。禁令只保留为无法正面表达的硬护栏，并说明替代行为。
- 完成标准写成可核对的 `Done when`。
- 事实自己查，决策交给用户。

## 纯 skills 分发

`skills/` 是唯一的内容与分发真源。仓库通过 `npx skills add TokenRollAI/motocortex` 直接安装，不维护 Claude plugin、runtime 专用 manifest 或生成镜像，也不为了分发新增 npm package。

修改任一 skill 后，用下面的命令确认 CLI 能发现预期的全部 skills：

```bash
npx -y skills add . --list
```

## 增删 skill 时同步

- 更新 `README.md` 与 `README.zh-CN.md` 的 skills 表和相关流程说明。
- 检查两份 README 的安装命令、skill 名称、触发层级与产物保持一致。
- 运行 `npx -y skills add . --list`，确认新增 skill 可发现、已删除 skill 不再出现。
- 若日后加入 router skill，同步它的路由图；路由里出现未提及或已删除的 skill，会让路由与仓库事实不符。
