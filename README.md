# Academic-writing kit for Claude Code — bilingual / dvojjazyčný

> 🇨🇿 [Česky](#-česky) · 🇬🇧 [English](#-english)

---

## 🇨🇿 Česky

Reprodukovatelný pipeline, ve kterém vás AI agent (Claude Code nebo Cursor) provede psaním
odborné studie — od syrového nápadu k hotové, ve zdrojích ukotvené práci — přičemž autorem a tím,
kdo ručí za pravdivost, zůstává člověk. Postaveno na
[LLM-wiki vzoru](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) Andreje Karpathyho
(neměnné syrové zdroje → artefakty vlastněné modelem, ukotvení, doslovná provenience, brána
nepřátelské oponentury).

Tento repozitář dodává kit ve **dvou jazycích**, jako dva samostatné adresáře:

| | |
|---|---|
| **[`cs/`](cs/README.md)** | 🇨🇿 Čeština — originál, empiricky vyladěný na studii o Karlu Čapkovi |
| **[`en/`](en/README.md)** | 🇬🇧 Angličtina — překlad téhož kitu |

Vyberte si adresář, `cd` do něj a řiďte se jeho `README`. Každý adresář je kompletní projekt: má
vlastní `CLAUDE.md` (mozek), slash příkazy a složky.

> Český kit je ten, který byl mnohokrát spuštěn, rozbit a opraven — jeho pravidla jsou jizvy ze
> skutečných selhání. Anglický kit je věrný překlad téže struktury; architektura a pravidla se
> přenášejí, ale neprošel stejnou empirickou smyčkou, takže ho doladěte tím, že ho spustíte na
> reálné práci a přidáte pravidlo pokaždé, když model uklouzne.

**Nekomitujte svůj korpus.** `raw_primary/` a `raw_secondary/` jsou v obou kitech v gitignore:
primární texty a zvláště sekundární literatura bývají chráněny autorským právem. Nechte si je lokálně.

---

## 🇬🇧 English

A reproducible pipeline that has an AI agent (Claude Code or Cursor) walk you through writing a
scholarly paper — from a raw insight to a finished, source-grounded study — while a human stays the
author and the one who vouches for the truth. Built on Andrej Karpathy's
[LLM-wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) (immutable
raw sources → model-owned artifacts, grounding, verbatim provenance, a hostile-review gate).

This repo ships the kit in **two languages**, as two self-contained directories:

| | |
|---|---|
| **[`cs/`](cs/README.md)** | 🇨🇿 Czech — the original, empirically tuned on a study of Karel Čapek |
| **[`en/`](en/README.md)** | 🇬🇧 English — a translation of the same kit |

Pick a directory, `cd` into it, and follow its `README`. Each directory is a complete project: its
own `CLAUDE.md` (the brain), slash commands, and folders.

> The Czech kit is the one that was run, broken, and fixed many times — its rules are scars from
> real failures. The English kit is a faithful translation of that same structure; the architecture
> and rules transfer, but it hasn't been put through the same empirical loop, so re-tune it by
> running it on a real paper and adding a rule whenever the model slips.

**Don't commit your corpus.** `raw_primary/` and `raw_secondary/` are git-ignored in both kits:
primary texts and especially secondary literature are usually under copyright. Keep them local.

---

Workflow: Josef Šlerka, "AI-Assisted Academic Writing Pipeline" (spring 2026). Adapt freely. /
Adaptujte volně.
