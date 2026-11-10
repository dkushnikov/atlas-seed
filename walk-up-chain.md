# Walk-Up Chain — how context reaches a session

**What each environment loads by itself, what it loads when asked, and what nothing loads. The contract Atlas Seed expects from any environment.**

> **Audience:** people who want to understand exactly how the rules and identity files get into a session, or who want to host Atlas Seed in an environment not covered here. The practical page is [environments.md](environments.md). The short route in ChatGPT does not need anything on this page.

---

## The term

**Walk-up chain** is Claude Code's loading pattern: at launch it reads `CLAUDE.md` from the working directory and from every directory above it, then the user-level `~/.claude/CLAUDE.md`, and concatenates them, closest file last. Codex does the mirror image: it reads `~/.codex/AGENTS.md`, then walks *down* from the project root to the working directory, one `AGENTS.md` per directory, up to 32 KiB. ChatGPT has no directories; it has custom instructions, a Project's instructions and the Project's files.

The pattern gives one thing: a file placed at a higher level reaches every session below it without being copied. Atlas Seed uses that when it is there and does without it when it is not.

## What loads, by level

| Level | ChatGPT | Codex | Claude Code |
|---|---|---|---|
| Global (every chat) | Custom instructions | `~/.codex/AGENTS.md` | `~/.claude/CLAUDE.md`, `~/.claude/rules/` |
| Scope (one project or folder) | A Project's instructions and files | `AGENTS.md` from the project root down to the working directory | `CLAUDE.md` from the working directory upward, `.claude/rules/`, `@imports` |
| On demand | Text you paste, files you upload | Files the agent opens when the instructions or you name them | Files the agent reads when the instructions or you name them |
| Never by itself | Your disk, a link's content, another product's store | Custom instructions, `CLAUDE.md`, Claude's memory | `~/.codex/AGENTS.md`, Codex memories, custom instructions |

Sources, checked 2026-11-10: [Codex AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md), [Claude Code memory](https://code.claude.com/docs/en/memory), [ChatGPT custom instructions](https://help.openai.com/en/articles/8096356-chatgpt-custom-instructions), [ChatGPT Projects](https://help.openai.com/en/articles/10169521-projects-in-chatgpt).

## The loading contract

What Atlas Seed can rely on, and what it cannot:

- **The instruction file loads at the start.** `AGENTS.md` in Codex, `CLAUDE.md` with its `@imports` in Claude Code, custom instructions in ChatGPT. This is mechanical.
- **Files the instruction file names load when the agent opens them.** "Read `working-rules.md` first" is honoured by the model, not by the tool. It is reliable in practice and not guaranteed. In Claude Code an `@working-rules.md` import is mechanical; in Codex there is no import, so the pointer is the mechanism.
- **A marker makes loading observable.** The template `AGENTS.md` asks for one line at the start of the first answer, `rules vN loaded`. No line, no load.
- **Nothing is loaded in full by default except what you put at the global or scope level.** The identity files are referenced, not inlined: `me-summary.md` is the one worth naming at the top; the rest the agent reads when the work needs depth. This keeps the start of a session cheap.
- **A link loads nothing.** A URL in a chat is text.

In the author's own setup the user-level file says, in effect, *"identity files are in `core/identity/`; load on demand when the work requires depth"*. That is a pointer, not an inline, and it is why the author's sessions start small.

## Closer scopes and contradictions

There is no priority mechanism in Markdown. When a project file says "do not challenge me" and the rules say "state a significant objection first", the model picks one, and not always the same one. Keep the two consistent, and when a project needs an exception, write the exception into the project file explicitly ("in this folder, objections after the answer, not before"). A rule that depends on being "higher" than another file is a rule that will fail.

## Privacy boundaries

The identity files are about you. Where they are readable is a decision with two layers:

1. **Policy**, which you write: which folders or projects get the rules, which get the identity files, which get nothing. A Markdown line stating the policy makes the agent aware of it and does not enforce it.
2. **Mechanism**, which the tool provides: Codex permission profiles and sandboxes, Claude Code permission rules (`permissions.deny` on paths, the `--add-dir` boundary), separate folders, separate ChatGPT Projects with project-only memory. These are enforced by the tool, and only to the extent the tool documents.

Atlas Seed asks for a policy and names the mechanisms. It does not provide a guarantee that identity never leaks into a private context, and no Markdown instruction can. The author's own private vault is isolated by tool permissions and by not being a source folder for any agent, not by a line in a file.

What this means for a knowledge tool reading the identity layer: it reads what the environment lets it read ([knowledge-metabolism-interface.md](knowledge-metabolism-interface.md) § A5).

## Requirements for an environment

Any environment that hosts Atlas Seed needs the following. The short route needs only R1 and R2.

### R1: A stable place for files

A folder, a note store, a Project. The path should survive sessions and tool updates. Cloud sync and Git are preferences, not requirements.

### R2: An instruction surface the tool reads at the start

Custom instructions, `AGENTS.md`, `CLAUDE.md`. If the environment has none, the user pastes the document at the start of every chat; the method still works, with more friction.

### R3: On-demand reading of files

The agent can open a file the instructions name. Codex and Claude Code have this. ChatGPT has it for uploaded files within a chat or a Project.

### R4: A carrier for work state

Somewhere the decisions, corrections and the next step survive between sessions: the corrections log in `working-rules.md`, or Obsidian Seed's `_claude/` files in a vault. A product's own memory (ChatGPT memory, Codex memories, Claude Code auto memory) is a supplement: you cannot read it as a file, and it does not move between products.

### R5: Frontmatter tolerance

The identity files carry YAML frontmatter for provenance. The environment does not need to parse it; the model needs to read past it. Every current environment does.

### Optional: hierarchical loading

Needed only for the global-plus-scope split (rules in every project without copying). Codex and Claude Code have it. ChatGPT has a two-level version: custom instructions plus a Project's instructions, where the project's instructions override the global ones.

### Explicitly not required

A vault, a graph view, mobile access, cloud sync, version control, real-time editing.

## Portability

The identity files and the working rules are flat Markdown with YAML frontmatter. They move between environments unchanged. What does not move: the instruction surface (custom instructions, `AGENTS.md` content specific to a tool), each product's memory, session logs. When you change products, copy the files and rewrite the pointer; nothing else carries over.

## Hosting Atlas Seed somewhere new

1. Check R1–R5. Note which are missing and what the workaround is.
2. Name the instruction surface and what it loads at the start.
3. Choose the stable path for the files and write it into the instruction surface.
4. Put the `rules vN loaded` marker in and check it appears.
5. Test the boundary you care about: start a session where the rules should not apply and confirm the marker is absent.
6. Write the result up as a section of [environments.md](environments.md) and open a pull request.

## Future work

- A small check that an environment actually loads the rules (the marker line, automated).
- Migration notes between environments with a validation step.
- Multi-machine loading, when the files live on more than one computer. Tracked in the author's Distributed Atlas project, not here.
