# Bootstrap Ritual

**Two routes into the same files: about 15 minutes for your working rules, 90–120 minutes for the full identity layer. Both continue as iterate-from-use.**

> **Read this before you run either route.** The short route needs a chat and nothing else. The full route needs an evening and a place to keep files. Neither needs Git, Obsidian or any install. Neither finishes: you start it and then live in it.

---

## Why "ritual" and not "wizard"

"Wizard" suggests a linear setup that completes in one session. This is a **ritual**: a repeatable practice that happens once at the start (rules, then optionally the interview), and then continues (every correction is one more line). More like moving into a home than installing software.

## Prerequisites, by route

| | Short route (rules) | Full route (identity) |
|---|---|---|
| Time | about 15 minutes | 90–120 minutes without interruption |
| Environment | any chat: ChatGPT, Claude, Codex, Claude Code | the same; a folder makes it easier |
| Files | none to start; one Markdown document to keep at the end | eight Markdown files; the agent writes them in a folder (Codex, Claude Code) or you save them by hand (ChatGPT) |
| Git | not needed; the version line and the corrections log are your history | recommended for a folder, not required |
| State of mind | any | rested, not rushed, not in a crisis: identity work needs presence |
| Reading | nothing | [identity-schema.md](identity-schema.md), at least skimmed |

---

## Route 1 — Working rules (short)

The prompt is in [prompts/start.md](prompts/start.md). It carries everything the assistant needs; you do not point it at this repository.

### What happens

1. **Three questions.** Your task for the next week or two, the role you expect, how you like to work. The assistant asks one at a time. You may skip any. There is no personality interview on this route.
2. **A draft of 5–7 rules.** Each rule is one observable behaviour of the assistant. The themes are the ones from the prompt: role, disagreement, facts and uncertainty, your state, the form of answers, corrections. They are themes for a conversation, not a constitution that fits everyone. Anything the assistant assumed is marked "(assumed, confirm?)".
3. **You refine and accept.** The work here is translation. "I value directness" is a value; "state a significant objection before the answer" is a rule. Push until every line says what the assistant does. The assistant does not continue until you say the text is accepted.
4. **You apply.** The assistant does the first useful piece of your task under the rules. You make one correction. The answer is one line, `rule: …`. That line goes into your document; the assistant does not keep it for you.
5. **You save.** Two artifacts: the Markdown document (the source, [templates/working-rules.md](templates/working-rules.md) shows the layout) and the short form for the assistant's settings. Where each goes, per environment: [environments.md](environments.md).

### What you produce

`working-rules.md` with a version line, three context lines, the numbered rules, the derived short form and a corrections log. Keep it where you can find it. ChatGPT does not keep it for you.

### What the short route does not do

It does not describe you. It does not read anything you did not paste. It does not apply your rules in every chat unless you put the short form where that happens, and that is a choice: custom instructions reach all chats, a Project's instructions reach one project, a folder's `AGENTS.md` reaches one folder.

---

## Route 2 — The full interview

The interview is a structured conversation covering eight dimensions of who you are. You talk, the assistant listens and synthesises, then proposes a draft for each file. You refine, you approve, the file is written. If you already have `working-rules.md`, the interview starts from it.

### How to start

**Codex or Claude Code**, in the folder where the files will live (for example `~/ai/`, with `AGENTS.md` and `CLAUDE.md` from [templates/](templates/)):

> *"Run the Atlas Seed bootstrap interview. The schema is in `<path to your atlas-seed checkout>/identity-schema.md`; the process is in `bootstrap-ritual.md` next to it. My working rules are in `working-rules.md` here; read them first. Write each file into `identity/` only after I approve it."*

**ChatGPT**: upload `identity-schema.md` to the chat, or to a Project, and paste:

> *"Run the Atlas Seed bootstrap interview using the schema in the uploaded file. My working rules are below. For each of the eight files, draft, let me refine, and when I approve print the final file as a Markdown block; I will save it myself."*

The assistant should answer with a short framing: eight dimensions, 90–120 minutes, one draft per file, nothing written before approval. If it starts writing files at once, or hands you a form to fill, stop: that is the wrong mode.

### The eight sections

The order can vary with what the conversation surfaces.

#### 1 — Soul (constitution)

*Goal:* the 5–8 principles that anchor who you are.

- *"What are the non-negotiables in how you live and work?"*
- *"Describe a recent decision that felt aligned. What principle was under it?"*
- *"Describe one that felt off. What principle did it violate?"*
- *"What do you wish other people understood about how you operate?"*

20–30 minutes if done well. The Soul changes least and matters most. **Produces:** `SOUL.md`.

#### 2 — Roles

*Goal:* the modes you operate in and what triggers each.

- *"What hats do you wear? Not job titles, modes."*
- *"How do you know which mode a piece of work needs?"*
- *"Which modes are 'we observe together', which 'you recommend, I decide', which 'you act for me'?"*

Trap: listing job titles. **Produces:** `roles.md`, 3–6 roles with triggers, output and autonomy tier.

#### 3 — Life capitals

*Goal:* the dimensions of life you invest in.

- *"What are the accounts in your life you would notice if they ran dry?"*
- *"Which get attention by themselves, which do you have to force?"*

The reference has six (Physical, Financial, Social, Intellectual, Emotional, Spiritual). Yours may have four or eight. Capitals are resources, not schedules. **Produces:** `life-capitals.md`.

#### 4 — Life compass

*Goal:* values and the principles you navigate by when capitals conflict.

- *"When two things you care about conflict, how do you decide?"*
- *"What principle did you learn the hard way?"*

**Produces:** `life-compass.md`, 5–12 values, accumulated principles.

#### 5 — Psychometrics (optional)

*"Have you taken CliftonStrengths, Hogan, Big Five or similar, and do you want the AI to know the results?"* If no, the file is skipped and the log says so. If yes, include derailers and blind spots, not the LinkedIn version. **Produces:** `psychometrics-summary.md`.

#### 6 — Me summary

The assistant compresses everything so far into 30–50 lines. You check: *"Does this sound like me, or like you describing me?"* **Produces:** `me-summary.md`, the file that loads first.

#### 7 — Working style

Start from `working-rules.md`. Add what a month of corrections taught: tone, language, what makes a session a waste of time, what the AI should be honest about regarding its own limits. **Produces:** `working-style.md`. The short rules stay the operational file; this one is their long form.

#### 8 — Complementarity

The assistant drives: *"Here is where I see us complementing each other: compensation, amplification, enablement."* You refine each row. Mark the file `status: draft`. **Produces:** `complementarity.md`.

### End of the interview

Review each draft: does it sound like you; is anything performative; is anything load-bearing missing; is there jargon you do not use. Approve files one by one. In a folder the agent writes them and, if the folder is under Git, commits with `bootstrap: initial identity layer`. In ChatGPT you save each block as a file.

### If you cannot finish in one session

Finish the current section. Save what exists. Note which section you were in. Resume within a day or two. Long pauses produce inconsistent files, because you are a different person at different times.

---

## Re-running either route

A second run must not produce a competing description of you.

1. Give the assistant the approved files first: paste the document, or name the folder. [prompts/continue.md](prompts/continue.md) has the wording.
2. Ask for **changes to these files**, shown as a before-and-after, not for new drafts.
3. Where today's answers differ from the files, both versions are shown and you say which stands.
4. Nothing global changes without your explicit choice: not `~/.codex/AGENTS.md`, not `~/.claude/CLAUDE.md`, not custom instructions.
5. If you already have personal files in `~/.claude/` or `~/.codex/` from an earlier setup, ask for a plan and a diff before anything moves. No automatic migration.

---

## Ingest (optional, by hand)

If you have writing that represents you (posts, journals, letters), you can paste it into the interview and ask the assistant to propose drafts from it. Inference from writing is lossy: a 2023 post reflects 2023. Performative writing distorts. There is no ingest tool in this repository; the earlier plan to build one on Mnemon's capture pipeline is not shipped and not promised.

---

## Iterate from use (ongoing, from day one)

The best edits come from noticing the assistant being wrong.

- The assistant writes in your voice and it feels off → `working-rules.md`, or `working-style.md` on the full route.
- It misremembers what matters to you → `life-capitals.md` or `life-compass.md`.
- A role fires at the wrong time → `roles.md`.
- It pushes back when it should not, or fails to → re-read the principle in `SOUL.md` first; if the principle is right, the problem is elsewhere.
- You read `me-summary.md` and feel mild embarrassment → fix it; that embarrassment is signal.

### The correction loop

Short route: you correct, the assistant answers `rule: …`, you paste the line into the rules, raise the version, regenerate the short form, replace it where the environment reads it. One loop, two minutes.

### When to iterate, when not to

Iterate when a specific interaction revealed a specific misalignment you can name. Do not iterate in anger, from a single frustration, to add aspirations, or in a voice that is not yours (tired, jet-lagged, under pressure). Rule of thumb: if you would be embarrassed to show the edit to yourself in a week, do not make it today.

### Versions without Git, and with

Without Git: the version line in the document and the "(rules vN)" tail of the short form are your history; the corrections log says why each line exists. With Git: commit each change (`identity: refine push-back rule after a frustrating session`). The log becomes a record of how your self-understanding moved.

### Do not over-iterate

Two weeks of daily edits, then it settles. By month three, edits come with events: a new job, a new assessment, a shift in roles. If you still edit `SOUL.md` daily at month four, take a week off and see whether the need survives.

---

## Pitfalls

**Running the interview exhausted.** You get files that sound tired. Wait for a calm hour.

**Asking for identity files without a conversation.** You get plausible generic content. The structure of the conversation is the point.

**Copying someone else's files.** Someone else's identity produces someone else's AI.

**Adding and never removing.** The files should stay compact. Only adding dilutes.

**Chasing the assistant's output.** If you rewrite your style because you liked how the assistant wrote, you are editing yourself to match the AI. Reverse it.

**Treating the rules as enforcement.** They are context. When a rule is missed, name it and sharpen the wording; do not conclude the method failed.

---

## Expected timeline

| Milestone | When |
|---|---|
| Working rules accepted, one correction folded in | Day 0, about 15 minutes |
| Rules in the place the next chat reads | Day 0, five more minutes |
| Full interview complete | an evening, when you want it |
| First edit from use | Day 1–3 |
| Rules feel settled | Week 2–3 |
| First time the rules catch something you would have missed | Month 1–2 |

---

## What you get at the end

- `working-rules.md` with a corrections log, and the short form where your environment reads it
- On the full route, up to eight identity files with provenance frontmatter
- A loading mechanism you understand, per environment ([environments.md](environments.md))
- A loop for the rest: correct, add a line, raise the version

What you do not get: a finished identity, perfect self-knowledge, or a replacement for therapy, coaching or journaling. The files are yours. Use them, refine them, never let them stagnate.
