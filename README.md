# Atlas Seed

**Your working rules for AI in about 15 minutes, in ChatGPT, Codex or Claude Code. Then, if you want it, a full identity layer that the same files grow into.**

> **Status: v0.2 alpha, unreleased (2026-11-10).** The short route is new. The identity schema and the full interview are the v0.1 material, reworked for three environments. Pairs with [Obsidian Seed](https://github.com/dkushnikov/obsidian-seed) when you want a vault; works without it.

---

## Start here: rules in 15 minutes, no install

1. Open a **new chat**. ChatGPT on any plan is enough. Claude, Codex and Claude Code work the same way.
2. Copy the prompt from [prompts/start.md](prompts/start.md): everything inside the code block, English or Russian. Paste it as your first message.
3. Answer three questions. You get a draft of 5–7 rules. Refine it until every rule says what the assistant *does*. Accept it.
4. Try your task under the rules. Make one correction. The assistant answers with one `rule:` line.
5. Save the two things the assistant gives you: the Markdown document (the source; keep it as a file) and the short form (paste it into the assistant's settings). Where exactly, for each environment: [environments.md](environments.md).

Afterwards you have a text that turns "I value directness" into "state a significant objection before the answer", one correction already folded in, and a place the next chat reads it from. You do not have a description of yourself, a personality profile, or a system that updates itself. The rules grow by hand: each correction is one line you add.

Fifteen minutes is the target, not a measurement. The author ran the prompt non-interactively in Codex and Claude Code on 2026-11-10 with a fictional persona ([environments.md § Verified runs](environments.md#verified-runs)); the ChatGPT product itself and a first-time user's timing are not recorded yet. If you run it, time it and open an issue with the number.

## Choose your environment

| You use | The rules live in | The next chat reads them | Guide |
|---|---|---|---|
| ChatGPT | Custom instructions (all your chats) or one Project's instructions (that project). The document stays a file you keep. | By itself, within the scope you chose | [environments.md § ChatGPT](environments.md#chatgpt) |
| Codex (CLI, IDE, app) | `working-rules.md` and `AGENTS.md` in a folder of yours | By itself when you start Codex in that folder | [environments.md § Codex](environments.md#codex) |
| Claude Code | The same folder; `CLAUDE.md` imports `AGENTS.md` | By itself when you run `claude` there | [environments.md § Claude Code](environments.md#claude-code) |
| Codex and Claude Code together | One `AGENTS.md`, one import, one folder | Both | [environments.md § one folder](environments.md#codex-and-claude-code-in-one-folder) |

Nothing moves between products by itself. When you switch products, you paste the text.

## Four things, kept apart

Atlas Seed distinguishes four things that most "AI + personal context" setups blur:

1. **Personal context** — facts, values and preferences you have confirmed. Short route: three lines (task, role, how you work). Full route: the identity files.
2. **Interaction rules** — observable behaviour you expect from the AI. `working-rules.md`. This is what the short route produces.
3. **Work state** — decisions, corrections, open questions, next step. Short route: the corrections log inside `working-rules.md`. With a vault: Obsidian Seed's `_claude/`.
4. **Environment mechanism** — where each of these is stored, what the tool reads by itself, who updates it, what the next chat sees. [environments.md](environments.md).

A guess about you is not a fact until you confirm it. You may skip any question. Rules you write do not change the priority of the platform's own instructions, do not lift the environment's limits, and give the assistant no access to other data.

## Going deeper: the identity layer

The short route gives the assistant rules. The full route gives it a model of *you*: eight markdown files with provenance frontmatter, populated in a 90–120 minute interview. Schema: [identity-schema.md](identity-schema.md). Process: [bootstrap-ritual.md](bootstrap-ritual.md).

| File | What it holds |
|------|---|
| `SOUL.md` | Constitution — stable principles that anchor who you are |
| `roles.md` | The hats you wear, their triggers, how much autonomy the AI has in each |
| `life-capitals.md` | The dimensions of life you invest in |
| `life-compass.md` | Values and the principles you navigate by |
| `me-summary.md` | One-page self-portrait, the file that loads first |
| `psychometrics-summary.md` | Optional: formal assessments, compressed |
| `working-style.md` | How you work with AI: the long form of `working-rules.md` after a month of use |
| `complementarity.md` | Where you and the AI complement each other |

How the two routes relate: the identity files **describe the person**; the working rules **prescribe the AI's behaviour**. The rules are justified by the description, but the AI acts on the rules. `working-rules.md` is the seed of `working-style.md`. Running the full route later does not replace it; it reads the approved rules first and proposes changes.

The full route needs a place for files (a folder you open with Codex or Claude Code, or files you save by hand from a ChatGPT chat) and an evening. Git is recommended for folders and not required. Nothing in it installs the author's own setup; there is no ingest script and no integration in this repository.

## With or without Obsidian Seed

Atlas Seed is about who you are and how you want the AI to behave. It is not a place for notes, decisions and a journal. When you want those, use [Obsidian Seed](https://github.com/dkushnikov/obsidian-seed): it builds a personal vault with the same four-way split and the same `AGENTS.md` + `CLAUDE.md` convention, so the rules you wrote here go into the vault unchanged.

Order does not matter. Rules first, vault later, or the other way round.

## Limits

- **Instructions, not enforcement.** A rule in a file is context for the model. It can be missed. When it is, say so and sharpen the wording.
- **No automatic loading from a link.** Pasting this repository's URL into a chat does not make the chat read it. The prompt is self-contained for that reason.
- **No sync between products.** Custom instructions, `AGENTS.md`, `CLAUDE.md` and each product's memory are separate stores. You carry the text.
- **Your text goes to the provider.** What you write into the rules and the identity files is sent to OpenAI or Anthropic like any other message. Write accordingly.
- **Not the author's Atlas.** The author's setup has hooks, pipelines and integrations. None of that is in this repository; the seed is Markdown and a few prompts.

## Files in this repository

| File | Role |
|---|---|
| [prompts/start.md](prompts/start.md) | The copyable start prompt (English and Russian) |
| [prompts/continue.md](prompts/continue.md) | Prompts for the next chat, for updates, for re-running |
| [templates/working-rules.md](templates/working-rules.md) | The Markdown source with its derived short form and corrections log |
| [templates/AGENTS.md](templates/AGENTS.md), [templates/CLAUDE.md](templates/CLAUDE.md) | Instruction files for a folder you open with Codex or Claude Code |
| [environments.md](environments.md) | What each environment reads, saves and does not do |
| [bootstrap-ritual.md](bootstrap-ritual.md) | Short route, full interview, re-running, iterate from use |
| [identity-schema.md](identity-schema.md) | The eight identity files |
| [walk-up-chain.md](walk-up-chain.md) | How context reaches a session; the contract any environment must meet |
| [knowledge-metabolism-interface.md](knowledge-metabolism-interface.md) | What a knowledge tool may read from the identity layer |
| `AGENTS.md`, `CLAUDE.md` | Instructions for an agent started inside this checkout: personal files do not belong here |

## Current state (2026-11-10)

- **Short route:** prompt, templates and environment guide written; runs with a fictional persona in Codex CLI 0.166.0 and Claude Code 2.1.319 recorded in [environments.md](environments.md#verified-runs), including a hand edit of the rules picked up by both tools; the ChatGPT product path described from the help center, not run there, not yet timed by a first-time user.
- **Identity schema:** eight files, in use by the author since 2026-03.
- **Full interview:** documented; tested by the author only.
- **Loading mechanism:** documented per environment; hierarchical loading is optional, not a requirement.
- **Knowledge Metabolism interface:** a contract, not a library. [Mnemon](https://github.com/dkushnikov/mnemon) is a compatible consumer.

Expect schema changes between v0.2 and v0.3. Open an issue when something is missing, wrong or surprising.

## Relationship to other projects

- **[Obsidian Seed](https://github.com/dkushnikov/obsidian-seed)** — the vault: notes, decisions, journal, continuity. Atlas Seed sits beside it.
- **[Mnemon](https://github.com/dkushnikov/mnemon)** — a knowledge library with an AI reader. Can read the identity layer through the interface contract.
- **[Nestor](https://github.com/dkushnikov/nestor-plugin)** — multi-model deliberation plugin. Not integrated.
- **[claude-environment](https://github.com/dkushnikov/claude-environment)** — infrastructure for a multi-machine Claude Code setup. Orthogonal.

## Philosophy, in short

Most attempts at "AI + personal context" confuse three things: your *notes* (content), your *tools* (plumbing) and your *self* (identity). They feed the AI notes and expect it to learn who you are. It works slowly, partially, inconsistently.

Atlas Seed does the opposite: make the rules explicit first, in a form the AI reads at the start of a chat, and let them grow from corrections. Then, when the rules stop being enough, make yourself explicit too. Eight small files. The substrate is replaceable; the files are yours.

## Contributing

The most useful contribution is running it and reporting what happened: where it broke, what was missing, how long it took. Open an issue. Pull requests on prompts, templates, documentation and the environment guide are welcome; the schema is still settling.

## License

MIT

## Credits

Born out of Obsidian Seed and the broader Atlas project. Inspired by, and different from, [personal-context](https://github.com/amr05008/personal-context) (portraits versus working identities). Converged with [Karpathy's Raw → Wiki → Frontend pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) on the architecture of personal AI systems.
