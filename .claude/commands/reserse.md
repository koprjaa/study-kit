---
description: Ingest zdroje z raw_secondary/ do rešerše (process/reserse.md) + APA 7 seznam literatury
---
Proveď ingest literatury dle CLAUDE.md, sekce „Literatura: ingest".

Pro nový soubor v `raw_secondary/`:
1. Ověř/dopiš BIBLIOGRAFICKÁ DATA (autor, rok, název, venue, DOI). Chybí-li,
   zeptej se člověka — NIKDY nedoplňuj odhadem (uhádnutý rok = vymyšlená citace
   v malém). Přidej BibTeX položku do `study/literatura.bib` (klíč `prijmeniROK`).
2. Přečti zdroj a zkompiluj jeho POZICI (co tvrdí k tématu práce) — PARAFRÁZÍ,
   s provenance `(raw_secondary/<soubor> — „kotevní fráze")`. NECITUJ ho jako
   doklad o tvém systému, jen jako cizí pozici s atribucí.
3. DVOUVRSTVÉ OVĚŘENÍ (pravidlo 1): kotevní fráze v souboru JE, a pozice sedí
   i v KONTEXTU (dataset, podmínky, nárok). Shoda slov nestačí; překroucení cizí
   pozice je fabulace. Nejistý kontext → oslab nebo vynech.
4. Zařaď do `process/reserse.md`. Zmapuj shody a rozpory s pozicemi, co tam už jsou.
5. Vyznač MEZERU, kterou tvá práce zaplňuje (co literatura neřeší / přehlíží).
6. PŘEPOČÍTEJ ORIGINALITU: co z výzkumné otázky tenhle zdroj už zodpovídá → co
   zbývá jako vlastní příspěvek? Zapiš ten zbytek. (Zdroj, který tezi potvrzuje,
   umí novost tiše sebrat.)
7. TYP A ROVNOVÁHA: metodologický zdroj (nástroj/technika), nebo tematický
   (výzkum přímo o tvém problému)? Samé nástroje bez tematického výzkumu =
   rešerše, která se s ničím nekonfrontuje — NAHLAS disbalanci. Klíčové definice
   a pozice musí stát na recenzovaných zahraničních zdrojích, ne na blozích.
8. REŠERŠNÍ PROTOKOL: zapisuj do `process/reserse.md`, jakými klíčovými slovy,
   v jakých databázích a s jakými počty výsledků člověk hledal (ptej se ho).
   Jen s tímhle protokolem smí práce použít pojem „SLR". Navrhni citation
   chaining (koho zdroj cituje / kdo cituje jeho).
9. Připiš JEN to, co v souboru najdeš — nikdy „autor by nejspíš tvrdil". Zdroj
   mimo `raw_secondary/` vůbec nejmenuj.

Zaloguj. Po několika zdrojích nabídni, že z `reserse.md` napíšeš kapitolu Rešerše
a situování do úvodu.
