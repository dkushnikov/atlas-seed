# Atlas Seed — instructions for an agent started in this checkout

This is the public template repository of Atlas Seed. It holds the method, the prompts and the templates. It holds nobody's personal files.

- If the user asks to run the ritual, write their rules or set up their identity: do it in a folder the user names (for example `~/ai/`), not here. Ask for the folder first. Never write personal content into this checkout.
- Never write into global files (`~/.codex/AGENTS.md`, `~/.claude/CLAUDE.md`, custom instructions) unless the user asks for that explicitly; folder-scoped rules are the default.
- The conversation to run is `prompts/start.md` (short route) or `bootstrap-ritual.md` (full route). Files for the user's folder come from `templates/`.
- Repository work (editing these docs): one process per document; environment-specific text lives in `environments.md`; do not fork the prompt or the ritual per environment.
