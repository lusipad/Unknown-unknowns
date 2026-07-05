# Unknown Unknowns

> Three words: **kickoff** when you start, **wrapup** when you finish, **quiz-me** when
> you're not sure. Everything else is the agent's job.

The person who most needs help finding their blind spots is, by definition, the person
who doesn't know they have them. So this toolkit doesn't ask you to learn a taxonomy or
remember nine techniques — you invoke moments you already feel, and the agent picks the
technique.

Works with **Claude Code**, **OpenAI Codex CLI**, and any agent supporting the open
[Agent Skills](https://agentskills.io) format (Cursor, Amp, …). Based on
[*A Field Guide to Fable: Finding Your Unknowns*](https://x.com/trq212/article/2073100352921215386)
by [Thariq (@trq212)](https://x.com/trq212).

[中文说明 / Chinese README](./README.zh-CN.md)

## Three commands

| Moment | Command | What the agent does |
|---|---|---|
| About to start something | `kickoff` | Diagnoses your unknowns, then runs only what's needed: a blind spot briefing for unfamiliar territory, throwaway prototypes when you'll "know it when you see it", a one-question-at-a-time interview for open decisions, semantics extraction from a reference — landing on an unknowns-first plan you can review in five minutes |
| Just finished | `wrapup` | Packages the work into a buy-in doc that leads with the demo, quizzes you on what actually changed (including the code paths diffs don't show), and only recommends merging when you pass — then banks the session's learnings into permanent context |
| Not sure you understand a change | `quiz-me` | The quiz alone: explain, test, grade strictly, explicit PASS / NOT YET verdict |

The nine techniques from the article — blind spot pass, brainstorms & prototypes,
interviews, references, unknowns-first plans, implementation notes, pitches, quizzes —
all still exist. They live in `references/` inside each skill as the agent's internal
toolbox. You never have to name them.

```
kickoff ──→ plan ──→ implement (fresh session, notes kept) ──→ wrapup
   ↑                                                              │
   └────────────── what you learn becomes the map ────────────────┘
```

## Install

### Claude Code (plugin marketplace)

```
/plugin marketplace add lusipad/Unknown-unknowns
/plugin install unknown-unknowns@unknown-unknowns
```

### OpenAI Codex CLI

```sh
git clone https://github.com/lusipad/Unknown-unknowns.git
cd Unknown-unknowns
./install.sh --codex        # copies skills to $CODEX_HOME/skills (default ~/.codex/skills)
```

Windows (PowerShell): `.\install.ps1 -Codex`

### Universal installer (Claude Code + Codex + Cursor + more)

```sh
npx skills add lusipad/Unknown-unknowns
```

### Optional: three always-on rules

Two things users never remember to trigger: keeping implementation notes mid-task, and
running wrapup before merging. Opt in per project:

```sh
./install.sh --rules /path/to/your/project     # or: .\install.ps1 -Rules D:\your\project
```

This appends three lines to the project's `CLAUDE.md` / `AGENTS.md` (idempotent — safe
to re-run): log deviations conservatively during plans, suggest `kickoff` when a
previous attempt came back wrong, suggest `wrapup` before merging unreviewed changes.
See [rules/unknowns-rules.md](./rules/unknowns-rules.md).

## When they trigger

Explicitly: `/kickoff`, `/wrapup`, `/quiz-me` in Claude Code, or just name them in
Codex. Automatically, when you say things like:

- "I've never touched this part of the codebase" → kickoff (blind spot briefing)
- "Show me a few directions, I'll know it when I see it" → kickoff (prototypes)
- "The last attempt came back wrong and I don't know why" → kickoff (diagnosis)
- "Done, package this up for review" → wrapup
- "I'm not confident I understand what changed" → quiz-me

Chinese trigger words (开工 / 收工 / 考考我) are built into the skill descriptions.

## Design notes

- **Moments, not taxonomy.** Users reliably feel "starting" and "finishing"; they don't
  reliably notice "I have unknown knowns." Commands map to the former; the agent handles
  the latter.
- **Progressive disclosure.** Three entry points; nine techniques as internal reference
  files the agent reads on demand — cheap on context until needed.
- **Portable by construction.** Frontmatter uses only `name` + `description`; bodies are
  plain instructions with no agent-specific tool names.
- **Multilingual.** Instructions stay in English (best model adherence), but every skill
  requires user-facing output in the language the user is speaking. Triggering works in
  any language via semantic matching; 中文 trigger words are built in.
- **Kickoff is a diagnosis, not a ceremony.** If a task has no meaningful unknowns, it
  says "just implement" and gets out of the way.

## License

MIT — see [LICENSE](./LICENSE). Concepts credit
[Thariq's field guide](https://x.com/trq212/article/2073100352921215386).
