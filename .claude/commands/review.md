---
description: Blok D — simulovaný posudek proti raw_primary/ (fáze 4.3)
---
Proveď fázi 4.3 dle CLAUDE.md.

KLÍČOVÉ: konfrontuj draft ze `study/` PROTI artefaktům v `raw_primary/`. Draft
NEBER jako zdroj pravdy o výsledcích — tvůj výtvor nesmí validovat sám sebe.

Tvrdé kontroly proveď VŽDY a doložitelně:
- VĚRNOST ČÍSEL: každé číslo v textu najdi v artefaktu a ověř, že pochází z běhu,
  o kterém text mluví (config, dataset, split). Žádné frankentabulky (pravidlo 1).
- CHERRY-PICKING: u každého reportovaného výsledku zjisti, kolik běhů v `raw_primary/`
  existuje celkem — je reportovaný reprezentativní, nebo nejlepší z mnoha? (pravidlo 9)
- KONZISTENCE: strojově (grep) porovnej klíčová čísla napříč abstraktem, textem
  a tabulkami.
- SPOJE, NE CIHLY: u syntetických tvrzení ověř férovost srovnání (stejná data,
  podmínky) a značení kauzality — korelace není kauzalita (pravidlo 8).
- OHRANIČENÍ (8b): není negativní/nepotvrzující výsledek „zachráněn" post-hoc
  příběhem? Negativní výsledek se reportuje jako negativní.

Napiš posudek: shrnutí, původní příspěvek, silné stránky, hlavní námitky (popis +
požadavek + závažnost), drobné připomínky, verdikt, a 1 nejdůležitější větu.
U námitek ukaž, kde se draft míjí s artefakty. Zapiš `process/posudek.md`,
zaloguj, navrhni `/revize`.
