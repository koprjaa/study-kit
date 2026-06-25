# Literary-Studies Paper — a Claude Code kit

*[🇨🇿 Česky](../cs/README.md) · 🇬🇧 English*

Write a scholarly paper by having Claude Code walk you through the whole process, from
a raw insight to a finished text. A "pipeline + artifacts + prompts" workflow folded into
**a single tool**: no NotebookLM, no copy-pasting between chats. `raw_primary/` is your
primary corpus; Claude Code reads it directly and finds the evidence itself.

> **Note on language.** This directory is the **fully English** kit: `CLAUDE.md`, all slash
> commands, and `WORKFLOW.md` are in English, and the slash commands use English names
> (`/thesis`, `/outline`, `/research`, …). What's *not* English is the tuning history: the kit
> was empirically refined on a Czech literary study (Karel Čapek), so the failure stories baked
> into the rules cite Czech examples. The architecture and rules transfer as-is; just re-tune by
> running it on a real paper in your language and adding a rule whenever the model slips — see
> "Adapting it" below.

Built on the LLM-wiki pattern (raw → derived, immutable source, grounding, provenance):
Andrej Karpathy, ["llm-wiki", GitHub gist, 2026](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

## What it is (and isn't)

This is **not** a "press a button, get a paper" machine. It's a division of labor: the
agent carries the **logistics** (generating candidates, searching the corpus, drafting,
diagnosing, writing its own hostile review), and you keep the **judgment** (which thesis,
how much risk, what counts as true, what you'll vouch for). The rules in `CLAUDE.md` exist
to keep a fluent, eager-to-please model **honest** — every quote is verified verbatim
against the source, the model is forbidden to cite from memory, and a simulated referee
reads the draft *against* the primary texts rather than trusting it.

Most of the rules are scars: each one was added after a real run where the model failed
(invented page numbers, spliced non-adjacent sentences into one quote, rested a claim on
mere juxtaposition). The template is, in effect, a test suite written back into the program.

## What's inside

```
CLAUDE.md            Method + rules + guide behavior. The brain. The only config.
idea.md              Seed: your raw insight, target journal, field, length.
raw_primary/         Primary corpus (the texts you study). IMMUTABLE — Claude only reads.
raw_secondary/       Secondary literature (scholarship). IMMUTABLE. May be empty.
                     Used to paraphrase others' positions, never to cite facts about the world.
process/             Working artifacts (thesis, outline, evidence, review…). Claude writes.
study/               The finished paper, section by section. The deliverable.
log.md               State + audit. Claude reads it on start to know where you left off.
.claude/commands/    Slash commands, one per phase.
```

## Quick start (5 minutes)

1. **Copy the folder** into a new project, rename it after your topic.
2. **Put primary texts into `raw_primary/`** (txt/md/pdf). Don't edit them afterwards.
   Put secondary literature into `raw_secondary/` — or leave it empty (primary-only mode).
3. **Fill in `idea.md`** — a raw insight, target journal, field, length is enough.
4. **Run Claude Code in the folder:** `claude`. It loads `CLAUDE.md` automatically.
5. **Type `/thesis`** (or just "start"). Claude leads you on, phase by phase — asking at every
   decision, waiting at every gate.

## How it runs

Claude works as a guide: it generates candidates → presents them → asks a quality-gate
question → waits for your decision → writes the artifact → proposes the next step. You do
the judgment (thesis choice, level of risk, what passes); Claude does the logistics
(corpus search, candidates, diagnostics, phrasing).

Slash commands = phases:

| Command | Phase |
|---|---|
| `/thesis` | Crystallize + stress-test the thesis (Block A) |
| `/outline` | Strategy + argument map (2.1–2.2) |
| `/intro` | Introduction design (2.3) |
| `/research` | Ingest secondary literature from `raw_secondary/` into a research map |
| `/evidence` | Select evidence from `raw_primary/` + analytical depth (2.4 + 3.1) |
| `/transitions` | Transitions between sections (3.2) |
| `/draft` | Draft the text section by section (3.3) |
| `/diagnose` | Diagnostics on 5 axes (4.1) |
| `/cuts` | Cuts — 5 kinds of surplus text (4.2) |
| `/review` | Simulated referee report against `raw_primary/` (4.3) |
| `/revise` | Revision per the report (4.4) |
| `/opponent` | Opponent's report: contribution / novelty / fit against `raw_secondary/` (after `/review`) |
| `/checklist` | Final checklist (4.5) |
| `/conclusion`, `/abstract` | Bonus: conclusion, abstract (EN+CZ) |
| `/status` | Where we are and what's next |
| `/lint` | Check: provenance, verbatim quotes, gates |

You don't need them by heart — if you type nothing, Claude proposes the next logical phase.

## Why a single tool beats the two-tool version

- **Grounding for free.** Claude reads `raw_primary/` directly and verifies every quote
  against the source. No quotes reconstructed from memory — that's a hard rule in `CLAUDE.md`.
- **The review loop is closed properly.** The simulated referee confronts the draft *against*
  the primary texts, it doesn't treat the draft as the source of truth. The AI doesn't
  review its own output unchecked.
- **Resumable.** `log.md` holds the state. Close it, reopen a week later — Claude knows
  where you stopped.
- **Provenance everywhere.** Every claim about the text points to a specific place in
  `raw_primary/` (an anchor phrase, not a page number — the corpus has no pagination).

## A few rules so it doesn't fall apart

- **Don't edit `raw_primary/`.** It's the source of truth and the fallback.
- **Version with Git.** `git init`, a private repo → history, backup, rollback.
- **Keep the human in the loop.** Claude generates and searches; you decide. No gate will
  hand you a provocative thesis (version D/E) — that nerve stays with you.

## Adapting it to another field

The kit is already in English; what's tuned for literary scholarship is the field-specific
wording (the test vocabulary, the example failures). To repurpose it for another field: adjust
`idea.md` (field, journal, terminology), keep the *structure* (immutable raw sources, model-owned
artifacts, grounding, verbatim verification, the hostile-review gate), and then re-tune by running
it on a real paper and adding a rule each time the model slips. The discipline is the point, not
the specific wording. (For another *language*, translate `CLAUDE.md` and `.claude/commands/*` the
way the Czech `cs/` kit was translated into this one.)

## Copyright

`raw_primary/` and `raw_secondary/` are git-ignored on purpose: **do not commit your
corpus.** Primary texts and especially secondary literature are usually under copyright;
keep them local. The repo ships with empty corpus folders.

---

Workflow: Josef Šlerka, "AI-Assisted Academic Writing Pipeline" (spring 2026).
Ported to Claude Code following the LLM-wiki pattern (Andrej Karpathy, "llm-wiki", GitHub
gist, 2026). Adapt freely.
