# Unknown Unknowns（未知的未知）

> 三个词：开工 **kickoff**，收工 **wrapup**，不放心 **quiz-me**。剩下的都是 Agent 的事。

最需要发现盲区的人，恰恰不知道自己有盲区——所以这套工具不要求你学会一套分类法、
记住九种技巧。你只需要说出自己能真切感知的时刻，Agent 来挑技巧。

同时支持 **Claude Code**、**OpenAI Codex CLI**，以及任何兼容开放
[Agent Skills](https://agentskills.io) 规范的工具（Cursor、Amp 等）。灵感来自
Claude Code 团队 [Thariq (@trq212)](https://x.com/trq212) 的文章
[*A Field Guide to Fable: Finding Your Unknowns*](https://x.com/trq212/article/2073100352921215386)。

[English README](./README.md)

## 三个命令

| 时刻 | 命令 | Agent 做什么 |
|---|---|---|
| 要开始干活了 | `kickoff` | 先诊断你的 unknowns，然后只跑需要的技巧：不熟的领域先做盲区简报；"看到才知道要什么"就出几个一次性原型让你挑；有悬而未决的决策就一次一个问题地访谈你；有参考实现就提炼语义清单——最后落成一份 5 分钟能审完的"最可能改的放最前"的计划 |
| 活干完了 | `wrapup` | 把成果打包成 demo 开头的 buy-in 文档；就真实发生的改动（包括 diff 看不到的既有代码路径）出题考你，全对才建议合并；最后把这轮学到的沉淀进永久上下文 |
| 不确定自己看懂了 | `quiz-me` | 单独的测验：讲解、出题、严格打分，明确给出 PASS / NOT YET |

原文的九种技巧——盲区扫描、头脑风暴与原型、访谈、参考实现、unknowns 优先的计划、
实现笔记、提案文档、测验——全都还在，它们作为 Agent 的内部工具箱放在每个 skill 的
`references/` 里。你永远不需要叫出它们的名字。

```
kickoff ──→ 计划 ──→ 实现（新会话，自动记笔记）──→ wrapup
   ↑                                                  │
   └────────── 这轮学到的，就是下一轮的地图 ──────────┘
```

## 安装

### Claude Code（插件市场）

```
/plugin marketplace add lusipad/Unknown-unknowns
/plugin install unknown-unknowns@unknown-unknowns
```

### OpenAI Codex CLI

```sh
git clone https://github.com/lusipad/Unknown-unknowns.git
cd Unknown-unknowns
./install.sh --codex        # 复制到 $CODEX_HOME/skills（默认 ~/.codex/skills）
```

Windows（PowerShell）：`.\install.ps1 -Codex`

### 通用安装器（Claude Code + Codex + Cursor 等）

```sh
npx skills add lusipad/Unknown-unknowns
```

### 可选：三条常驻规则

有两件事用户永远想不起来主动触发：干活途中记实现笔记，以及合并前跑 wrapup。
可以按项目选择性注入：

```sh
./install.sh --rules /path/to/your/project     # 或 .\install.ps1 -Rules D:\your\project
```

这会往项目的 `CLAUDE.md` / `AGENTS.md` 追加三行（幂等，重复运行安全）：执行计划时
保守处理偏差并记录；用户说"上次干的活是错的"时建议 kickoff；合并未审查的大改动前
建议 wrapup。详见 [rules/unknowns-rules.md](./rules/unknowns-rules.md)。

## 什么时候触发

显式触发：Claude Code 里 `/kickoff`、`/wrapup`、`/quiz-me`；Codex 里直接点名。
自动触发——当你说出这类话时：

- "这块代码我从来没碰过" → kickoff（盲区简报）
- "给我看几个方向，我看到才知道要什么" → kickoff（原型）
- "上次让 AI 干的活回来是错的，不知道为什么" → kickoff（诊断）
- "干完了，打包一下给人看" → wrapup
- "我不太确定自己看懂了这次改动" → quiz-me

中文触发词（开工 / 收工 / 考考我）已经写进 skill 的 description 里。

## 设计说明

- **按时刻划分，不按分类法划分。** 人人都能感知"要开始了"和"干完了"，但没人能察觉
  "我现在有 unknown knowns"。命令对应前者，后者交给 Agent。
- **渐进式披露。** 3 个入口，9 种技巧作为内部参考文档按需加载——不用时不占上下文。
- **天生可移植。** Frontmatter 只用 `name` + `description`，正文不含任何特定 Agent
  的工具名。
- **多语言。** 指令正文保持英文（模型遵循度最高），但每个 skill 都明确要求：面向
  用户的输出必须使用用户正在说的语言。任何语言都能通过语义匹配触发；中文触发词
  已内置。
- **kickoff 是诊断，不是仪式。** 任务本身没有值得挖的 unknowns 时，它会直说
  "直接实现吧"，然后让开。

## 许可

MIT——见 [LICENSE](./LICENSE)。理念归功于
[Thariq 的原文](https://x.com/trq212/article/2073100352921215386)。
