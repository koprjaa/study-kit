# Diplomka na FIS VŠE — Claude Code kit

Fork [study-kit](https://github.com/josefslerka/study-kit) Josefa Šlerky,
adaptovaný z literárněvědné studie na **závěrečné práce na FIS VŠE**
(informatika, datová analytika, statistika, BI, informační systémy…).

Reprodukovatelný pipeline, ve kterém tě Claude Code provede psaním diplomky —
od surového nápadu k hotové, ve výsledcích a literatuře ukotvené práci v LaTeXu.
Autorem a tím, kdo ručí za pravdivost před komisí, zůstává člověk. Postaveno na
LLM-wiki vzoru Andreje Karpathyho (neměnné syrové zdroje → odvozené artefakty,
grounding, provenience, nepřátelský posudek).

**Kit je v adresáři [`cs/`](cs/README.md)** — kompletní projekt: `CLAUDE.md`
(mozek s fakultními kritérii FIS), slash příkazy a složky. Zkopíruj, vyplň
`idea.md`, spusť `claude`.

Hlavní odchylky od originálu:

- `raw_primary/` = **vlastní artefakty** (data, logy experimentů, metriky,
  transkripty) místo literárního korpusu; `raw_secondary/` = literatura
- citace **APA 7** přes biblatex-apa, výstup **LaTeX kapitoly** do fakultní šablony
- nová fáze `/metodika` (data, baseline, metriky, hrozby validity, povinná
  validace u DP), `/reserse` s rešeršním protokolem (SLR)
- **fakultní kritéria obhajitelnosti FIS** zadrátovaná v quality gates
- `/review` cílí na věrnost čísel, cherry-picking a férovost srovnání;
  `/oponent` přidává otázky k obhajobě

**Nekomituj svůj korpus.** `raw_primary/` a `raw_secondary/` jsou git-ignored:
vlastní data a literatura pod copyrightem patří jen na lokální disk.

---

Původní workflow: Josef Šlerka, „AI-Assisted Academic Writing Pipeline"
(jaro 2026). Adaptujte volně.

**Licence:** [MIT](LICENSE) © 2026 Josef Šlerka (originál) / adaptace pro FIS VŠE.
