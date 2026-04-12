# Walk-Up Chain Spec

**How identity files get loaded into every AI session, across any substrate.**

> **Audience:** this spec is for people who want to implement Atlas Seed on a substrate other than Claude Code, OR who want to understand exactly how Claude Code loads the identity layer. If you're just a user running Atlas Seed with Claude Code + Obsidian Seed, this spec is background — you don't need to read it to use the system.

---

## What "walk-up chain" means

**Walk-up chain** is a hierarchical configuration loading pattern: at session start, the AI reads configuration from multiple levels of scope, starting at the broadest (global) and walking toward the narrowest (project/session), with closer-scoped files overriding or augmenting farther-scoped ones.

The term comes from how Claude Code loads `CLAUDE.md` files: it starts at the project directory, then walks *up* the directory tree (checking each parent for a `CLAUDE.md`), then consults user-global and system-global levels. Each `CLAUDE.md` it finds gets loaded, with closer files having higher precedence.

For Atlas Seed, the walk-up chain is how identity files become available to every session automatically — no manual imports, no session-start boilerplate, no copy-paste between projects.

**The core claim:** if the substrate supports a walk-up chain, the identity layer can be made available to every session with zero per-session effort. If the substrate doesn't support it, identity loading becomes manual and the value drops sharply.

## Heritage

Walk-up chain as a concept comes from the Unified Claude project (2026-04). It was the mechanism that allowed a single identity definition (Atlas) to be visible across multiple project-scoped Claude Code sessions without duplication. The same pattern was then generalized as the preferred way to load any cross-project configuration in Claude Code.

Atlas Seed inherits this pattern and formalizes it as the identity loading mechanism. The pattern was developed as part of the Atlas project for unified AI identity management.

## The spec

### Load order

Atlas Seed expects the following load order during session start, from broadest to narrowest:

1. **System-global configuration** — whatever the substrate uses for system-wide settings (usually absent for personal use)
2. **User-global configuration** — `~/.claude/CLAUDE.md` in the Claude Code case, or equivalent in other substrates
3. **Atlas-user configuration** — `~/Atlas/core/CLAUDE.md` in the reference implementation. This is where identity files are referenced via walk-up.
4. **Project/vault configuration** — `<project_root>/CLAUDE.md`, the closest scope. Inherits from above, can override.
5. **Session-specific overrides** — transient, via session start hooks or runtime instructions. Not persistent.

**Identity files are referenced at level 3 (Atlas-user configuration).** The file `~/Atlas/core/CLAUDE.md` contains pointers into `~/Atlas/core/identity/` (the eight identity files described in `identity-schema.md`). Because level 3 sits in the walk-up chain, every project-level session inherits the identity reference automatically.

### The reference mechanism

The identity files are not *copied* into each session — they are *referenced* from the Atlas-user CLAUDE.md. The reference takes the form of explicit path or import statement, depending on substrate.

In Claude Code specifically:

```markdown
# Atlas — Unified AI Identity

I am Atlas — [user]'s AI partner.

Soul, roles, working-style, and person framework are in `~/Atlas/core/identity/`
(load on demand when session work requires depth).
```

Note the phrase **"load on demand when session work requires depth"**: identity files are NOT loaded into the context window at session start by default. They are *referenced* — Claude knows where they are and loads them when work requires it. This is a deliberate choice to keep session start costs low while preserving identity availability.

For substrates without lazy-load semantics, an alternative is a compact summary that loads at session start (e.g. `me-summary.md`, kept deliberately short) with full files loaded on demand.

### How closer scopes interact with identity

A project-level `CLAUDE.md` (level 4 in the chain) does NOT typically override identity — identity is stable, project-level is situational. The standard interaction is:

- **Project inherits identity** from the walk-up chain (level 3)
- **Project adds project-specific context** (vault structure, conventions, current work)
- **Project does NOT contradict identity** (if a project CLAUDE.md says "don't challenge me", and SOUL.md says "challenge is the contract", the Soul wins)

Projects that genuinely need to adjust identity (e.g., role mode switching for work vs personal contexts) should do so via explicit role activation, not by re-defining identity.

### Privacy boundaries

The walk-up chain respects bounded contexts. Specifically:

- **Identity is readable across all bounded contexts** by default — this is the point of a stable self.
- **Project memory and session logs are NOT readable across bounded contexts** — these are project-scoped.
- **Certain vaults (Sanctum, Private) may exclude even identity references** if they're designed for isolation. Sanctum's privacy policy overrides identity loading — Atlas Seed respects substrate-level privacy.

In practice: if a substrate has a deny-all-export policy for a particular vault, identity loading should be EITHER skipped entirely OR marked read-only with explicit user consent per session. The Sanctum case is the reference example — see Obsidian Seed documentation on vault-level privacy.

**Concrete guarantee:** no session log, no memory write, and no Claude response inside a bounded private context leaks back into the identity layer. Identity is a read source for private contexts, not a write target.

---

## Substrate requirements

**Any substrate that hosts Atlas Seed must provide the following.** If a substrate can't meet these requirements, Atlas Seed won't work without adaptation.

### R1: Hierarchical configuration loading

The substrate must load configuration from multiple scope levels automatically at session start, with closer-scoped files augmenting or overriding broader ones.

Claude Code satisfies this natively via `CLAUDE.md` walk-up. Other substrates may need a plugin, hook, or manual import mechanism.

**Minimum:** at least two levels — user-global and project-local.
**Recommended:** three or more levels including an intermediate "Atlas-user" level for identity.

### R2: Stable file paths for identity

The substrate must support a stable location where identity files live, accessible from config loading.

Reference implementation: `~/Atlas/core/identity/` on a Unix filesystem, with the eight identity files as flat markdown.

**Requirement:** path must be stable across sessions, machines (via sync), and substrate upgrades. Identity files are the most stable artifacts in the system; their path shouldn't break on every tool update.

**Acceptable alternatives:** Cloud-sync directory (iCloud, Dropbox, Syncthing), git repository, or a substrate-managed location with a stable canonical path.

### R3: On-demand file loading

The substrate's AI must support reading additional files during a session when instructed. Identity files are referenced at session start but loaded lazily when work requires depth.

Claude Code satisfies this via the Read tool. Other substrates need equivalent capability.

**Fallback for substrates without lazy load:** preload a compact summary (`me-summary.md`) at session start, load full files only when explicitly invoked. Costs more session-start tokens but still works.

### R4: Persistent memory

The substrate must support persistent memory the AI reads at session start — decisions, preferences, and context that survive between sessions.

Claude Code calls this `MEMORY.md` (auto-memory). Other substrates may use different mechanisms (memory plugins, embedded databases, session log history).

**Requirement:** memory must be *writable during session* and *readable at next session start*. One-way load or manual copy-paste doesn't count.

### R5: Session continuity infrastructure

The substrate must support session logs or equivalent continuity — a way to record what a session accomplished, referenceable by future sessions.

Reference implementation: `_claude/session-logs/YYYY-MM-DD — Title.md` files in each vault.

**Requirement:** session history must be retrievable by the AI at next session start, not just stored-for-humans.

### R6: Minimum frontmatter schema support

Identity files carry frontmatter for provenance:

```yaml
---
type: identity
subtype: soul
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources:
  - "session: YYYY-MM-DD — title"
  - "path to canonical long version, if any"
---
```

The substrate doesn't need to enforce this schema, but the AI must be able to parse it. Claude Code handles this natively (reads YAML frontmatter in markdown files). Other substrates: verify frontmatter parsing before adopting Atlas Seed.

### R7: Privacy boundaries respect

If the substrate supports bounded contexts (multiple vaults, profiles, isolated projects), the substrate must provide a way to:

- Mark contexts as "identity-excluded" (identity not loaded)
- Prevent session memory or logs from leaking across boundaries
- Distinguish "read identity, don't write" from "read and write"

This is necessary for privacy-sensitive contexts. See the Sanctum reference case in Obsidian Seed documentation.

### Non-requirements (explicit)

Substrates do NOT need to provide:

- **A vault** (identity works without one — Obsidian Seed is just one substrate option)
- **A graph view** (identity is flat markdown, no graph traversal required)
- **Mobile access** (identity works on any platform the AI can run on, but mobile is not a hard requirement)
- **Cloud sync** (local-only substrates work; sync is user preference, not architectural requirement)
- **Version control** (git is recommended but not required; identity files work without git)
- **Real-time editing** (identity files are edited between sessions, not during)

---

## Portability

A key claim of Atlas Seed is that identity is **portable across substrates**. If you set up Atlas Seed today with Claude Code + Obsidian Seed, and in two years you migrate to a different AI environment, your identity files come with you.

**What makes this possible:**

- Identity files are flat markdown with YAML frontmatter — works anywhere markdown works
- The schema is substrate-agnostic — no assumptions about Claude, Obsidian, or any specific tool
- The walk-up chain pattern is implementable on most substrates (direct support in Claude Code, plugin/hook support possible in others)
- Privacy boundaries are policy, not implementation — any substrate with access control can respect them

**What doesn't come with you:**

- Substrate-specific configuration (CLAUDE.md contents, Obsidian vault conventions)
- Runtime memory (MEMORY.md gets reset unless you also migrate that)
- Session logs (unless you manually migrate the directory)

**The interface boundary:** identity files and their schema are portable. Everything else is substrate-coupled. If you're designing Atlas Seed usage for portability, keep identity separate from substrate-specific content.

---

## Implementing on a non-Claude-Code substrate

If you're porting Atlas Seed to a substrate other than Claude Code, this checklist helps:

1. **Verify substrate satisfies R1-R7** (requirements above). If any are missing, identify workarounds or decide whether the substrate is compatible.
2. **Map substrate's config loading mechanism to the walk-up chain concept.** Document how level 3 (Atlas-user config) will work.
3. **Choose a stable path for identity files.** Document the expected absolute path in the substrate's conventions.
4. **Implement identity references** in the substrate's user-global config, pointing at the identity files.
5. **Test privacy boundaries** — verify bounded contexts don't leak identity writes or session content.
6. **Document substrate-specific quirks** in a section labeled "On [substrate]" in this spec or a sibling doc.
7. **Share your implementation** — open a PR to this repo with a new document describing the adaptation. Helps the next person.

## Future work (v0.2+)

Explicitly not in alpha, flagged for future:

- **Automatic substrate detection and adaptation** — right now adoption is manual; future versions could sniff the substrate and configure automatically.
- **Cross-substrate migration tooling** — scripts that move identity files between substrates with validation.
- **Walk-up chain verification tool** — a script that checks whether a substrate's config loading actually loads identity correctly (catches silent misconfiguration).
- **Multi-machine walk-up** — when identity lives on multiple machines (e.g., laptop + server), how does walk-up chain coordinate? Captured in Distributed Atlas project, not alpha scope.
