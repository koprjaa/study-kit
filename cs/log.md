# Log & stav

Append-only. Claude sem zapisuje po každé fázi a na začátku session to čte,
aby věděl, kde jsme skončili. Resumovatelnost projektu stojí na tomhle souboru.

## Stav
Fáze: — (nezačato)
Další krok: vlož primární texty do raw_primary/, vyplň idea.md, pak spusť /teze

## Záznam
<!-- YYYY-MM-DD  fáze  co se rozhodlo / co vzniklo -->

## Co se osvědčilo (přenosné metodické učení)
<!-- Sem si ty i Claude zapisujte postřehy o procesu: co fungovalo, kde AI klouzalo,
     jaký gate odhalil problém. Tahle sekce je přenosná do dalších projektů. -->

<!-- Tři pravidla doplněná z experimentů (provenance/falzifikace/ukotvitelnost): -->
<!-- 1. Provenance je výstup, ne procesní krok — Claude Code citáty ověřil v tool-callech, -->
<!--    ale do poznámek dal holé „Tamtéž"; doložitelnost se ztratila. (pravidlo 3) -->
<!-- 2. Zákaz nefalzifikovatelné záchrany — když teze nesedne na text, nepřeváděj absenci -->
<!--    na potvrzení (hrubě ani vývojovým příběhem); ohraničuj ověřením na protikladu. (8b) -->
<!-- 3. Test ukotvitelnosti teze — slovník textu vs. importovaná nálepka; rozhoduje o -->
<!--    ukotvitelnosti víc než model. (fáze 1.2) -->

<!-- Tři pravidla k /badani doplněná z reálného běhu (studie-karel-capek-05, Claude Code): -->
<!-- 1. Dvouvrstvé ověření sekundárky — fráze v souboru JE nestačí; pozice musí sedět -->
<!--    i v kontextu (Klein: splitting jako obrana vs. jako rozpad). Překroucení = fabulace. -->
<!-- 2. Přepočet originality po každém zdroji — Freud 1912 ukázal, že rozštěp matka/milenka -->
<!--    není nový; bez tohoto kroku se novost tiše ztrácí, příspěvek se scvrkne na aplikaci. -->
<!-- 3. Hlídání typu/rovnováhy zdrojů — 3.+ teoretická optika bez oborového bádání = -->
<!--    disbalance (přehlídka aparátu); chybí předmět, ne další čočka. -->

<!-- /oponent přidán: recenzentský posudek (přínos/novost/zařazení) proti raw_secondary/, -->
<!-- oddělený od /review (integrita proti raw_primary/). Běží po /review. Novost se tvrdí -->
<!-- jen proti načteným zdrojům; kde obor chybí, oponent přizná „neposoudím", neeskaluje na -->
<!-- odhad — tatáž anti-fabulace jako u citátů, přenesená na přínos. -->

<!-- Balíček „ať to dýchá" (přímost studie → interpretační hloubka): -->
<!-- 1. Hloubka 3.1 zvednuta — u nosných citátů rozvinout do 2–3 odstavců (co znamená / -->
<!--    co ne / námitka). Méně dokladů, víc řečeného. Hranice: maso KOLEM cihel, ne místo nich. -->
<!-- 2. Zrušen 40slovní strop — souvětí je v humanitní studii nástroj myšlení; hlídá se -->
<!--    čitelnost, ne délka (/checklist). -->
<!-- 3. /skrty chrání interpretaci (vata vs hloubka: přidává věta MYŠLENKU, nebo SLOVA?); -->
<!--    /lint kontroluje, že rozvinutá pasáž je interpretace, ne vata ani malta bez cihly. -->
