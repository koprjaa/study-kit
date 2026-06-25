# Literárněvědná studie — Claude Code kit

*🇨🇿 Česky · [🇬🇧 English](../en/README.md)*

Napiš akademickou studii tak, že tě Claude Code provede celým procesem od surového
vhledu k hotovému textu. Verze workflow „pipeline + artefakty + prompty" převedená do
**jednoho nástroje**: žádný NotebookLM, žádné copy-paste mezi chaty. `raw_primary/` je tvůj
primární korpus, Claude Code z něj čte přímo a hledá v něm evidenci sám.

Postaveno na vzorci LLM-wiki (raw → odvozené, neměnný zdroj, grounding, provenance).

## Co je uvnitř

```
CLAUDE.md            Metoda + pravidla + chování průvodce. Mozek kitu. Jediná konfigurace.
idea.md              Zárodek: sem napíšeš surový vhled, časopis, obor, rozsah.
raw_primary/         Primární korpus (texty, které zkoumáš). NEMĚNNÉ — Claude jen čte.
raw_secondary/       Sekundární literatura (bádání). NEMĚNNÁ. Smí být prázdná.
                     Z ní se parafrázují cizí pozice, necituje doklad o světě.
process/             Pracovní artefakty (teze, kostra, evidence, posudek…). Píše Claude.
study/               Hotová studie po sekcích (01-uvod.md, …). Výsledný produkt.
log.md               Stav + audit. Claude to čte na startu, ví, kde jste skončili.
.claude/commands/    Slash příkazy pro každou fázi.
```

## Rozjezd (5 minut)

1. **Zkopíruj složku** do nového projektu, přejmenuj podle tématu.
2. **Vlož primární texty do `raw_primary/`** (txt/md/pdf — co máš). Po vložení je needituj.
   Sekundární literaturu (Opelík, Holý…) dej do `raw_secondary/` — nebo ji nech prázdnou.
3. **Vyplň `idea.md`** — stačí surový vhled, cílový časopis, obor, rozsah.
4. **Spusť Claude Code ve složce:** `claude`. Načte `CLAUDE.md` automaticky.
5. **Napiš `/teze`** (nebo jen „začni"). Claude tě povede dál — fázi po fázi,
   u každého rozhodnutí se zeptá, u každého gate počká.

## Jak to běží

Claude pracuje jako průvodce: vygeneruje kandidáty → předloží → položí otázku
quality gate → počká na tvé rozhodnutí → zapíše artefakt → navrhne další krok.
Ty děláš úsudek (volba teze, míra rizika, co projde), Claude dělá logistiku
(hledání v korpusu, kandidáti, diagnostika, formulace).

Slash příkazy = fáze:

| Příkaz | Fáze |
|---|---|
| `/teze` | Krystalizace + stresový test teze (Blok A) |
| `/kostra` | Strategie + argumentační mapa (2.1–2.2) |
| `/uvod` | Design úvodu (2.3) |
| `/badani` | Ingest sekundární literatury z `raw_secondary/` do mapy bádání |
| `/evidence` | Výběr evidence z `raw_primary/` + analytická hloubka (2.4 + 3.1) |
| `/prechody` | Přechody mezi sekcemi (3.2) |
| `/draft` | Psaní draftu po sekcích (3.3) |
| `/diagnostika` | Diagnostika na 5 osách (4.1) |
| `/skrty` | Škrty — 5 typů nadbytečného textu (4.2) |
| `/review` | Simulovaný posudek proti `raw_primary/` (4.3) |
| `/revize` | Revize dle posudku (4.4) |
| `/oponent` | Oponentský posudek: přínos / novost / zařazení proti `raw_secondary/` (po `/review`) |
| `/checklist` | Finální checklist (4.5) |
| `/zaver`, `/abstrakt` | Bonus: závěr, abstrakt CZ+EN |
| `/stav` | Kde jsme a co dál |
| `/lint` | Kontrola: provenance, doslovnost citátů, gates |

Nemusíš je znát zpaměti — když nezadáš nic, Claude navrhne logicky další fázi.

## Proč je to lepší než dvounástrojová verze

- **Grounding zadarmo.** Claude čte `raw_primary/` přímo a každý citát ověřuje proti zdroji.
  Žádné zpaměti rekonstruované citáty — to je v `CLAUDE.md` tvrdé pravidlo.
- **Opravený uzavřený kruh u posudku.** Simulovaný posudek konfrontuje draft *proti*
  primárním textům v `raw_primary/`, nebere tvůj draft jako zdroj pravdy. AI nerecenzuje
  vlastní výstup.
- **Resumovatelné.** `log.md` drží stav. Zavřeš a za týden otevřeš — Claude ví, kde jste
  skončili. (Tohle původní pipeline neměl — každý projekt startoval od nuly.)
- **Provenance všude.** Každé tvrzení o textu ukazuje na konkrétní místo v `raw_primary/`.

## Pár pravidel, ať se to nerozpadne

- **Needituj `raw_primary/`.** Je to zdroj pravdy a záchranná cesta.
- **Verzuj přes Git.** `git init`, privátní repo → historie, záloha, rollback.
- **Drž lidskou smyčku.** Claude generuje a hledá, ty rozhoduješ. Provokativní tezi
  (verze D/E) ti žádný gate nedodá — ta odvaha zůstává na tobě.

---

Workflow: Josef Šlerka, „AI-Assisted Academic Writing Pipeline" (jaro 2026).
Převedeno do Claude Code podle vzorce LLM-wiki (Andrej Karpathy, „llm-wiki", GitHub gist, 2026: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). Uprav si jak chceš.
