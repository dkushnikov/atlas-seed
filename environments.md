# Environments — how your rules reach a session

Atlas Seed keeps four things apart. This page is about the fourth.

1. **Personal context** — facts, values and preferences you confirmed (`identity/`, or the three context lines of the short route).
2. **Interaction rules** — observable behaviour you expect from the AI (`working-rules.md`).
3. **Work state** — decisions, corrections, open questions, next step (the corrections log; in a vault, Obsidian Seed's `_claude/`).
4. **Environment mechanism** — where each of these is stored, what the tool reads by itself, who updates it, and what the next chat sees.

Nothing below promises that a rule is always followed. Instruction files are context for the model, not enforcement. Nothing carries rules from one product to another by itself: you move the text.

## What each environment reads

| | ChatGPT (web, desktop, mobile) | Codex (CLI, IDE, app) | Claude Code (terminal) |
|---|---|---|---|
| Read by itself at the start of a chat | Custom instructions; a Project's instructions and files, inside that Project | `~/.codex/AGENTS.md`, then `AGENTS.md` from the project root down to the working directory, 32 KiB in total by default | `~/.claude/CLAUDE.md`, every `CLAUDE.md` from the working directory upward, `.claude/rules/`, files they import with `@path` |
| Read when you ask | Text you paste; files you upload | Any file in the folder you name | Any file you name; outside the folder it asks first |
| Its own memory | ChatGPT memory (Settings → Personalization) | Codex memories, local, off by default | Auto memory in `~/.claude/projects/<project>/memory/` |
| Does not read | Your disk, Git, GitHub, a link you paste | Custom instructions, `CLAUDE.md`, `.claude/rules/`, Claude's memory (unless you configure a fallback) | `~/.codex/AGENTS.md`, Codex memories, custom instructions |

Sources checked 2026-11-10: [ChatGPT custom instructions](https://help.openai.com/en/articles/8096356-chatgpt-custom-instructions), [Codex: Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md), [Codex: Memories](https://learn.chatgpt.com/docs/customization/memories), [Claude Code: How Claude remembers your project](https://code.claude.com/docs/en/memory).

## ChatGPT

**Save.** The Markdown document is yours to keep: a note in Obsidian, Apple Notes, a private Gist, a file in a folder. ChatGPT does not keep files for you outside Projects.

**Connect in the next chat.** Three ways; pick by scope.

- *All chats:* Settings → Personalization → Custom instructions, with "Enable customization" on. Paste the short form. It applies immediately to all chats, including existing ones. Limit: 1,500 characters on Free and Go, 5,000 on Plus, Pro, Business, Enterprise and Education (help center, 2026-11-10). The template keeps the short form under 1,500 so it fits every plan.
- *One project:* create a Project, paste the short form into the project's instructions, upload the document as a project file. The rules apply only to chats inside that Project. Use this when the rules are for one piece of work, so they do not leak into every chat.
- *This chat only:* paste the document at the start of the chat ([prompts/continue.md](prompts/continue.md)). Works in a Temporary chat too.

**Update.** Edit the source document, raise the version, ask the assistant to regenerate the short form ([prompts/continue.md](prompts/continue.md)), paste it over the old one. The "(rules vN)" tail in the field shows which version is live.

**Memory.** ChatGPT may remember things you said. Treat it as a supplement: it can forget, and you cannot read it as a file. Custom instructions are the carrier you control.

**Verified here:** not run in the ChatGPT product by the author (the only account at hand was a personal one; a run there would have mixed in its own memory and settings). The help-center facts above were checked on 2026-11-10; the prompt itself was run in Codex and Claude Code, see the table at the end. The 15-minute run in ChatGPT is the one check left for a first-time user.

## Codex

**Save.** In a folder of yours, for example `~/ai/`: `working-rules.md` and `AGENTS.md` from [templates/](templates/). `identity/` appears after the full route. Codex writes the files when you ask it in that folder; the default permission mode asks before anything outside the folder.

**Connect in the next chat.** Start Codex in that folder (`codex` from the folder, or open the folder in the app). It reads `AGENTS.md` at the start of every run and the file tells it to read `working-rules.md`. The first line of the answer should be `rules vN loaded`; if it is not, the file was not read.

For another project: add one line to that project's `AGENTS.md` (`Read ~/ai/working-rules.md before starting and follow it`). For every project: paste the short form into `~/.codex/AGENTS.md`. The second is your choice, not a default.

**Update.** Edit `working-rules.md`; the next run reads it. If you also keep a copy in `~/.codex/AGENTS.md`, regenerate and paste.

**Memory.** Codex memories are off by default, local, and generated from past chats. A supplement; the file wins when they disagree.

**Does not.** Codex does not read `CLAUDE.md` or `.claude/rules/` unless you add `project_doc_fallback_filenames = ["CLAUDE.md"]` to your `~/.codex/config.toml`. It does not read Claude's memory or ChatGPT custom instructions. Codex in the browser (cloud tasks) runs in its own container and is not covered here.

**Verified here:** Codex CLI 0.166.0 on macOS, see the table at the end. The desktop app and the IDE extension read the same `AGENTS.md`; they were not exercised by the author.

## Claude Code

**Save.** Same folder, same files. `CLAUDE.md` holds one line, `@AGENTS.md`, so Claude Code and Codex read one file. Claude Code also reads an `AGENTS.md` on its own when there is no `CLAUDE.md` in the folder or above it (v2.1.277+); the import makes that unconditional.

**Connect in the next chat.** Run `claude` in the folder. `CLAUDE.md` and its import load at launch; `/context all` lists them under Memory files. The first line of the answer should be `rules vN loaded`.

For another project: `@~/ai/working-rules.md` in that project's `CLAUDE.md`. For every project: the same import in `~/.claude/CLAUDE.md`. Your choice.

**Update.** Edit `working-rules.md`; the next session reads it.

**Memory.** Auto memory lives outside your folder, under `~/.claude/projects/`. A supplement; copy anything that matters into your files.

**Does not.** Claude Code does not read `~/.codex/AGENTS.md`, Codex memories or ChatGPT settings.

**Verified here:** Claude Code 2.1.319 on macOS, see the table at the end.

## Codex and Claude Code in one folder

One `AGENTS.md` with the content, one `CLAUDE.md` with `@AGENTS.md`. Never two copies of the rules.

If the folder already has a `CLAUDE.md` with content, do not overwrite it. Two honest options:

1. Move the content into `AGENTS.md` and leave `@AGENTS.md` in `CLAUDE.md`. Ask the agent to show the diff before it writes.
2. Keep `CLAUDE.md` as is and tell Codex to read it: `project_doc_fallback_filenames = ["CLAUDE.md"]` in `~/.codex/config.toml`. This is your global Codex config; edit it by hand.

If the folder already has an `AGENTS.md`, add the pointer to `working-rules.md` to it; do not replace it.

## Not covered

- ChatGPT desktop app with access to a local folder ("local projects" in the Codex docs). Not tested by the author; if you use it, the Codex section is the closest description, but check what the app reads.
- Automatic migration of an existing setup. If you have personal files in `~/.claude/` or `~/.codex/` already, read [bootstrap-ritual.md](bootstrap-ritual.md) § Re-running and let the agent show a plan before it changes anything.

## Verified runs

The author's runs on 2026-11-10, macOS, with a fictional persona ("a product manager, decision memo on dropping a free trial") in a throw-away folder, non-interactive: the persona's answers to the three questions, the acceptance and the one correction were given up front in the same message. "Verified" means the run produced the named artifact and the named behaviour; it does not mean every rule is always followed, and it is not a first-time user's timing.

| Environment | Version | What ran | Observed |
|---|---|---|---|
| Codex CLI | 0.166.0 | Start prompt in a folder holding the template `AGENTS.md` + `CLAUDE.md` | 63 s. Six rules drafted, the correction folded into rule 4 as a `rule:` line, `working-rules.md` written with frontmatter v1, short form 889 characters ending "(rules v1)". `AGENTS.md`/`CLAUDE.md` untouched. |
| Codex CLI | 0.166.0 | New run, same folder, `[energy 2/5]` task | 19 s. Followed rule 4 (recommendation plus one next action, nothing else). The `rules v1 loaded` marker line was **not** printed in this run. |
| Claude Code | 2.1.319 | New session, same folder (`CLAUDE.md` → `@AGENTS.md`), same task | 27 s. `rules v1 loaded` printed; answer ended with "For approval:"; longer than rule 4 asks for. |
| hand edit | — | Version raised to 2 and a seventh rule added in `working-rules.md` by hand, no chat | — |
| Codex CLI | 0.166.0 | New run, `[in a hurry]` question | 11 s. `rules v2 loaded`; three lines; one objection; "For approval:". |
| Claude Code | 2.1.319 | New session, same question | 41 s. `rules v2 loaded`; three lines; one objection; "For approval:". |
| ChatGPT | — | not run in the product by the author | The help-center facts above are checked; the 15-minute run in ChatGPT itself is still yours to time. |

Two readings of this table. The files are the carrier: both tools picked up the hand-edited v2 without any chat about it, which is the whole point of keeping the source as a file. And the rules are context, not enforcement: one run skipped the marker line, one answered at more length than the state tag asked. When that happens, sharpen the wording, do not conclude the method failed.

Global files on the test machine (`~/.codex/AGENTS.md`, `~/.codex/config.toml`, `~/.claude/settings.json`, the user `CLAUDE.md`) were hashed before and after the runs and did not change. The public checkout of this repository stayed clean. One caveat on fidelity: the machine's own global `~/.codex/AGENTS.md` was in Codex's context during these runs (Codex always reads it), so a first-time user's Codex sees slightly less than these runs did.
