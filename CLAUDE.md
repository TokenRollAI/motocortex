# CLAUDE.md — 改 motocortex 这个仓库时的契约

这里是 skill 的仓库。改它时维持下面的不变量。

## 分层:SKILL.md 只讲怎么想,模板单独放

每个 SKILL.md 只写 **discipline(纪律与判断力)**——怎么想、怎么判定、边界在哪。**要照抄的交付物骨架不写进 SKILL.md**,收到该 skill 目录下的 `templates/` 子目录(一个产物一个文件,如 `templates/VISION.md`),SKILL.md 用一句话把它指出来(context pointer)。

判据(branch test):SKILL.md 里每个分支都需要的,inline;只有产出文件时才照抄的骨架,推到 `templates/`。这样 SKILL.md 保持可读,模板改动不动纪律。

模板文件里,把要照抄的骨架用 `<xxx-template>` XML tag 包起来——标记"这是照抄的结构,别当散文读"。分节一律用 markdown 标题,XML tag 只用于包模板。

## 两层 invocation

- **user-invoked**(`disable-model-invocation: true`):负责编排,人手动触发。`start`(生成)/ `goal`(执行)。
- **model-invoked**(默认):负责可复用纪律,被上层拉入。`grill` / `frame` / `loop`。
- 硬约束:user-invoked 可调 model-invoked,**永不调另一个 user-invoked**。

## frontmatter

只用 `name`、`description`,user-invoked 加 `disable-model-invocation: true`。
model-invoked 的 `description` 保留富 trigger 措辞("Use when …");user-invoked 的写成给人看的一行摘要。

## 写法

- 祈使句、散文优先(先讲为什么,再给规则)、浅标题。
- 正面提示优先,禁令只留作无法正面表述的硬护栏,且配上"那就做什么"。
- 完成标准写成可核对的 `Done when`。
- 事实自己查,决策交给用户。

## 增删 skill 时要同步的地方

- `README.md` 与 `README.zh-CN.md` 的 skills 表(两份都改)。
- `.claude-plugin/plugin.json` 的 `skills` 数组。
- 若日后加 router skill,它的路由图必须随之同步——路由里有它没提的 skill、或指向已删的 skill,就是个会撒谎的路由。
