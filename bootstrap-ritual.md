# Bootstrap Ritual

**How to go from zero identity files to a populated starting point in 90-120 minutes.**

> **Read this before running the bootstrap.** The ritual has three parts: a structured interview (required), optional ingest of existing writing, and iterate-from-use protocol (ongoing). You can skip ingest and still get a working identity. You cannot skip the interview or iterate-from-use — they are the core.

---

## Why "ritual" and not "wizard"

"Wizard" suggests a linear setup process that completes in one session. Atlas Seed bootstrap is not that. It's a **ritual** — a repeatable, deliberate practice that happens once at the start (interview), optionally enriches from history (ingest), and then continues forever (iterate). It's more like moving into a new home than installing software.

You don't finish the ritual. You start it, and then you live in it.

---

## Prerequisites

Before running the bootstrap, verify:

1. **You have a working Claude Code session** (or equivalent AI environment that meets the substrate requirements in `walk-up-chain.md`)
2. **You have a location for identity files** (`~/Atlas/core/identity/` in reference, or your substrate equivalent)
3. **You have 90-120 minutes** without interruption for the interview part. This is not a 10-minute task.
4. **You have read `README.md` and at least skimmed `identity-schema.md`** — so you know what you're producing
5. **You're in a state to do reflective work** — not exhausted, not rushed, not distracted by a crisis. Identity work needs presence.
6. **Git is set up** in the location where identity files will live — every draft gets committed, rollback is `git reset`

If any of these are missing, fix them before starting. The ritual is not forgiving of a broken substrate or a distracted operator.

---

## Part 1 — The Interview (required, 90-120 minutes)

The interview is a structured conversation with Claude covering each of the eight identity dimensions. You talk, Claude listens and synthesizes, Claude proposes drafts for each file based on your answers. You refine, you approve, Claude writes the files to disk.

### How to start

In your configured environment, open a Claude Code session. Say:

> *"Run the Atlas Seed bootstrap interview."*

Or, if you want to give Claude explicit context:

> *"I want to populate my Atlas Seed identity layer. I've read the README and identity-schema. Run the bootstrap interview with me."*

Claude should respond by acknowledging the task and starting with a brief framing: *"This will take about 90-120 minutes. I'll ask questions covering eight dimensions of who you are. At the end, I'll draft files for each dimension. You approve before anything gets written. Ready?"*

If Claude starts writing files immediately or asks you to fill in a form, stop. That's not the right mode. The ritual is a conversation, not a template.

### The eight sections

Claude walks through each identity dimension in approximately this order, though the order can vary based on what the conversation surfaces:

#### Section 1 — Soul (constitution)

*Goal:* identify the 5-8 principles that anchor who you are.

Typical questions:

- *"What are the non-negotiables in how you live and work? The things you'd refuse to compromise on even when it's costly."*
- *"Describe a decision you made recently that felt aligned. What principle was underneath it?"*
- *"Describe a decision you made recently that felt off. What principle was it violating?"*
- *"What do you wish other people understood about how you operate?"*

Claude listens for patterns, proposes 5-8 principles, shows you the list, asks you to refine. This section takes 20-30 minutes if done well. Don't rush. The Soul is the file that changes least and matters most.

**What you're producing:** the content for `SOUL.md`. One paragraph of identity statement, 5-8 principles with short elaborations.

#### Section 2 — Roles

*Goal:* identify the different modes you operate in and what triggers each.

Typical questions:

- *"What roles or 'hats' do you wear? Not job titles — modes."*
- *"When you sit down to work, how do you know what kind of work this is? What tells you which mode to be in?"*
- *"Which of these modes are 'me and AI observe together' vs 'AI recommends and I decide' vs 'AI can act on my behalf'?"*
- *"Is there a mode you wish you could delegate entirely? A mode you'd never delegate?"*

Claude proposes 3-6 roles with triggers, outputs, and autonomy tiers. You refine.

**Trap to avoid:** listing job titles. "I'm a product manager" is not a role in Atlas Seed sense. "When a new spec lands, I go into research mode to understand user impact before design mode" — that's two roles with clear triggers.

**What you're producing:** the content for `roles.md`. 3-6 role blocks with disposition/triggers/output/autonomy.

#### Section 3 — Life Capitals (resource framework)

*Goal:* identify the dimensions of life you invest in.

Typical questions:

- *"What are the 'accounts' in your life that you invest in — that you'd notice if they were depleted?"*
- *"Which ones get automatic attention, and which do you have to force yourself to attend to?"*
- *"How do you notice when one of these dimensions is off?"*

Claude proposes a framework. The reference is 6 capitals (Physical / Financial / Social / Intellectual / Emotional / Spiritual) but you may end up with a different decomposition — your life might have 4 dimensions or 8. The goal is fit, not conformity.

**Trap to avoid:** treating this as a time-tracking exercise. Capitals are resources, not schedules. "I need to spend 2 hours on Physical every day" is a schedule claim, not a capital claim. Capitals are about investment and depletion, not about minutes.

**What you're producing:** the content for `life-capitals.md`. Framework description, one section per capital, pattern section linking to concrete Areas.

#### Section 4 — Life Compass (values + principles)

*Goal:* identify your values and the principles you use to navigate when capitals conflict.

Typical questions:

- *"When two things you care about conflict, how do you decide?"*
- *"What's a principle you've learned the hard way and now always apply?"*
- *"What values would you refuse to trade off even for significant reward?"*

Claude proposes a list of values (5-12) and accumulated principles. You refine.

**What you're producing:** the content for `life-compass.md`. Purpose, Vision, Values list, Principles list.

#### Section 5 — Psychometrics (optional)

*Goal:* integrate formal self-knowledge assessments if you have them.

Claude asks: *"Have you taken CliftonStrengths, Hogan, Big Five, or any other formal assessment? Do you want your AI to know the results?"*

If yes, Claude asks you to share or describe the results and proposes a compressed summary. If no, Claude skips this file entirely and notes in its log that the file is absent.

**Trap to avoid:** treating this as a marketing exercise. Include derailers, blind spots, anti-talents alongside strengths. Your AI needs the full picture, not the LinkedIn version.

**What you're producing (optional):** the content for `psychometrics-summary.md`. Top-line results + your synthesis of what they imply.

#### Section 6 — Me Summary (compression)

*Goal:* produce a one-page compressed self-portrait that loads in every session.

Claude will compress everything discussed so far into ~30-50 lines. Your job is to refine it.

Typical refinement questions:

- *"Does this sound like you, or does it sound like me trying to describe you?"*
- *"What's missing that feels important?"*
- *"What's here that feels performative or aspirational?"*

**What you're producing:** the content for `me-summary.md`. Compact, honest, loadable.

#### Section 7 — Working Style (AI interaction protocol)

*Goal:* identify how you want to work with your AI — tone, preferences, anti-patterns.

Typical questions:

- *"What tone do you want me to use? Formal, casual, ironic, blunt?"*
- *"Is sarcasm a working language between us, or does it get in the way?"*
- *"When I disagree with you, how should I disagree? Diplomatic, or direct?"*
- *"What makes a session with me feel like a waste of time?"*

Claude proposes a draft based on your answers. This file will evolve fastest — don't try to get it perfect. Get it reasonable, plan to iterate.

**What you're producing:** the content for `working-style.md`. About you, AI limitations, what makes sessions productive.

#### Section 8 — Complementarity (user ↔ AI map)

*Goal:* map where you and AI complement each other.

This is often the hardest section because it requires both self-knowledge and AI-knowledge. Claude typically drives this section: *"Based on what you've told me, here's where I see us complementing each other in three modes: Compensation, Amplification, Enablement. Let me walk through each."*

You refine each row. Mark the file as `status: draft` — it will evolve fastest.

**What you're producing:** the content for `complementarity.md`. Three tables (compensation, amplification, enablement) plus a "you enable me" section.

### End of interview

After all eight sections, Claude shows you a summary: "Here are the eight files ready to write. Review each one. I'll write them to disk only after you approve each file individually."

Review each file. Check:

- Does this sound like *you* or like *a description of you*?
- Are there things that are performative (written for an audience) vs. honest (written for working use)?
- Are there omissions that feel load-bearing?
- Is there jargon you don't actually use?

Approve each file. Claude writes to disk, commits to git with message `bootstrap: initial identity layer`. Session ends.

**Total time:** 90-120 minutes for most adopters. Longer for people who want to think carefully about each section. Shorter for people with substantial prior self-knowledge work.

### What if I can't finish in one session?

The bootstrap is designed for one session because continuity matters — you're in a reflective state, Claude has fresh context, the synthesis works better when it's one arc. But if you need to pause:

- Finish the current section before stopping
- Commit whatever is written so far to git
- Note which section you were in
- Resume within 24-48 hours so context is fresh

Don't let the bootstrap drag over a week. Long pauses between sections produce inconsistent identity files because you're in different states at different sessions.

---

## Part 2 — Ingest (optional, parallel to interview)

If you have existing writing that represents you — blog posts, journals, letters, notes, published work — you can use ingest to give Claude a head start on the interview. Instead of asking you everything from scratch, Claude reads your writing, proposes draft identity files based on inferred patterns, and the interview becomes a refinement pass rather than a cold start.

### When to use ingest

- You have 10+ pieces of substantial writing from the last 2-3 years
- The writing is representative of how you actually think (not ghost-written, not heavily edited by others)
- You're comfortable letting Claude read it
- You'd rather refine drafts than generate from blank pages

### When to skip ingest

- Your existing writing is performative, edited for audience, or inauthentic
- You're early-career and don't have a corpus
- You want the identity files to capture who you are *now*, not who you were when you wrote those pieces
- You find blank-page interviews more generative than refinement

**Default recommendation:** skip ingest for alpha v0.1. The ingest pipeline is less mature than the interview. Come back to it in v0.2 when we have a tested implementation.

### How ingest works (when shipped)

The ingest pipeline reuses [Mnemon](https://github.com/dkushnikov/mnemon)'s capture pattern — the same infrastructure that processes external knowledge sources.

1. **Collect sources.** Put your writing in a folder: blog posts as markdown or text, journals as dated files, letters as individual files, etc.
2. **Run ingest.** `atlas-seed ingest <path>` (planned command for v0.2; v0.1 uses manual invocation in a Claude session)
3. **Claude reads the corpus.** For each source, Claude notes patterns, values expressed, recurring themes, tone indicators, principles invoked.
4. **Claude proposes drafts.** Based on the corpus, Claude drafts identity files. These are *proposals*, not finished files.
5. **You enter interview mode with drafts loaded.** The interview becomes a refinement conversation: *"I noticed this pattern — does this match how you see yourself?"*

### Ingest caveats

- **Claude's inference from writing is lossy.** You wrote a post in 2023 — it reflected who you were then, not who you are now. Don't treat inferred drafts as authoritative.
- **Performative writing distorts ingest.** Content written to impress or persuade doesn't represent your working self. Filter accordingly.
- **The ingest pipeline is v0.2 scope.** In v0.1 alpha, ingest is conceptual — you can manually paste writing into the interview session and ask Claude to synthesize, but there's no dedicated tooling yet.

### Mnemon compatibility

The ingest pattern mirrors Mnemon's source capture:

| Mnemon | Atlas Seed ingest |
|--------|-------------------|
| Captures external sources | Captures self-authored sources |
| Extracts via reader-context | Extracts via identity-candidate framing |
| Output: structured knowledge entries | Output: draft identity files |
| Consumer: vault | Consumer: identity layer |

Same pipeline, different target corpus. When Atlas Seed v0.2 ships the ingest script, it will reuse Mnemon infrastructure rather than building from scratch.

---

## Part 3 — Iterate from Use (ongoing, starts day 1)

The bootstrap ritual doesn't end when the interview ends. It begins.

The third part of the ritual is **iterate from use**: the protocol for refining identity files when you notice them being wrong in practice.

### The pattern

> *"The best edits come from noticing when the AI gets something wrong."*

Concretely:

1. **Claude writes something in your voice and it feels off.** → Open `working-style.md` and fix the thing that produced the mismatch.
2. **Claude misremembers what matters to you.** → Open `life-capitals.md` or `life-compass.md` and correct the weight or framing.
3. **A role trigger fires at the wrong time.** → Open `roles.md` and tighten the trigger condition.
4. **Claude pushes back when it shouldn't** (or fails to push back when it should). → Open `SOUL.md` and re-read the relevant principle. If the principle is right, the problem is elsewhere; if the principle is wrong, update it (with deliberation).
5. **You read `me-summary.md` and feel mild embarrassment.** → Fix it. That embarrassment is signal. Either the file is inaccurate or you've drifted.

### When to iterate (and when not to)

**Iterate when:**

- A specific interaction revealed a specific misalignment
- You can name what was wrong and what would be right
- The fix improves the file, not just adds to it

**Don't iterate when:**

- You're in a bad mood and want to rewrite SOUL.md in anger
- You're responding to a single frustration without thinking about the pattern
- You want to add aspirations rather than fix descriptions
- You're editing in a different voice than you normally write in (tired, jetlagged, under pressure)

**Rule of thumb:** if you'd be embarrassed to show the edit to yourself in a week, don't make it today.

### Git as time machine

Every identity file lives under git. Every edit is committed. You can always see how your identity files evolved — and if an edit turns out to be wrong, you can revert.

Recommended commit message patterns:

- `identity: refine working-style push-back section after frustrating session`
- `identity: update SOUL.md principle 3 — corrected after reflection`
- `identity: deprecate old psychometrics interpretation, add new Clifton reading`

The commit log becomes an artifact in itself — a record of how your self-understanding evolved.

### Don't over-iterate

New adopters often over-edit in the first two weeks, then stabilize. This is normal. The ritual is self-correcting: once the files are close enough, friction drops, and you stop noticing them until something shifts significantly.

**Expected iteration frequency:**

- **First two weeks:** edits daily or every other day. Fine-tuning.
- **First month:** edits every few days. Still settling.
- **Months 2-3:** edits weekly or less. The files are stable.
- **After month 3:** edits triggered by significant events (new job, major life change, new assessment, role shift). Ambient friction low.

If you're still editing SOUL.md daily at month 4, either life is genuinely shifting fast, or you're over-editing. Take a week off and see if the need is still there.

---

## Pitfalls and anti-patterns

### Bootstrap anti-patterns

**Running the interview when you're exhausted.** You'll produce files that sound tired. Identity work needs presence. Wait for a morning or a calm evening.

**Trying to get every file perfect in one session.** Bootstrap produces a starting point, not a final draft. Iterate from use handles the rest.

**Asking Claude to write identity files without a conversation.** This fails — Claude generates plausible but generic content. The interview structure matters.

**Copy-pasting identity files from someone else's setup.** Tempting shortcut, guaranteed failure. Identity is personal. Someone else's identity produces someone else's behavior from your AI.

**Treating bootstrap as one-time.** The iterate-from-use phase is where value compounds. Skipping it because "I already did bootstrap" wastes most of the benefit.

### Iterate-from-use anti-patterns

**Editing when emotional.** Bad state produces bad edits. Wait.

**Adding more, never removing.** Identity files should stay compact. If you're only adding, you're diluting.

**Chasing the AI's output instead of your own voice.** If you edit `working-style.md` because Claude produced a style you liked, you're rewriting yourself to match the AI. Reverse the direction — edit to make the AI match you.

**Skipping commits.** Every edit should be committed. Without git, you lose the evolution history and the rollback safety.

---

## Expected timeline

| Milestone | When |
|-----------|------|
| Bootstrap interview complete | Day 0 (90-120 minutes) |
| First iterate-from-use edit | Day 1-3 |
| First time identity feels "settled" | Week 2-3 |
| First time identity catches a misalignment you wouldn't have caught manually | Month 1-2 |
| First schema version bump from adopter feedback | v0.2 release (TBD) |
| First major identity shift requiring SOUL.md revision | Life-dependent — months to years |

The curve is not linear. Bootstrap is frontloaded. The payoff is compound — each week of use makes the identity layer more useful, up to a plateau around month 2-3.

---

## What you get at the end

After a complete bootstrap (interview + optional ingest) and first week of iterate-from-use, you have:

- **8 identity files** in `core/identity/` with provenance frontmatter
- **Git history** showing bootstrap + early refinements
- **A working loading mechanism** via walk-up chain so every session has identity available
- **A starting point** for the iterate-from-use phase

What you do NOT have:

- A finished, final, never-changes identity — that's not the goal
- Perfect self-knowledge — that's not achievable through a file
- A replacement for therapy, coaching, or reflective journaling — identity files are working artifacts, not tools for self-discovery

**The files are yours. Use them. Refine them. Never let them stagnate.**
