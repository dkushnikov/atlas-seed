# Changelog

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
