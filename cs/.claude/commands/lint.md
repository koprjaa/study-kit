---
description: Kontrola integrity — čísla vs. artefakty, citace vs. zdroje, APA 7, gates
---
Projdi `process/` a `study/` a nahlas (jako checklist, NEopravuj automaticky to,
co mění význam):
- má každé číslo ve `study/` mapování v `process/evidence.md` (artefakt + kotva)?
  (Provenance je výstupní artefakt, ne jen ověření v průběhu; pravidlo 3.)
- uvádí každá tabulka/graf zdrojový artefakt z `raw_primary/`?
- sedí čísla napříč abstraktem, textem a tabulkami? (strojově, grep — drift čísel)
- pochází každé číslo z běhu, o kterém text tvrdí, že mluví? (config, dataset,
  split — žádné frankentabulky; pravidlo 1)
- existuje každý citovaný zdroj v `raw_secondary/` A v `process/literatura.md`?
  sedí formát APA 7 (text i seznam)? nejsou v seznamu položky, které text necituje?
- nesedí některá připsaná pozice jen na shodě slov mimo kontext? (dvouvrstvé
  ověření; pravidlo 1)
- stojí nějaké tvrzení na jediném běhu bez přiznání? (pravidlo 9)
- stojí nějaký syntetický spoj jen na shodě slov/metrik, ne na férovém srovnání?
  je kauzalita značená? (pravidlo 8)
- je nějaký negativní výsledek „zachráněn" post-hoc příběhem? (pravidlo 8b)
- jednotky a zaokrouhlování konzistentní? (zaokrouhlení nesmí otočit srovnání)
- prošly všechny quality gates z CLAUDE.md?
- cyrilské homoglyfy v české sazbě? (strojová kontrola znaků)
Navrhni opravy, ale rozhodnutí nech na člověku.
