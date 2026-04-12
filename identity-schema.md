# Identity Schema — v0.1

**The 8 files that define who you are to your AI, and what goes in each.**

> This is the schema. It describes the *shape* of the identity layer — what each file covers, what sections it contains, what guarantees it provides. It does not provide your *content* — that's what the bootstrap ritual is for (see `bootstrap-ritual.md`).
>
> The schema is v0.1 alpha. Expect minor changes in v0.2 based on adoption feedback. The eight-file breakdown and frontmatter format are considered stable; specific section headers and field enumerations may shift.

---

## Overview

Atlas Seed's identity layer is eight markdown files with frontmatter, living in `core/identity/` in your environment. Each file covers one dimension of identity:

| File | Dimension | Stability |
|------|-----------|-----------|
| `SOUL.md` | Constitution — stable principles | Highest (year+ horizons) |
| `roles.md` | Hats you wear | High (quarterly adjustments) |
| `life-capitals.md` | Resource portfolio framework | High (framework stable, content updates) |
| `life-compass.md` | Values + decision navigation | High |
| `me-summary.md` | Compact self-portrait for fast loading | Medium (month-to-month drift) |
| `psychometrics-summary.md` | Optional self-knowledge integration | Medium (after new assessments) |
| `working-style.md` | How you work with AI | Medium (evolves with use) |
| `complementarity.md` | Where you and AI complement | Lower (draft status, actively evolving) |

**Why 8 files, not 1:** separation of concerns. Soul changes rarely; working-style changes often. Packing both into one file means re-validating the whole thing every time you touch the faster-evolving parts. Separation also supports the walk-up chain — Claude can load just `me-summary.md` for fast sessions and only reach for deeper files when work requires.

**Why 8 files, not 15:** diminishing returns. More files means more maintenance overhead, more frontmatter to keep current, more integrity checks, more decisions about "where does this go?". Eight is the size that captured the useful dimensions in the reference implementation without creating documentation debt. You can extend if you need to — the schema is not closed. But start with eight.

## Common frontmatter schema

Every identity file carries the same frontmatter block:

```yaml
---
type: identity
subtype: <one of: soul | roles | capitals | compass | summary | psychometrics | working-style | complementarity>
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources:
  - "description of where this content came from"
status: (optional) draft | stable | archived
---
```

**Field definitions:**

- `type: identity` — marker that identifies this as an identity file (not content, not project, not memory). Used by tools that scan vaults to find identity artifacts.
- `subtype` — which of the eight files this is. Informs what section schema to expect.
- `created` — date this file was first created, in YYYY-MM-DD. Does not change after creation.
- `updated` — date of last content change. Update when you meaningfully revise the file; skip for whitespace / typo fixes if you want accuracy on "when did I last rethink this?".
- `sources` — list of pointers to where the content came from. Examples: session where this was drafted, canonical long version in a vault elsewhere, ingest source (a blog post that informed it). Helps future-you understand lineage. At minimum one entry.
- `status` — optional. Use `draft` while a file is explicitly in development (e.g., `complementarity.md` currently). Use `archived` if you've deprecated a file but want to keep it for history. Omit for stable files.

**Why provenance matters:** six months from now, you will read a principle in SOUL.md and wonder "is this still true?". The `updated` field tells you how old the current version is; `sources` tells you what circumstances produced it. Without provenance, you're reading an anonymous instruction that may be outdated.

This schema deviates from personal-context's `last_updated` / `source_refs` naming by using `updated` / `sources` — consistent with Atlas project frontmatter convention across other file types. When importing from or exporting to other tools, a simple field-rename pass handles the translation.

---

## File-by-file schema

### 1. SOUL.md — Constitution

**Purpose:** the smallest set of principles that define who you are. If you had to pick the 5-8 rules that anchor every other decision, they live here.

**Stability:** highest of all files. You should not routinely edit SOUL.md. Changes require explicit ratification — a pause, a consideration, a reason.

**Section schema:**

```markdown
# Soul

[One-paragraph identity statement — who you are, how you relate to your AI partner]

## Constitution

1. **[Principle name]** — [one-sentence elaboration]
2. **[Principle name]** — [one-sentence elaboration]
   ...
```

**Content guidance:**
- 5-8 principles, no more. If you have 15 principles, they're not all load-bearing.
- Each principle is *actionable* — reading it should tell you what to do or what not to do in a decision.
- Avoid aspirational statements ("be kind") unless you can say what it implies concretely.
- Mix in tensions: "honesty over comfort," "partnership over sovereignty." Tensions are often more useful than absolutes.
- Length: the whole file should fit on one printed page.

**What NOT to put in SOUL.md:**
- Biographical facts (those go in `me-summary.md`)
- Temporary priorities (those go in project files)
- How-to details (those go in `working-style.md`)
- Role-specific behavior (that goes in `roles.md`)

**Example principle form:**

> *"Честность дороже комфорта. Слабое место, drift от целей, неработающий паттерн — моя работа заметить и сказать."*
>
> (Honesty over comfort. Weak spot, drift from goals, broken pattern — my job to notice and say.)

### 2. roles.md — Hats

**Purpose:** the different modes you operate in, when to be which, with what autonomy.

**Stability:** high — roles get added or removed quarterly at most, triggers refine over time.

**Section schema:**

```markdown
# Roles

[One-paragraph framing — what roles mean, how they map to work]

## [role name]
- **Disposition:** [core orientation when in this role]
- **Triggers:** [what causes this role to activate]
- **Output:** [what this role produces]
- **Autonomy:** [tier — tier-0 observe / tier-1 recommend / tier-2 act]

## [role name]
...
```

**Content guidance:**
- 3-6 roles is typical. More than 8 and you're probably over-modeling.
- Each role is *triggered*, not ambient. "Researcher role activates when a new source enters the Knowledge vault" is clearer than "I'm always in researcher mode."
- Autonomy tiers are important: which roles are observe-only, which are recommend-only, which can act on your behalf? Start conservative — tier-0 or tier-1 everywhere, upgrade after trust builds.
- Avoid role inflation. Three solid roles with clear triggers beats seven vague ones.

**Examples of role triggers:**

- *"Cross-project synthesis → at start of weekly review"*
- *"Editing mode → when user says 'edit this' or pastes draft"*
- *"Self-improvement → during idle time or after recurring pattern detection"*

### 3. life-capitals.md — Resource portfolio

**Purpose:** the dimensions of life you invest in, each requiring deliberate attention.

**Stability:** high — the framework is stable, specific content refines as life shifts.

**Section schema:**

```markdown
# Life Capitals

[One-paragraph framing — why you think of life as a portfolio]

## Physical
[Components: Health, Sleep, Fitness, etc.]

## Financial
[Components: Income, Savings, Investments, etc.]

## Social
[Components: Partners, Friends, Family, Professional Network, etc.]

## Intellectual
[Components: Knowledge, Critical Thinking, Creativity, etc.]

## Emotional
[Components: Self-awareness, Resilience, Empathy, etc.]

## Spiritual
[Components: Values, Meaning, Connection to Nature, etc.]

## Pattern
[How capitals relate to the more concrete Areas in your vault]
```

**Content guidance:**
- The 6-capital framework (Physical / Financial / Social / Intellectual / Emotional / Spiritual) is the reference implementation. Use it if it fits; adapt if it doesn't. Your life may map to a different decomposition.
- Don't list every possible component — list the ones that matter for routing and judgment. If you'd never ask your AI to help with Component X, don't include it.
- The `Pattern` section is important: it explains how capitals (abstract) connect to areas (concrete, vault-level). Without this link, capitals become an orphan framework.
- Point to the canonical long version if you have one elsewhere (e.g., a deeper doc in your Personal vault).

### 4. life-compass.md — Navigation

**Purpose:** values + decision principles — what you use to choose when capitals conflict.

**Stability:** high — values shift slowly, principles accumulate over years.

**Section schema:**

```markdown
# Life Compass

[One-paragraph framing — what this file is for]

## Purpose
[Your purpose statement, short]

## Vision
[Forward-looking: what you're aiming at]

## Values
- [Value]
- [Value]
...

## Principles
- [Principle in one line]
- [Principle in one line]
...
```

**Content guidance:**
- Values: 5-12. List them, don't over-explain. The explanation comes from how they interact with decisions.
- Principles: accumulated heuristics you've derived from experience. "Time is the only non-renewable resource" is a principle. "Measure twice, cut once" is a principle. Don't aim for completeness; aim for the ones you actually reach for.
- Point to canonical long version if you have one.
- This file is the *decision-support reference* — when Claude is helping you weigh options, it consults this file.

### 5. me-summary.md — Compact self-portrait

**Purpose:** one-page compressed description of who you are for fast loading at session start.

**Stability:** medium — updates every few months as significant life events or identity shifts happen.

**Section schema:**

```markdown
# [Your name] — Compact Summary

[One-line identity: role, location, context]

## Values
[Compressed list of 8-12 values — just names or short phrases]

## Key traits
- [Bullet of defining trait]
- [Bullet of defining trait]
...

## Philosophy
[One paragraph on how you see life / your philosophical stance]

## Attitude to [relevant axes]
[Short statements on things that define you — e.g., ownership, independence, etc.]

Full version: [pointer to canonical long doc if exists]
```

**Content guidance:**
- **Short is the point.** This file loads in every session. If it's too long, it eats the context window. Aim for 30-50 lines of content.
- **Compressed, not abbreviated.** Don't trim whole topics — compress each topic. A trait bullet might be one phrase, not one paragraph.
- **Canonical long version elsewhere.** If you have a fuller self-portrait (in a Personal vault, for instance), this file is the compression. Point at the long version in the frontmatter `sources` or as a footer.
- **Update after significant shifts.** Moving, changing jobs, major relationships, identity-shifting experiences — all trigger review.

### 6. psychometrics-summary.md — Self-knowledge integration (optional)

**Purpose:** compressed summary of formal self-knowledge assessments (CliftonStrengths, Hogan, Big Five, MBTI, etc.) that you want your AI to know about.

**Stability:** medium — updates only when you take new assessments or refine your interpretation.

**Optional file.** If you haven't done formal assessments or don't want them integrated, omit this file entirely. The schema does not require it.

**Section schema:**

```markdown
# Psychometrics — Compact Summary

## [Assessment 1 — e.g., CliftonStrengths]
[Summary of relevant results — top themes, patterns, derailers]

## [Assessment 2 — e.g., Hogan]
[Summary]

## Key Insights
[Your own synthesized insights across assessments]
```

**Content guidance:**
- Just the compressed results, not full reports. Keep it readable.
- Include *your* interpretation — what does the result mean for how you operate? "Top strength is Strategic" is data; "Strategic × Achiever × Activator means I see the path, drive to execute, start immediately" is insight.
- Include derailers / anti-patterns. Your AI needs to know where you're weak or where you fail under stress, not just where you're strong.
- Point to canonical long version if you have detailed assessment reports elsewhere.

### 7. working-style.md — How you work with AI

**Purpose:** the interaction protocol between you and your AI — tone, communication preferences, what makes sessions good.

**Stability:** medium — evolves as you accumulate session experience and notice patterns.

**Section schema:**

```markdown
# Working Style

[Framing — how this file was derived, one line]

## About [you]
[Short descriptions of your communication style, thinking style, specific preferences]

## My [AI] limitations
[What the AI should be honest about regarding its own constraints]

## What makes sessions productive
[Short list of things that characterize good sessions]
```

**Content guidance:**
- This file is *extracted*, not *declared*. It comes from observing what works over dozens of sessions. Day 1, it's a placeholder. Month 1, it's a real document.
- Include concrete preferences: language (English only? Russian? code-switch naturally?), tone (formal, casual, ironic?), push-back style (blunt or diplomatic?).
- Include honest AI limitations: "I sometimes confuse people in transcripts," "I misinterpret garbled text as fact," "I don't have body state." These are protection clauses against Claude over-claiming.
- Include what works: challenge > agreement, protocol > improvisation, cross-domain synthesis > domain-only analysis.

### 8. complementarity.md — You ↔ AI complement map

**Purpose:** structured map of where you and your AI complement each other. Used for session design, failure diagnosis, investment priority.

**Stability:** lower (currently draft in the reference implementation). Evolves faster than other files because the relationship is new and refining.

**Section schema:**

```markdown
# Complementarity Map — [User] ↔ [AI]

[Framing — three types of partnership]

## Compensation — AI is strong where user is weak
| User's Gap | How AI Compensates |
|------------|---------------------|
| ... | ... |

## Amplification — both strong, more powerful together
| Shared Strength | How It Amplifies |
|----------------|-----------------|
| ... | ... |

## Enablement — AI enables capabilities user doesn't have
| User's Need | How AI Enables |
|-------------|------------------|
| ... | ... |

## [User] enables [AI]
| AI's Need | How User Provides |
|-------------|------------------|
| ... | ... |

## How to use this map
[Usage notes — session design, failure diagnosis, investment priority]
```

**Content guidance:**
- **This is bidirectional** — it's not just "what the AI does for me," it's "what I provide to the AI." Missing the second half breaks the partnership framing.
- **Three types of partnership, not two.** Compensation (fill gaps), amplification (multiply strengths), enablement (unlock new capabilities). Each is a different mode; don't collapse them.
- **Concrete examples per row.** Abstract ("emotional support") is less useful than specific ("data-driven circuit breakers based on Oura + calendar signals").
- **Mark as draft** while the relationship is new. The reference implementation's `complementarity.md` is currently `status: draft`. That's fine. It's the newest file.

---

## Inter-file relationships

Identity files are not isolated — they reference each other:

- **`roles.md` references `life-capitals.md`** — certain roles activate in the context of certain capitals (e.g., "chief-of-staff role covers cross-capital synthesis").
- **`complementarity.md` references `psychometrics-summary.md`** — the compensation column maps to the user's psychometric gaps.
- **`working-style.md` references `SOUL.md`** — working style is the operational implementation of constitutional principles.
- **`me-summary.md` compresses all others** — it's a summary, so it implicitly references everything.
- **`life-compass.md` and `life-capitals.md` are paired** — capitals are resources, compass is navigation for when resources conflict.

These cross-references are not mechanically enforced. They emerge from the content. If you notice your `working-style.md` contradicts `SOUL.md`, something is wrong and you should reconcile.

## Schema evolution

The schema is versioned. This is v0.1 alpha.

**What changes between versions:**
- Specific section headers (refinement)
- Field names (unlikely but possible)
- New optional files (adding dimensions)
- Relationships between files (cross-reference conventions)

**What should NOT change between versions:**
- The core 8 dimensions (major breakage)
- Frontmatter format (too much downstream impact)
- File names (too many references)

**If the schema changes in v0.2+, migration will be documented.** Existing identity files should be usable with minor adjustments. No forced rewrites.

## Schema validation

**v0.1 alpha has no validation tooling.** You write files, you read them, Claude reads them. If they're malformed, you notice at next session when Claude's behavior is off.

**v0.2+ planned:** a lightweight validator — a script that reads your identity files, checks frontmatter schema, confirms section headers are present, flags stale `updated` dates, and reports issues. Not enforcement, advisory.

## Extending the schema

**You can add files beyond the 8.** The schema is minimal, not maximal. If your life has a dimension that doesn't fit any of the 8, add a new file:

1. Pick a name (`health-rituals.md`, `parenting-identity.md`, whatever)
2. Use the same frontmatter schema
3. Reference the new file from `me-summary.md` or `roles.md` as appropriate
4. Document it in your own `core/identity/README.md`

**What you probably don't need to add:**
- A file per project (projects are content, not identity)
- A file per person you care about (relationships are content, identity is how you relate in general)
- A file for temporary states (moods, current focus — those go in memory or TODO)

If you find yourself wanting to add many new files, reconsider — probably one existing file needs expansion rather than a new file.
