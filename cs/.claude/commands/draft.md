---
description: Blok C — psaní draftu po kapitolách (fáze 3.3)
---
Proveď fázi 3.3 dle CLAUDE.md.

Z artefaktů (`kostra.md`, `metodika.md`, `evidence.md`, `prechody.md`,
`uvod-navrhy.md`) piš práci kapitolu po kapitole do souborů šablony ve `study/`
(`uvod.tex`, `kapNN-nazev.tex`, `zaver.tex`) — jen obsah kapitol, žádné vlastní
preambule; novou kapitolu přidej do `\include` seznamu v `prace.tex`. Nesahej
na `makra.tex`, `zacatek.tex`, `biblatex-setup.tex`, `pdf-a.tex`. Dodržuj
plánovaný rozsah. Čistý akademický
text, citace `\parencite{key}`/`\textcite{key}`, obrázky a tabulky s `\caption`
(+ zdroj), `\label` a `\ref` z textu; stylistika dle fakultních kritérií
(neosobní forma, žádný budoucí čas, citace před tečkou, zkratky/pojmy zavedené
při prvním použití); žádné meta-komentáře ve `study/`. V každé kapitole drž
rozlišení: PŮVODNÍ výsledek / PŘEVZATÝ fakt (citace) / SPEKULACE-diskuse.

DŮLEŽITÉ: každé číslo před zapsáním OVĚŘ proti `raw_primary/` (a proti správnému
běhu — config, dataset, split) a každý citační klíč proti `study/literatura.bib`
+ `raw_secondary/`. Nepoužij nic, co v artefaktech nenajdeš. Každá tabulka/graf
uvádí zdrojový artefakt. Po každé kapitole zaloguj. Po dokončení navrhni `/diagnostika`.
