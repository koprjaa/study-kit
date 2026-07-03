# Log & stav

Append-only. Claude sem zapisuje po každé fázi a na začátku session to čte,
aby věděl, kde jsme skončili. Resumovatelnost projektu stojí na tomhle souboru.

## Stav
Fáze: — (nezačato)
Další krok: vlož artefakty do raw_primary/ a literaturu do raw_secondary/,
vyplň idea.md (vč. oficiálního zadání), pak spusť /teze

## Záznam
<!-- YYYY-MM-DD  fáze  co se rozhodlo / co vzniklo -->
2026-07-03  AI+šablona  Napojení na oficiální šablonu FIS (SablonaBP-DP):
            study/ = rozbalená šablona, kit edituje jen kapitolové soubory,
            literatura.bib, prace.tex (\include) a prohlaseniAI.tex; šablona
            gitignorována (distribuce přes intranet). AI transparentnost dle
            pravidel VŠE + citace AI dle CIKS: process/ai-log.md vedený po
            každé fázi, nový /prohlaseni generuje prohlaseniAI.tex podklady
            + přílohu o použití AI se zvýrazněným vlastním přínosem.
2026-07-03  úprava   Kit zuniverzálněn pro FIS VŠE (ne jen AI/BI), odebrána
            anglická verze (en/), CLAUDE.md zhuštěn na ~440 řádků kvůli kontextu.
            LaTeX workflow: study/ = kapitoly .tex pro \input do fakultní
            šablony, study/literatura.bib (biblatex-apa, klíč prijmeniROK),
            \parencite/\textcite, \caption+\label+\ref; /lint kontroluje
            \cite ↔ .bib obousměrně.
2026-07-03  pokyny  Zapracována fakultní kritéria FIS VŠE (Doporučení pro tvorbu
            závěrečných prací + pokyny vedoucího KIT): nová sekce „Fakultní
            kritéria" v CLAUDE.md; test formulace cíle v /teze; IMRaD + proporce
            teorie v /kostra; kroky/pracnost/povinná validace v /metodika;
            rešeršní protokol (SLR) v /reserse; stylistika + značení
            původní/převzaté/spekulace v /draft, /checklist, /lint, /oponent.
2026-07-03  adaptace  Kit adaptován z literárněvědné studie na technickou
            diplomku (informatika/AI/BI, APA 7): raw_primary/ = vlastní artefakty
            (data, logy, metriky), raw_secondary/ = literatura; přidán /metodika,
            /badani → /reserse (+ APA 7 seznam literatury); /review cílí na
            věrnost čísel, cherry-picking a férovost srovnání; /oponent přidává
            otázky k obhajobě a kontrolu splnění zadání.

## Co se osvědčilo (přenosné metodické učení)
<!-- Sem si ty i Claude zapisujte postřehy o procesu: co fungovalo, kde AI klouzalo,
     jaký gate odhalil problém. Tahle sekce je přenosná do dalších projektů. -->

<!-- Pravidla zděděná z původního (literárněvědného) kitu — jizvy z reálných běhů,
     přeložené do technického kontextu: -->
<!-- 1. Provenance je výstup, ne procesní krok — ověření čísla v tool-callu se ztratí;
     mapa tvrzení → artefakt musí skončit v process/evidence.md a u tabulek. (pravidlo 3) -->
<!-- 2. Zákaz nefalzifikovatelné záchrany — negativní výsledek se reportuje jako
     negativní, nepřevádí se post-hoc příběhem na potvrzení. (pravidlo 8b) -->
<!-- 3. Dvouvrstvé ověření literatury — fráze v souboru JE nestačí; pozice musí sedět
     i v kontextu (dataset, podmínky, nárok). Překroucení = fabulace. (pravidlo 1) -->
<!-- 4. Přepočet originality po každém zdroji — bez něj se novost tiše ztrácí
     a příspěvek se scvrkne na aplikaci. (/reserse krok 6) -->
<!-- 5. Riziko je ve spoji, ne v cihle — pravá čísla, falešná syntéza (neférové
     srovnání, korelace vydávaná za kauzalitu) je nejhorší druh chyby. (pravidlo 8) -->
<!-- 6. Nová technická pravidla: žádné frankentabulky (čísla z různých běhů jako
     jeden experiment), jeden běh není důkaz, drift čísel se kontroluje strojově. -->
