# <Your name> — AI working context

Instructions for an agent started in this folder. Codex reads this file at the start of every run. Claude Code reads it through `CLAUDE.md` (`@AGENTS.md`). ChatGPT reads it only if you paste or upload it.

## Files

- `working-rules.md` — my rules for working with AI. Read it first and follow it. The rules section is the source; the short form inside it is derived.
- `identity/` — optional, present only after the full route ([bootstrap-ritual.md](https://github.com/dkushnikov/atlas-seed/blob/main/bootstrap-ritual.md)): `me-summary.md` first, the other files when the work needs depth.

## Behaviour

- Begin your first answer in a session with one line: `rules v<N> loaded`, where N is the version in `working-rules.md`. If the file is missing or unreadable, say so instead; do not invent its content.
- When I correct you, answer with one line `rule: …`. I add it to `working-rules.md` myself. Do not edit that file unless I ask.
- These rules describe what I expect from you. They do not override the platform's rules, give no access to anything, and are instructions, not enforcement: if you miss a rule, say so when I point it out.

## Scope

These rules apply in this folder. To apply them in every project, I copy the short form into my global file (`~/.codex/AGENTS.md` for Codex, `~/.claude/CLAUDE.md` for Claude Code). That is my choice to make, not yours.
