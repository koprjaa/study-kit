---
description: Integrity check — provenance, verbatim quotes, gates
---
Go through `process/` and `study/` and report (as a checklist, do NOT auto-fix anything that
changes meaning):
- does EVERY footnote in `study/` carry an anchor phrase + location? (A bare "Ibid." may refer
  only to a note that itself has an anchor phrase — provenance is an output artifact, not just an
  in-process check; rule 3.)
- does every quote/claim about the text have provenance into `raw_primary/`?
- do quotes match `raw_primary/` VERBATIM and CONTIGUOUSLY? (spot-check; reordering, spliced
  sentences, undefended ellipses)
- does any claim stand on a repeated word without a frequency check?
- does any synthetic core joint stand only on word-match, not on a concept? (rule 8)
- is any secondary position carrying an attributed claim through mere word-match, not in
  context? (rule 1, two-layer verification)
- is any thesis "rescued" by turning its counter-example into confirmation? (rule 8b)
- did all the quality gates from CLAUDE.md pass?
- is any section built on a single quote?
- any slide from characters to author, to labeling, or to a register outside the target journal?
- is every developed passage interpretive work over the evidence (turns the quote, defines,
  meets an objection), not padding (restatement/decoration) or mortar without a brick (asserting
  past the evidence)?
Propose fixes, but leave the decision to the human.
