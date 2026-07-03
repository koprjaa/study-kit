# Diplomová práce (informatika · AI · BI) — Claude Code kit

*Adaptace [study-kit](https://github.com/josefslerka/study-kit) Josefa Šlerky
z literárněvědné studie na technickou diplomku (APA 7).*

Napiš diplomovou práci tak, že tě Claude Code provede celým procesem od surového
nápadu k hotovému textu. `raw_primary/` jsou tvoje vlastní artefakty (data, logy
experimentů, výsledky), `raw_secondary/` je literatura — Claude z nich čte přímo
a každé číslo i citaci ověřuje proti zdroji.

## Co je uvnitř

```
CLAUDE.md            Metoda + pravidla + chování průvodce. Mozek kitu. Jediná konfigurace.
idea.md              Zárodek: vhled/otázka, oficiální zadání, fakulta, norma, rozsah.
raw_primary/         Vlastní artefakty: data, logy běhů, exporty metrik, výstupy měření.
                     Append-only — nové běhy = nové soubory, existující se needitují.
raw_secondary/       Literatura (papery, dokumentace). NEMĚNNÁ. Jediný zdroj citací.
process/             Pracovní artefakty (teze, reserse, metodika, evidence, posudek…).
study/               Hotová práce po kapitolách (01-uvod.md, …). Výsledný produkt.
log.md               Stav + audit. Claude to čte na startu, ví, kde jste skončili.
.claude/commands/    Slash příkazy pro každou fázi.
```

## Rozjezd (5 minut)

1. **Zkopíruj složku** do nového projektu, přejmenuj podle tématu.
2. **Vlož artefakty do `raw_primary/`** (logy, CSV s metrikami, výstupy notebooků…)
   a literaturu do `raw_secondary/` — obojí může zpočátku být skoro prázdné,
   artefakty přibývají s experimenty.
3. **Vyplň `idea.md`** — vhled, oficiální zadání, fakulta + šablona, rozsah.
4. **Spusť Claude Code ve složce:** `claude`. Načte `CLAUDE.md` automaticky.
5. **Napiš `/teze`** (nebo jen „začni"). Claude tě povede fázi po fázi,
   u každého rozhodnutí se zeptá, u každého gate počká.

## Fáze = slash příkazy

| Příkaz | Fáze |
|---|---|
| `/teze` | Krystalizace + stresový test výzkumné otázky (Blok A) |
| `/kostra` | Struktura kapitol dle zadání a šablony fakulty (2.1–2.2) |
| `/metodika` | Data, baseline, metriky, protokol, hrozby validity (2.3) |
| `/uvod` | Design úvodu (2.4) |
| `/reserse` | Ingest literatury z `raw_secondary/` + APA 7 seznam |
| `/evidence` | Mapa tvrzení → artefakt + analytická hloubka (2.5 + 3.1) |
| `/prechody` | Přechody mezi kapitolami (3.2) |
| `/draft` | Psaní draftu po kapitolách (3.3) |
| `/diagnostika` | Diagnostika na 5 osách (4.1) |
| `/skrty` | Škrty — vč. encyklopedických pasáží (4.2) |
| `/review` | Posudek proti `raw_primary/`: čísla, cherry-picking, spoje (4.3) |
| `/revize` | Revize dle posudku (4.4) |
| `/oponent` | Oponentura: přínos/novost/otázky k obhajobě, proti `raw_secondary/` |
| `/checklist` | Finální checklist vč. APA 7 a náležitostí fakulty (4.5) |
| `/zaver`, `/abstrakt` | Závěr, abstrakt CZ+EN |
| `/stav` | Kde jsme a co dál |
| `/lint` | Kontrola: čísla vs. artefakty, citace vs. zdroje, drift, homoglyfy |

## Pár pravidel, ať se to nerozpadne

- **Žádné číslo mimo `raw_primary/`, žádný zdroj mimo `raw_secondary/`.**
  Vymyšlená citace a „dopočítané" číslo jsou dvě nejčastější AI selhání
  v kvalifikačních pracích — kit je blokuje tvrdými pravidly.
- **Verzuj přes Git.** `git init`, privátní repo → historie, záloha, rollback.
- **Nekomituj korpus.** `raw_primary/` (vlastní data) a `raw_secondary/`
  (literatura pod copyrightem) drž lokálně — jsou v `.gitignore`.
- **Drž lidskou smyčku.** Claude generuje a ověřuje, ty rozhoduješ — a ty ručíš
  za práci před komisí. Pravidla AI-asistence si ověř na své fakultě.

---

Původní workflow: Josef Šlerka, „AI-Assisted Academic Writing Pipeline" (jaro 2026),
podle vzorce LLM-wiki (Andrej Karpathy). Adaptace pro technickou diplomku s APA 7.
