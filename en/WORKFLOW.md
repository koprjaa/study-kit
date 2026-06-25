# Workflow — detailed description and the hidden commands for agents

The operational reference for the kit. It explains the whole run from insight to finished study,
and for each step shows the **hidden command** — the instruction the agent receives when you type
a slash command (`/thesis` etc.). You type `/thesis`; the agent receives a whole paragraph of
instructions that refers into `CLAUDE.md`. Hence "hidden": you see three syllables, the agent gets
the full procedure.

The hidden commands are files `.claude/commands/<name>.md`. Both Claude Code and Cursor load them
as the project's own slash commands.

---

## 1. How the whole run works (the loop)

The workflow is not batch, it's **interactive** and agent-led:

```
start session → agent reads log.md + process/ + study/ → says where we are and what's next
   ↓
you type a slash command (or let the agent propose the next one)
   ↓
agent: generates candidates → presents them → at a JUDGMENT point asks and WAITS
   ↓
you decide (thesis, risk, gate pass/fail, accept/reject)
   ↓
agent: passes the GATE → writes the artifact into process/ or study/ → adds a line to log.md
   ↓
agent proposes the next phase → (loop)
```

**Division of labor:** you own judgment (insight, choice of risk, what's true, pass/fail). The
agent owns logistics (candidates, search in `raw_primary/`, diagnostics, writing). At judgment
points the agent never decides for you — it presents and waits.

**State** is held by `log.md`. That's why the run is resumable: close it, reopen a week later, the
agent reads the log and knows where you stopped. Start any time with `/status`.

---

## 2. Setup

```
raw_primary/      primary corpus (the texts you study) — drop in, don't edit afterwards
raw_secondary/    secondary literature — fill it, or leave it empty (primary-only mode)
idea.md           raw insight + target journal + field + length — fill in
```

Then run the agent in the folder (`claude`, or open in Cursor) and type `/thesis` (or "start").
`CLAUDE.md` is loaded as instructions automatically.

---

## 3. Data flow and state

```
raw_primary/  ─┐
raw_secondary/ ┼─►  agent (driven by CLAUDE.md)  ──►  process/   (working artifacts)
idea.md       ─┘                                 └──►  study/     (the finished study)
                                                  └──►  log.md    (state + audit)
```

Everything in `process/` and `study/` is **derived and re-derivable** from the immutable `raw_*`
layers and `idea.md`. If the study drifts, delete the derived files and re-derive.

---

## 4. The pipeline step by step

For each phase: **command** · what you do · **hidden instruction** (what the agent gets, in brief)
· decision point · **GATE** · artifact.

### BLOCK A — Crystallizing the thesis

**`/thesis`** — phases 1.1 + 1.2
*You:* have a raw insight in `idea.md`. *Hidden instruction:* the agent reads `idea.md`, searches
`raw_primary/`, applies the thesis-ness test (5 conditions), presents **5 reformulations by risk
(A–E)**, recommends one for the journal. Then on the chosen thesis, 5 stress tests (scope,
structurability, "so what", uniqueness, **groundability** = is the thesis's load-bearing
vocabulary the text's own, or an imported label?). *Decision:* **the choice of thesis and risk is
yours** — the agent waits. *GATE:* the thesis meets 5 conditions + 5 tests; for imported vocabulary
a commitment is recorded to mark the interpretive move from the start. *Artifact:* `process/thesis.md`.

### BLOCK B — Architecture

**`/outline`** — phases 2.1 + 2.2
*Hidden instruction:* assesses 5 strategies (cumulative / dialectical / detective / layered /
comparative), recommends. For each section (5–7) defines function, entry condition, exit state,
evidence type, length (%). *Decision:* choice of strategy. *GATE (outline test):* remove a section
→ does the argument collapse? swap two → does the logic change? is the last section more than a
restatement of the thesis? *Artifact:* `process/outline.md`.

**`/intro`** — phase 2.3
*Hidden instruction:* 4 hook variants (hook from `raw_primary/`, not from memory), recommends the
strongest. Positioning (consensus → gap → my study), placement of the thesis, a map, tone.
Assembles an introduction draft. *Artifact:* `process/intro-drafts.md`.

**`/evidence`** — phases 2.4 + 3.1
*Hidden instruction:* for each section searches `raw_primary/`, finds 4–6 candidates **with
provenance** (file + location, verbatim), scores 1–5 (relevance, persuasiveness,
representativeness, multifunctionality, independence), picks main + supporting. **RED FLAG:** no
passage > 3 → section unsupportable; it never supplies an invented quote, it reports that the
corpus gives no support. Then 3.1: for each key quote, the depth work (paraphrase, link to thesis,
layering ≥2 of 5, transition, model paragraph, 2–3 paragraph development of load-bearing quotes).
*Artifact:* `process/evidence.md`.

### BLOCK C — Writing

**`/transitions`** — phase 3.2
*Hidden instruction:* for each section interface, 3 transition variants (logical / contrastive /
deepening), recommends the most natural; watches the reader's trajectory. *Artifact:*
`process/transitions.md`.

**`/draft`** — phase 3.3
*Hidden instruction:* from the artifacts writes the study section by section into `study/`
(`01-intro.md`…). Clean academic prose with footnotes; no meta-comments. **Verifies every quote
verbatim against `raw_primary/` before writing it; uses nothing it can't find.** *Artifacts:*
`study/NN-*.md`.

### BLOCK D — Revision and finalization

**`/diagnose`** — phase 4.1
*Hidden instruction:* goes through the draft on 5 axes (continuity, proportion, cohesion,
redundancy, unspoken assumptions), builds a prioritized list of fixes (critical/important/cosmetic)
and implements them **in a targeted way** — no wholesale rewrite. *Artifact:*
`process/diagnostics.md` + the corrected sections.

**`/cuts`** — phase 4.2
*Hidden instruction:* finds 5 kinds of surplus text (decorative, defensive, rehearsal,
encyclopedic, lost digressions), estimates the % cuttable; protects interpretive development.
*Decision:* you approve the cuts. *Artifact:* `process/cuts.md` + the cuts made.

**`/review`** — phase 4.3 — *the most important epistemic gate*
*Hidden instruction:* confronts the draft **against `raw_primary/`** as an opponent (not the other
way round). Three hard checks every time: **quote fidelity** (verbatim + contiguity), **frequency
of "proofs"** (grep), **joints, not bricks** (synthesis stands on a concept, not on word-match).
Plus the bounding of the thesis (rule 8b): is some text "rescued" by a developmental story or an
"exception that proves the rule"? Writes a review with objections and 1 most important sentence.
*Artifact:* `process/review-report.md`.

**`/revise`** — phase 4.4
*Hidden instruction:* for each objection finds material in `raw_primary/` to answer it, proposes an
edit and implements it; iterates until all MAJOR objections are resolved. *Artifact:*
`process/response.md` + the corrected sections.

**`/checklist`** — phase 4.5
*Hidden instruction:* goes through 6 categories (argument, evidence, theory, secondary literature,
formal, readability — not word count; a long sentence is fine if it carries the structure of a
thought and reads in one breath). Last test: do the 1st + last sentence of each section form a
story? *Artifact:* `process/checklist.md`.

### Bonus

**`/conclusion`** (B.1) — a conclusion that moves the reader, opens perspectives, returns to the
hook, gives a "so what", offers 3 variants of the last sentence.
**`/abstract`** (B.2) — abstract EN + CZ with 5 functions + 5–8 keywords; checks that it matches
the actual content, not the intent.
**`/opponent`** (B.3) — a referee report on contribution/novelty/fit against `raw_secondary/`, run
**after `/review`** (truth before worth). Asserts novelty only against loaded sources; where the
field is missing it admits "can't judge" and escalates to the human. *Artifact:*
`process/opponent-report.md`.

---

## 5. Support commands (outside the linear flow)

**`/status`** — the agent reads `log.md` + `process/` + `study/`, says where you are and what the
next step is. Changes nothing. Run it at the start of a session.

**`/lint`** — integrity check (as a checklist, no auto-fix): do notes carry anchor phrases (not
bare "Ibid.")? quotes verbatim and contiguous? a claim on a repeated word without a frequency
check? a synthetic joint on word-match? a thesis "rescued" by its counter-example? a section on a
single quote? a register outside the target journal? a secondary position distorted out of context?

**`/research`** — ingest a secondary source from `raw_secondary/` into `process/research.md`:
compiles the author's position (paraphrase + provenance + anchor phrase), maps agreements/conflicts
with others, marks the gap the thesis fills, recomputes originality, watches source-type balance.
Attributes only what's in the file; doesn't name a source outside `raw_secondary/`. After a few
sources it can write the positioning for the introduction.

---

## 6. Hidden-command reference (what exactly the agent gets)

The verbatim instructions the slash commands expand to. They live in `.claude/commands/`. They are
deliberately thin — the detail of the method is in `CLAUDE.md`; they only trigger a phase and
remind the gate. `CLAUDE.md` is the single source of truth; when you change the method, change it
there, not in the commands.

| Command | Triggers | Gate / key check | Output |
|---|---|---|---|
| `/status` | orientation | — | (nothing) |
| `/thesis` | 1.1 + 1.2 | 5 conditions + 5 tests (incl. groundability) | `process/thesis.md` |
| `/outline` | 2.1 + 2.2 | outline test (remove/swap a section) | `process/outline.md` |
| `/intro` | 2.3 | hook from `raw_primary/` | `process/intro-drafts.md` |
| `/evidence` | 2.4 + 3.1 | RED FLAG (passage > 3); ≥2 of 5 layers | `process/evidence.md` |
| `/transitions` | 3.2 | reader's trajectory | `process/transitions.md` |
| `/draft` | 3.3 | quote verified against `raw_primary/` | `study/NN-*.md` |
| `/diagnose` | 4.1 | 5 axes; targeted fixes | `process/diagnostics.md` |
| `/cuts` | 4.2 | 5 kinds of padding | `process/cuts.md` |
| `/review` | 4.3 | quote+contiguity, frequency, joint, bounding (8b) | `process/review-report.md` |
| `/revise` | 4.4 | major objections resolved | `process/response.md` |
| `/checklist` | 4.5 | 6 categories; story from 1st+last sentence | `process/checklist.md` |
| `/conclusion` | B.1 | a move, not a summary | `study/` (conclusion) |
| `/abstract` | B.2 | matches content, not intent; EN+CZ | `study/` (abstract) |
| `/research` | secondary lit | only what's in `raw_secondary/`; invent nothing | `process/research.md` |
| `/opponent` | contribution | novelty only vs `raw_secondary/`; admit gaps | `process/opponent-report.md` |
| `/lint` | check | provenance in the note, contiguity, joints, 8b | (checklist) |

---

## 7. Typical pass (happy path)

```
/status   →   /thesis   →   /outline   →   /intro   →   /evidence   →   /transitions
   →   /draft   →   /diagnose   →   /cuts   →   /review   →   /revise
   →   /checklist   →   /conclusion   →   /abstract
```

Secondary literature in parallel any time: fill `raw_secondary/` → `/research` (repeat as needed)
→ the positioning feeds into `/intro`; run `/opponent` after `/review` to judge contribution. Run
`/lint` before `/review` and before submission. If you lose the thread, `/status`.

---

## 8. Where you actually decide (and must not leave it to the agent)

These points are yours, and the agent should wait at them:

1. **The choice of thesis and level of risk** (`/thesis`) — no gate will hand you the nerve for
   version D/E.
2. **The choice of strategy** (`/outline`).
3. **Pass/fail at each gate** — the agent proposes, you judge.
4. **Approving cuts** (`/cuts`) and **accepting/rejecting objections** (`/revise`).
5. **What is true** — the final verbatim verification of quotes is non-transferable; the agent
   prepares it, but you vouch for it.
6. **Dialogue with scholarship** — you find and place the secondary sources; the agent won't
   invent them.
