---
description: Ingest sekundárního zdroje z raw_secondary/ do mapy bádání (process/badani.md)
---
Proveď ingest sekundární literatury dle CLAUDE.md, sekce „Sekundární literatura".

Pro nový soubor v `raw_secondary/`:
1. Přečti ho a zkompiluj jeho POZICI (co tvrdí o předmětu studie) — PARAFRÁZÍ, s provenance
   `(raw_secondary/<soubor>)` a kotevní frází u každého klíčového tvrzení. NECITUJ ho jako
   doklad o světě, jen jako cizí pozici s atribucí.
2. **Dvouvrstvé ověření (pravidlo 1):** u každé připsané pozice ověř nejen, že kotevní fráze
   v souboru JE, ale že pozice sedí i v KONTEXTU — že použití nepřekrucuje, co autor reálně
   tvrdí. Shoda slov nestačí; překroucení cizí pozice je fabulace. Nejistý kontext → oslab
   nebo vynech.
3. Zařaď do `process/badani.md`. Zmapuj shody a rozpory s pozicemi, co tam už jsou.
4. Vyznač mezeru, kterou teze studie zaplňuje (co tahle literatura přehlíží).
5. **Přepočítej originalitu:** co z teze tenhle zdroj už říká sám → co zbývá jako vlastní
   příspěvek? Zapiš ten zbytek. (Zdroj, který tezi potvrzuje, umí novost tiše sebrat.)
6. **Typ a rovnováha:** je to teoretická optika, nebo doklad konsensu oboru? Když přibývá
   3.+ teoretická čočka bez jediného oborového zdroje, NAHLAS disbalanci (riziko „přehlídky
   aparátu") — chybí bádání o předmětu, ne další čočka.
7. Připiš JEN to, co v souboru najdeš — nikdy „autor by nejspíš řekl". Zdroj mimo
   `raw_secondary/` vůbec nejmenuj.

Zaloguj. Po několika zdrojích nabídni, že z `badani.md` napíšeš situování do úvodu.
