# Changelog

## v0.2.0-alpha (unreleased, draft 2026-11-10)

Adaptation for ChatGPT and Codex, keeping Claude Code. Prepared for review; not released.

### Added
- **Short route** — `prompts/start.md`: a self-contained start prompt (English and Russian) that produces 5–7 working rules, one correction and two artifacts (Markdown source, short form) in about 15 minutes, in ChatGPT without any install. `prompts/continue.md` for the next chat, updates and re-running.
- **Templates** — `templates/working-rules.md` (source + derived short form + corrections log), `templates/AGENTS.md` and `templates/CLAUDE.md` for a folder opened with Codex or Claude Code (one file, one import, marker line `rules vN loaded`).
- **`environments.md`** — what ChatGPT, Codex and Claude Code read by themselves, where rules are saved, how the next chat reconnects, what each product does not do; verified runs table.
- Root `AGENTS.md` / `CLAUDE.md` for an agent started inside the checkout: personal files do not belong here.

### Changed
- **README** — starts with the short route; environment choice; the four-way split (personal context · interaction rules · work state · environment mechanism); honest limits; dangling `PHILOSOPHY.md` references removed.
- **bootstrap-ritual.md** — two routes (short, full), prerequisites per route, Git optional, re-running rules (approved files first, diffs not competing drafts, no global changes without choice), ingest marked as manual and unshipped.
- **walk-up-chain.md** — loading described per environment; hierarchical loading optional; "identity wins over project files" and isolation guarantees replaced by what Markdown does and does not do; requirements R1–R5 with the short route needing only R1–R2.
- **identity-schema.md** — which files describe the person and which prescribe behaviour; what loads automatically (nothing by itself); `working-rules.md` as the seed of `working-style.md`.
- **knowledge-metabolism-interface.md** — paths resolved from the instruction file; A5 restated as policy plus whatever mechanism the environment provides, not a guarantee; KM consumers are an extension of the folder case.

## v0.1.0-alpha (2026-04-12)

Initial alpha release. Concept-level — read to understand the idea; implementation is minimal.

### What's included

- **README.md** — positioning, 5-component overview, three usage paths (with/without/considering Obsidian Seed), substrate-agnostic framing
- **identity-schema.md** — detailed schema for 8 identity files (Soul, roles, life-capitals, life-compass, me-summary, psychometrics-summary, working-style, complementarity) with frontmatter conventions, stability levels, inter-file relationships
- **bootstrap-ritual.md** — three-part process: structured interview (90-120 min), optional ingest from existing writing, iterate-from-use protocol (ongoing)
- **walk-up-chain.md** — hierarchical configuration loading spec with 7 substrate requirements (R1-R7) defining what any hosting environment must provide
- **knowledge-metabolism-interface.md** — contract between identity layer and Knowledge Metabolism implementations (e.g., Mnemon), defining what KM systems can assume and consume

### What alpha means

The schema and walk-up chain are proven in the author's setup (~6 weeks of daily use). The bootstrap ritual needs external testing. The ingest script is conceptual (not yet executable). The Knowledge Metabolism interface is a contract, not a library.

Expect breaking schema changes between v0.1 and v0.2. If you're looking for stability, wait for v0.3+.

### Related

- [Obsidian Seed](https://github.com/dkushnikov/obsidian-seed) — substrate layer (vault methodology)
- [Mnemon](https://github.com/dkushnikov/mnemon) — one Knowledge Metabolism implementation
- [Nestor](https://github.com/dkushnikov/nestor-plugin) — multi-model deliberation plugin
