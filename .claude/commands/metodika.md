---
description: Blok B — metodika: data, baseline, metriky, protokol, hrozby validity (fáze 2.3)
---
Proveď fázi 2.3 dle CLAUDE.md. Metodika se píše PŘED experimenty, ne po nich.

Zpracuj pět částí:
- DATA: původ, licence, velikost, preprocessing, splity, známé limity a biasy.
- BASELINE: proti čemu se měří a proč je srovnání férové (stejná data, stejné podmínky).
- METRIKY: definice každé + proč zrovna ona + co NEměří.
- PROTOKOL: seedy, počty opakování, hyperparametry, prostředí (HW/SW verze).
  Postup v krocích s odhadnutelnou pracností, konkrétně (ne „analýza, syntéza");
  neprovedené kroky zřetelně označené + důvod (fakultní kritérium).
- HROZBY VALIDITY: interní (confoundy, leakage), externí (zobecnitelnost),
  konstrukční (měří metrika to, co tvrdíme?).
- VALIDACE VÝSLEDKŮ (pro DP povinná): naplánuj už teď — srovnání s literaturou,
  důkaz, strukturované rozhovory, exaktní testování/měření. Dolepená v závěru
  neobstojí.

V úsudkových bodech (volba baseline, metrik, designu) předlož varianty a nech
rozhodnutí na člověku.

GATE (reprodukovatelnost): dokázal by cizí člověk experiment z popisu zopakovat?
Má každé plánované tvrzení výsledkové kapitoly předem definované měření? Je
naplánovaná validace? Po průchodu zapiš `process/metodika.md`, zaloguj, navrhni `/uvod`.
