# Diplomka na FIS VŠE — Claude Code kit

*Adaptace [study-kit](https://github.com/josefslerka/study-kit) Josefa Šlerky
pro závěrečné práce na FIS VŠE (APA 7, LaTeX).*

Napiš diplomku tak, že tě Claude Code provede celým procesem od surového nápadu
k hotovému textu. `raw_primary/` jsou tvoje vlastní artefakty (data, logy
experimentů, výsledky, transkripty), `raw_secondary/` je literatura — Claude
z nich čte přímo a každé číslo i citaci ověřuje proti zdroji. Výstup jsou LaTeX
kapitoly + BibTeX, které vložíš do fakultní šablony.

## Co je uvnitř

```
CLAUDE.md            Metoda + pravidla + fakultní kritéria FIS. Mozek kitu.
idea.md              Zárodek: vhled/otázka, oficiální zadání, program, rozsah.
raw_primary/         Vlastní artefakty: data, logy běhů, metriky, transkripty.
                     Append-only — nové běhy = nové soubory, nic se needituje.
raw_secondary/       Literatura (papery, dokumentace). NEMĚNNÁ. Jediný zdroj citací.
process/             Pracovní artefakty (teze, reserse, metodika, evidence, posudek…).
study/               Hotová práce po kapitolách (01-uvod.tex, …) + literatura.bib.
log.md               Stav + audit. Claude to čte na startu, ví, kde jste skončili.
.claude/commands/    Slash příkazy pro každou fázi.
```

## Rozjezd (5 minut)

1. **Zkopíruj složku** do nového projektu, přejmenuj podle tématu.
2. **Vlož artefakty do `raw_primary/`** a literaturu do `raw_secondary/` —
   obojí může zpočátku být skoro prázdné, artefakty přibývají s experimenty.
3. **Vyplň `idea.md`** — vhled, oficiální zadání, program, rozsah.
4. **Spusť Claude Code ve složce:** `claude`. Načte `CLAUDE.md` automaticky.
5. **Napiš `/teze`** (nebo jen „začni"). Claude tě povede fázi po fázi,
   u každého rozhodnutí se zeptá, u každého gate počká.

## Fáze = slash příkazy

| Příkaz | Fáze |
|---|---|
| `/teze` | Krystalizace + stresový test výzkumné otázky (Blok A) |
| `/kostra` | Struktura kapitol logikou IMRaD, dle zadání (2.1–2.2) |
| `/metodika` | Data, baseline, metriky, protokol, validita, validace (2.3) |
| `/uvod` | Design úvodu (2.4) |
| `/reserse` | Ingest literatury + BibTeX + rešeršní protokol |
| `/evidence` | Mapa tvrzení → artefakt + analytická hloubka (2.5 + 3.1) |
| `/prechody` | Přechody mezi kapitolami (3.2) |
| `/draft` | Psaní LaTeX kapitol (3.3) |
| `/diagnostika` | Diagnostika na 5 osách (4.1) |
| `/skrty` | Škrty — vč. encyklopedických pasáží (4.2) |
| `/review` | Posudek proti `raw_primary/`: čísla, cherry-picking, spoje (4.3) |
| `/revize` | Revize dle posudku (4.4) |
| `/oponent` | Oponentura: přínos, novost, otázky k obhajobě |
| `/checklist` | Finální checklist vč. fakultních kritérií FIS (4.5) |
| `/zaver`, `/abstrakt` | Závěr, abstrakt CZ+EN |
| `/stav` | Kde jsme a co dál |
| `/lint` | Kontrola: čísla vs. artefakty, \cite vs. .bib, stylistika |

## Pár pravidel, ať se to nerozpadne

- **Žádné číslo mimo `raw_primary/`, žádný zdroj mimo `raw_secondary/`.**
  Vymyšlená citace a „dopočítané" číslo jsou dvě nejčastější AI selhání
  v kvalifikačních pracích — kit je blokuje tvrdými pravidly.
- **Fakultní kritéria FIS jsou zadrátovaná v gates** — formulace cíle, IMRaD,
  značení původní/převzaté/spekulace, povinná validace u DP, stylistika.
- **Verzuj přes Git**, privátní repo. **Nekomituj korpus** (`raw_primary/`,
  `raw_secondary/` jsou v `.gitignore` — vlastní data a literatura pod copyrightem).
- **Drž lidskou smyčku.** Claude generuje a ověřuje, ty rozhoduješ — a ty ručíš
  za práci před komisí. Použití AI musí být v souladu s pravidly VŠE.

---

Původní workflow: Josef Šlerka, „AI-Assisted Academic Writing Pipeline" (jaro 2026),
podle vzorce LLM-wiki (Andrej Karpathy). Adaptace pro FIS VŠE: APA 7, LaTeX,
fakultní kritéria obhajitelnosti.
