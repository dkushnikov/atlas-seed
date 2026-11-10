# Knowledge Metabolism — Identity-Side Interface

**The contract between Atlas Seed's identity layer and any Knowledge Metabolism implementation that wants to personalize processing per user.**

> **Important framing:** This document does NOT define Knowledge Metabolism. The full concept and research live in a separate project (see "Relationship to the research" below). This document defines only the **interface contract** — what Atlas Seed's identity layer exposes to KM systems, and what KM systems can rely on from the identity layer.
>
> If you're looking for "what is Knowledge Metabolism," read the research doc, not this one. If you're implementing a KM system and want to consume Atlas Seed identity, this is the right document.

---

## What this is

Atlas Seed's identity layer is a set of markdown files describing who the user is (see `identity-schema.md`). Knowledge Metabolism is a framework for how knowledge moves through a system: capture → extract → personalize → structure → retrieve → feedback.

**Personalization is the meeting point.** Any Knowledge Metabolism system that wants to produce *personalized* output (not generic summaries) needs an input that says "who is this user?". That input is the identity layer.

This document defines the **interface contract**: what Atlas Seed guarantees to provide, what KM systems can assume, and what the boundaries are.

## Relationship to the research

The Knowledge Metabolism research project (a separate project of the author, not yet published) contains:

- The full biological metabolism metaphor (ingestion → digestion → absorption → metabolism → circulation → elimination)
- Mapping to ~10 existing knowledge management frameworks (SECI, CODE, GTD, Boundary Objects, Double-Loop Learning, Cynefin, DIKW, Kepinski's Information Metabolism, etc.)
- Gap analysis of what exists in the market vs what's missing
- Market landscape of tools partially implementing the concept (Tana, Fabric/PAI, Granola, Rosebud, Mind Cortex, AudioPen, Voicenotes, Limitless)
- Validation that "Knowledge Metabolism" as a framework name is available (no established framework owns it)

**Atlas Seed does not redefine or compete with that research.** It provides one piece: the identity-side input that personalizes processing.

The relationship in one line: **Knowledge Metabolism is the cycle; Atlas Seed's identity layer is one of its inputs.**

**Scope note (2026-11-10).** Atlas Seed supports three ways of running: ChatGPT (files you keep and paste), Codex and Claude Code (a folder with `AGENTS.md`). A KM system is an *extension* on top of the folder case: it reads files from a folder the user names. Nothing in this repository installs, connects or runs one. The ChatGPT route has no folder and therefore no KM consumer; the user pastes what a tool should know.

## What the identity layer exposes

A KM system consuming Atlas Seed can read any or all of the eight identity files. In practice, the most useful inputs per KM stage are:

### For *absorption* (routing to correct context)

The question at this stage is: *where does this incoming knowledge belong?*

Identity inputs:

- **`life-capitals.md`** — the user's resource portfolio. A KM system routes an article about sleep science to the Physical capital, an article about investment strategy to Financial, an article about a relationship framework to Social. The user's capital breakdown defines the routing space.
- **`roles.md`** — the user's modes. An article about leadership practice might route differently if the user has an "executive" role versus a "practitioner" role in their identity.
- **`me-summary.md`** — the fast-loading compressed self-portrait. For routing decisions where full context isn't needed, this alone is often enough signal.

### For *metabolism* (transformation into artifact)

The question at this stage is: *how should this be framed for the user?*

Identity inputs:

- **`working-style.md`** — tone, preferences, interaction protocol. Determines format (bullet list vs prose, formal vs ironic, Russian vs English).
- **`life-compass.md`** — values and principles. Determines which aspects of the source to highlight vs de-emphasize (e.g., a user who values "time is the only non-renewable resource" gets time-cost framing emphasized).
- **`psychometrics-summary.md`** (if present) — top strengths and blind spots. A user with low Empathy score gets different framing than a user with high Empathy — not because the content is different, but because the user's natural attention differs.

### For *circulation* (cross-context routing)

The question at this stage is: *this knowledge is relevant in multiple contexts — which ones, and how?*

Identity inputs:

- **`life-capitals.md`** — if an insight touches three capitals, it should circulate to all three. The capital structure defines the circulation map.
- **`complementarity.md`** — what does the user need the AI to compensate for? An insight relevant to a compensation gap gets prioritized for circulation.

### For *feedback loop* (system learning over time)

The question at this stage is: *did this processing produce useful output? how do we learn?*

Identity inputs:

- **`SOUL.md`** — constitutional principles. Feedback loops should tune *toward* these principles, not away. If "honesty over comfort" is a Soul principle, the system shouldn't learn to produce softer output even if the user occasionally rewards softness in a specific moment.
- **`working-style.md`** — updated from observed misalignment. Feedback from user corrections can propose edits to working-style, but always with user ratification before writing (see iterate-from-use in `bootstrap-ritual.md`).

---

## What KM systems can assume

Any KM implementation consuming Atlas Seed's identity layer can assume:

### A1: Files exist at stable paths

The eight identity files live at predictable paths: the folder the user's instruction file (`AGENTS.md`, `CLAUDE.md`) names, `identity/<file>.md` in the templates and `core/identity/<file>.md` in the author's setup. A KM system takes the folder from its own configuration or from that instruction file; it does not guess.

### A2: Frontmatter schema is consistent

All identity files carry `type: identity`, `subtype: <specific>`, `created`, `updated`, `sources`. KM systems can parse this frontmatter to determine freshness, provenance, and which file they're reading.

### A3: Content is markdown with defined section schemas

Each file has a documented section schema (see `identity-schema.md`). KM systems can rely on section headers being present in the expected form (e.g., `## Constitution` in `SOUL.md`, `## Values` in `life-compass.md`).

### A4: Updates are visible via `updated` field

When the user refines an identity file, the `updated` frontmatter field changes. KM systems caching identity can detect staleness and reload.

### A5: Privacy boundaries are a policy the user states and a mechanism the environment may or may not provide

The user decides where identity may be read (`walk-up-chain.md` § Privacy boundaries). Where the environment has an enforcement mechanism (Codex permission profiles, Claude Code deny rules, a folder the agent cannot reach), that mechanism is what prevents access. Where it has none, nothing does. A KM system must therefore: read only the folder it was pointed at; treat a stated policy ("do not read identity in this context") as binding on itself; and never present "the substrate prevents it" as a guarantee to the user. Atlas Seed states requirements here; it ships no enforcement.

## What KM systems should NOT assume

### NA1: Identity files are structured data

They are markdown, not JSON. Parsing is language-level (regex, heading detection, paragraph parsing), not schema-level. Don't expect typed fields.

### NA2: All eight files exist

`psychometrics-summary.md` is optional. Any file could be missing if the user skipped it during bootstrap. KM systems should degrade gracefully when a file is absent.

### NA3: Content is complete

Identity files are working documents, not exhaustive reference. A user's `life-capitals.md` lists the capitals they track; it doesn't prove those are the only dimensions of their life. Don't over-infer from absence.

### NA4: The identity layer is recent

A user might have populated identity three months ago and not touched it since. That's valid — stability is the point. KM systems should not assume fresh identity every session.

### NA5: All users are technical

Identity files are readable by humans too. A KM system shouldn't produce output that references internal identity file structure to the user. The user knows their `life-compass.md` exists; they don't need to see "based on your life-compass.md file's Values section..." as verbatim attribution.

---

## Concrete example: Mnemon consuming Atlas Seed

[Mnemon](https://github.com/dkushnikov/mnemon) is one concrete Knowledge Metabolism implementation — it captures external sources (articles, podcasts, papers, ideas) and produces structured extracts framed for the user. Mnemon reads a `reader-context.md` file today for personalization.

**How Mnemon could consume Atlas Seed:**

1. **At extract time**, Mnemon reads `me-summary.md` for fast user context and `life-capitals.md` for routing signal.
2. **For source-type-specific framing**, Mnemon reads `working-style.md` to determine tone (formal/casual) and format (bullets/prose).
3. **For value framing** (what aspects of the source to emphasize), Mnemon reads `life-compass.md` for values and principles.
4. **For routing to destination**, Mnemon uses `life-capitals.md` capital breakdown as the routing space — which capital does this source belong to?
5. **For cross-capital relevance**, Mnemon uses `life-capitals.md` plus the "Pattern" section that links capitals to concrete Areas.

**What Mnemon does NOT need from Atlas Seed:**

- Direct access to `SOUL.md` — Soul principles are high-level, not source-specific. Mnemon's extract doesn't reference Soul directly.
- Real-time updates — identity changes slowly, daily re-reads are wasteful. Mnemon can cache identity for an hour+ without drift.
- Write access — Mnemon reads identity, never writes it. Write access belongs to the user and the bootstrap/iterate ritual.

**What Mnemon's existing `reader-context.md` becomes:**

Mnemon's current `reader-context.md` is a single flat file containing what Atlas Seed decomposes into 6-8 identity files. When Atlas Seed adoption happens, Mnemon can:

- **Option 1:** Keep `reader-context.md` as a Mnemon-internal compressed view, populated from Atlas Seed identity files at bootstrap
- **Option 2:** Deprecate `reader-context.md`, read directly from Atlas Seed identity layer at extract time
- **Option 3:** Support both — Mnemon picks up Atlas Seed if present, falls back to `reader-context.md` if not

Option 3 is the graceful adoption path. Mnemon v2 could support both. Atlas Seed v0.2 may document this as the recommended integration.

## Concrete example: a hypothetical KM system without Atlas Seed

A KM system running in an environment without Atlas Seed has three options:

1. **Produce generic output.** The source is extracted and structured, but not personalized. Functional but forgettable.
2. **Maintain its own user-context file.** Something like Mnemon's current `reader-context.md` — a single file the user populates once. Works, but redundant if the user later adopts Atlas Seed.
3. **Support Atlas Seed optionally.** Check for identity files; if present, use them; if absent, fall back to generic or ask the user to populate a context file.

The recommendation for new KM system implementers is option 3: support Atlas Seed identity as an optional personalization input. Graceful degradation when not present. Users who adopt Atlas Seed get better output; users who don't get the same output as today.

## Interface versioning

This contract is **v0.1 alpha**. Expect:

- Section header names in identity files may refine (v0.2 — breaking for parsers relying on exact matches)
- New optional identity files may be added (v0.2+ — non-breaking)
- Frontmatter schema is stable in v0.1 — changes would be breaking and avoided

**For implementers:** treat this contract as unstable until v0.3. Write consumers to be tolerant of minor schema shifts. Cache parsed identity with a version marker so upgrades can invalidate cache cleanly.

## What this interface enables

The point of documenting this contract is **decoupling**. Without it:

- Each KM system invents its own user-context format
- Users populate multiple redundant context files (one per tool)
- No portability — switching tools means rewriting everything

With this interface:

- One identity layer, many KM consumers
- Users populate identity once, get personalized output from every tool that supports the interface
- Portability — switching tools keeps identity
- **Identity becomes a protocol-level artifact, not a tool-level artifact** — and that's what makes it valuable in the long term

## Non-goals

This interface does NOT define:

- How a KM system implements capture, extraction, or routing (that's the KM system's own design)
- What "Knowledge Metabolism" means philosophically (see the research doc)
- How personalization should work internally in a specific KM system (that's implementation)
- What the user should do with extracted output (that's vault / substrate concerns)

This interface ONLY defines: **how a KM system reads Atlas Seed's identity layer.**

---

## For implementers — checklist

If you're building a KM system that wants to support Atlas Seed identity:

- [ ] Resolve identity file paths through substrate's walk-up chain or direct config
- [ ] Parse frontmatter for `type: identity`, `subtype: <name>`, `updated`
- [ ] Parse markdown sections per `identity-schema.md` schemas
- [ ] Degrade gracefully when files are missing (especially `psychometrics-summary.md`)
- [ ] Cache identity for efficiency (identity changes slowly, don't re-read per request)
- [ ] Respect the user's stated privacy policy yourself (if a context excludes identity, skip; do not rely on the environment to stop you)
- [ ] Treat identity as read-only (never propose writes from KM system; writes go through user's iterate-from-use ritual)
- [ ] Version your identity cache against schema v0.1 so upgrades can invalidate correctly
- [ ] Document your KM system's use of identity in your own README so users know what's consumed
