---
description: Blok D — oponentský posudek z pohledu obhajoby (přínos, novost, úroveň), proti raw_secondary/
---
Napiš posudek, jaký by na práci napsal OPONENT diplomové práce. Toto NENÍ `/review`:
`/review` ověřuje, že práce je PRAVDIVÁ (integrita proti `raw_primary/`); `/oponent`
posuzuje, zda OBSTOJÍ U OBHAJOBY (přínos, novost, úroveň proti `raw_secondary/`
a nárokům na diplomku). Spouštěj AŽ PO `/review` — pravda před hodnotou.

Tvrdě odděl dvě roviny posudku:

A) CO POSOUDÍŠ SÁM (z textu práce + raw_primary/ + raw_secondary/ + zadání v idea.md):
- Splnění zadání: kryje práce všechny body oficiálního zadání?
- Triviálnost: není odpověď banální pravda, kterou nikdo nepopírá?
- Přepálení: netvrdí abstrakt/závěr víc, než experimenty ukazují? (porovnej nárok
  s doloženým — podmínky, rozptyl, počet běhů)
- Metodika: je obhajitelná, nebo reduktivní? férové baseline? přiznané hrozby validity?
- Rozsah a úroveň: sedí na nároky diplomky dané fakulty (z `idea.md`)?
- Koherence celku: drží argument jako celek? (na úrovni stavby — čísla řeší /review)
- Dialog s literaturou: vyrovnává se práce s tím, co JE v `raw_secondary/`, nebo
  zdroje ignoruje / účelově ohýbá?
- Fakultní kritéria: projdi sekci „Fakultní kritéria (FIS VŠE)" z CLAUDE.md —
  nesplněná položka = argument komise pro neobhajitelnost, tedy zásadní námitka.
  Zvlášť: značení původní/převzaté/spekulace, povinná validace výsledků,
  formulace cíle.
- OTÁZKY K OBHAJOBĚ: 3–5 otázek, které u obhajoby pravděpodobně padnou, s odhadem,
  jak na ně práce odpovídá. Vždy mezi nimi: „Čím je práce původní? Lze výsledky
  použít i jinde než v kontextu, kde vznikly?"

B) CO POSOUDÍŠ JEN PROTI `raw_secondary/` (a jinak NE):
- Novost: zaplňuje práce reálnou mezeru, nebo replikuje, co načtená literatura už říká?
- Zařazení: sedí do téhle výzkumné debaty?
ZÁSADNÍ PRAVIDLO (anti-fabulace novosti): novost a zařazení tvrď VÝHRADNĚ proti
tomu, co je v `raw_secondary/`. Kde literatura není načtená, NEHÁDEJ — napiš
výslovně: „proti načteným zdrojům je mezera X; zda ji širší výzkum už nezaplnil,
NEPOSOUDÍM — chybí zdroj". Nikdy netvrď „je to nové" bez opory; nikdy nevymýšlej,
co by v nenačteném zdroji bylo. Když na soud chybí zdroj, eskaluj na člověka
(„sem patří zdroj, sežeň ho"), ne odhad.

Když je `raw_secondary/` prázdná: rovinu B NEDĚLEJ vůbec, jen v posudku uveď, že
přínos a novost nelze posoudit bez vložené literatury — a rovinu A proveď normálně.

VÝSTUP `process/oponentura.md`: shrnutí práce (1 odstavec, věcně) · tvrzený přínos
(jak ho čteš z textu) · silné stránky · hlavní námitky (popis + co by autor musel
doplnit + tíže: zásadní/střední/drobná) · drobné připomínky · otázky k obhajobě ·
verdikt (doporučuji k obhajobě / s výhradami / nedoporučuji) · 1 nejdůležitější
věta. Zaloguj. Navrhni, co z toho řeší `/revize` a co musí člověk (typicky:
sehnat a vložit zdroj do `raw_secondary/`, doběhnout experiment).
