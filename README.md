# Atlas Seed

**An identity layer for personal AI. Not a vault, not a tool, not a methodology — a schema for making yourself explicit to the AI you work with, plus a ritual for doing it without starting from a blank page.**

> **Status: v0.1 alpha.** Concept-level. Read to understand the idea; implementation is minimal. Pairs with [Obsidian Seed](https://github.com/dkushnikov/obsidian-seed) (substrate) but works with any substrate that supports CLAUDE.md and persistent memory.

---

## What this is

Atlas Seed is a small collection of files and a process for populating them. The files describe **who you are** in a form that an AI partner can read and reason about — not your notes, not your data, but your identity: values, roles, strengths, working style, compass, complementarity with the AI.

The process is a structured interview + optional ingest from existing writing, with an iterate-from-use protocol for refinement. The output is a set of markdown files with frontmatter, living in `core/identity/` in your environment, loaded automatically by your AI through a walk-up chain pattern.

This is the *identity layer*. It's distinct from:

- **Your vault or notes** — those are content. Identity is frame.
- **Tool configuration** — that's plumbing. Identity is what the plumbing serves.
- **AI memory** — that's runtime state. Identity is the stable substrate memory sits on.
- **Personality templates** — those are fictional. Identity is yours, evolved through use.

If you've used Obsidian Seed to build a vault, Atlas Seed is the layer that sits on top of your vault and gives the AI an explicit model of *you*. If you haven't used Obsidian Seed, Atlas Seed still works — you just need any environment that supports CLAUDE.md and persistent memory.

## What this is NOT

- **Not a productivity system.** No habit trackers, no goal frameworks, no task managers. Those are tools you can build inside your substrate; Atlas Seed doesn't touch them.
- **Not a therapy exercise.** The interview asks about who you are, but it's oriented at making you legible to an AI partner, not at self-discovery for its own sake. Self-discovery may happen as a side effect. That's fine. It's not the goal.
- **Not a replacement for your substrate.** You still need a place where your notes, decisions, and session logs live. That's what substrates (Obsidian Seed, other) are for. Atlas Seed is additive.
- **Not a fork of personal-context or other similar projects.** Those are portraits — static snapshots for giving LLMs a voice. Atlas Seed is a working identity — live, evolving, memory-integrated, partner-oriented. Different genres.
- **Not finished.** v0.1 alpha is a concept-level release. Expect breaking changes. Expect gaps. Open an issue if something is missing or wrong.

## The five components of v0.1 alpha

Atlas Seed alpha has five concrete components. Each is a document or a small collection of files. Together they define the identity layer and how to populate it.

### 1. Identity schema (8 files)

Eight markdown files with frontmatter, each covering one dimension of identity:

| File | What it holds |
|------|---|
| `SOUL.md` | Constitution — stable principles that anchor who you are (≤1 page, 5-8 items) |
| `roles.md` | The hats you wear — when to be which, triggered by what, with autonomy tiers |
| `life-capitals.md` | Your resource portfolio — the dimensions of life you invest in (framework, not content) |
| `life-compass.md` | Values + navigation — how you decide when capitals conflict |
| `me-summary.md` | Compact self-portrait — who you are in one page for fast loading |
| `psychometrics-summary.md` | Optional self-knowledge integration (CliftonStrengths, Hogan, etc.) |
| `working-style.md` | How you work with AI — extracted from accumulated interaction |
| `complementarity.md` | Where you and the AI complement each other (compensation, amplification, enablement) |

Each file carries frontmatter with `type`, `subtype`, `created`, `updated`, `sources`. This provenance lets you know six months from now whether a principle is still load-bearing or a fossil.

The eight files are not a template to fill in — they're a schema that the bootstrap ritual populates through conversation and ingest.

### 2. Bootstrap ritual

A three-part process for going from zero to populated identity files:

**Interview (90 minutes).** Structured conversation with Claude covering each dimension. The AI asks, you answer. Claude proposes drafts for each file based on your answers. You refine. You ship.

**Ingest (optional, parallel).** If you have existing writing — blog posts, journals, letters, notes — you can point the bootstrap script at them. Claude reads, summarizes patterns, proposes draft identity files based on inferred voice and values. You edit the drafts. This reuses the Mnemon capture pipeline (same pattern, different target corpus).

**Iterate from use (ongoing).** The best edits come from noticing when the AI gets something wrong. When Claude writes a message in your voice and it feels off — fix the relevant file. When Claude misremembers your priorities — update `life-capitals.md`. When a role trigger fires at the wrong time — tune `roles.md`. Identity is not static; it evolves through observed misalignment.

The bootstrap ritual does not produce perfect identity files. It produces *populated starting points* that you refine over the first month of use.

### 3. Walk-up chain spec

How the identity files get loaded into any AI session.

Atlas Seed does not require a specific AI platform or environment — but it does require the environment to support **hierarchical config loading**. Claude Code calls this the "walk-up chain": at session start, Claude reads configuration from multiple levels (global → user → project → session), with closer-scoped files overriding farther-scoped ones.

The walk-up chain spec defines:

- **Where identity files live** (`core/identity/` in your environment)
- **How they're referenced** from the environment's top-level configuration (typically `CLAUDE.md`)
- **Load order** (identity before project-specific overrides)
- **Substrate requirements** — what any substrate must provide for Atlas Seed to work
- **Privacy boundaries** — how identity doesn't leak across bounded contexts (multi-vault, multi-profile)

See `walk-up-chain.md` in this repo for the full spec.

### 4. Positioning — substrate-agnostic

Atlas Seed works with any substrate that provides:

- A location for identity files to live
- A top-level configuration file (`CLAUDE.md` by convention) that can reference them
- Persistent memory the AI reads at session start
- Session logs or equivalent continuity infrastructure

Obsidian Seed is one substrate. A bare Claude Code project with a few rules is another. A hypothetical future mobile/web AI environment would be a third — as long as it supports the four requirements above.

**The substrate is an interface, not a product.** If you're using Atlas Seed and you migrate substrates later, your identity files come with you. The substrate is replaceable; identity is yours.

This framing is prospectively important: generic knowledge aggregation (articles, books, search) will be increasingly displaced by personalization (AI adapted to your context). In that future, identity is the moat — it's what makes your AI *yours*. Keeping the substrate interface clean protects that investment.

### 5. Knowledge Metabolism — identity-side interface

Atlas Seed does not define or own the Knowledge Metabolism concept. That lives in a separate research project (see the repo's `PHILOSOPHY.md` for links). Knowledge Metabolism is the broader framework for how knowledge moves through a system: capture → extract → personalize → structure → retrieve → feedback.

Atlas Seed contributes **the identity-side interface**: what Knowledge Metabolism systems need from an identity layer to personalize processing per user.

Concretely: when a Knowledge Metabolism tool (like [Mnemon](https://github.com/dkushnikov/mnemon)) processes an incoming source and needs to decide *how to frame this for the user*, it reads the identity layer. Values and compass inform relevance ranking. Roles inform tone. Working style informs output format. Life Capitals inform where the extract gets routed. Complementarity informs what to highlight vs what to skip.

Without identity, Knowledge Metabolism produces generic extracts. With identity, it produces personalized ones. Atlas Seed alpha defines the *interface contract* between identity layer and any KM implementation. It does not prescribe the implementation.

See `knowledge-metabolism-interface.md` in this repo for the contract details.

## How to use this

### If you already have Obsidian Seed

1. Clone this repo alongside your existing `obsidian-seed` setup.
2. Run the bootstrap interview (`claude` in this directory, say "Run the bootstrap ritual for Atlas Seed").
3. Your identity files land in `core/identity/` — either in `~/Atlas/` if you have that, or in a location of your choosing.
4. Reference them from your vault's `CLAUDE.md` via walk-up chain pattern.
5. Iterate from use over the first month.

### If you don't have Obsidian Seed

You can use Atlas Seed as a thin standalone layer on top of any Claude Code project:

1. Clone this repo.
2. Create a `~/.claude/` directory if you don't have one.
3. Run the bootstrap interview.
4. Identity files go in your global Claude Code config.
5. Any project you work in reads identity through walk-up chain.

You don't need a vault. You do need persistent memory and the ability to reference identity files from a top-level config.

### If you're considering both

We recommend starting with Obsidian Seed first (it gives you the substrate), then layering Atlas Seed on top (it gives you the identity). But the order doesn't fundamentally matter — both work as standalone or combined.

## Current state (2026-04-11)

- **Schema:** 8 identity file templates with provenance frontmatter — working, in use by the project author for ~6 weeks
- **Bootstrap ritual:** interview protocol documented, ingest script conceptual (not yet shipped as executable)
- **Walk-up chain spec:** documented, working in Obsidian Seed vaults
- **Positioning:** this document
- **Knowledge Metabolism interface:** contract documented, Mnemon is a compatible consumer

**What alpha means here:** the schema and walk-up chain are proven in the author's setup. The bootstrap ritual needs external testing. The ingest script needs building. The Knowledge Metabolism interface is a contract, not a library — any implementer can conform to it.

**What you should expect:** breaking schema changes between v0.1 and v0.2. Missing implementations. Undocumented assumptions. This is alpha. If you're looking for stability, wait for v0.3+.

## Relationship to other projects

- **[Obsidian Seed](https://github.com/dkushnikov/obsidian-seed)** — substrate layer. Where knowledge lives. Atlas Seed sits on top of any Obsidian Seed vault and adds the identity layer.
- **[Mnemon](https://github.com/dkushnikov/mnemon)** — one concrete implementation of Knowledge Metabolism. Consumes Atlas Seed identity layer via the interface contract (component #5) to personalize knowledge processing.
- **[Nestor](https://github.com/dkushnikov/nestor-plugin)** — multi-model deliberation plugin. Could consume Atlas Seed identity to better frame questions for the council, but doesn't currently. Possible integration point for v0.2+.
- **[claude-environment](https://github.com/dkushnikov/claude-environment)** — infrastructure layer for Claude Code (multi-machine setup, data pipelines). Orthogonal to Atlas Seed — identity is content, environment is plumbing.

## Philosophy (the short version)

Most "AI + personal context" attempts fail because they confuse three things: your *notes* (content), your *tools* (plumbing), and your *self* (identity). They try to feed the AI notes and expect it to learn who you are. It doesn't work — or works slowly, partially, inconsistently.

Atlas Seed takes the opposite approach: **make yourself explicit, up front, in a form the AI can load in every session**. Not everything about you — just enough that the AI has a working model. Values, roles, compass, working style, complementarity. Eight small files. Less than a day to populate. Loaded automatically forever after.

The effect compounds. Session one with identity feels like session one with a smart stranger who read your resume. Session ten feels like session ten with a partner who has *thought about* your resume. The difference is identity being *present in the loop*, not retrieved on demand.

For the longer philosophy, see `PHILOSOPHY.md`.

## Contributing

This is v0.1 alpha. The most useful contribution is **running it**: go through the bootstrap ritual, tell us where it broke, tell us what was missing, tell us what was surprising. Open an issue.

We're not yet accepting PRs on the schema — it's stabilizing. PRs on documentation, typos, examples, and the walk-up chain spec are welcome.

## License

MIT

## Credits

Born out of Obsidian Seed and the broader Atlas project. Inspired by — but different from — [personal-context](https://github.com/amr05008/personal-context) (portraits vs working identities, different genres). Converged with [Karpathy's Raw → Wiki → Frontend pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) on the underlying architecture of personal AI systems. Knowledge Metabolism framework developed independently.
