---
description: Ingest a secondary source from raw_secondary/ into the research map (process/research.md)
---
Run the secondary-literature ingest per CLAUDE.md, section "Secondary literature".

For a new file in `raw_secondary/`:
1. Read it and compile its POSITION (what it claims about the subject of the study) — by
   PARAPHRASE, with provenance `(raw_secondary/<file>)` and an anchor phrase for each key claim.
   Do NOT cite it as a fact about the world, only as someone's position with attribution.
2. **Two-layer verification (rule 1):** for each attributed position verify not only that the
   anchor phrase IS in the file, but that the position holds in CONTEXT — that the use does not
   distort what the author actually claims. Word-match is not enough; distorting a position is
   fabrication. Uncertain context → weaken or drop.
3. Place it in `process/research.md`. Map agreements and divergences with positions already there.
4. Mark the gap the study's thesis fills (what this literature overlooks).
5. **Recompute originality:** what of the thesis does this source already say itself → what
   remains as the author's own contribution? Write that remainder. (A source that confirms the
   thesis can quietly take its novelty.)
6. **Type and balance:** is it a theoretical lens, or a document of field consensus? When a 3rd+
   theoretical lens accrues without a single field source, REPORT the imbalance (risk of an
   "apparatus parade") — what's missing is scholarship about the subject, not another lens.
7. Attribute ONLY what you find in the file — never "the author would probably say". Don't name a
   source outside `raw_secondary/` at all.

Log it. After a few sources, offer to write the positioning for the introduction from
`research.md`.
