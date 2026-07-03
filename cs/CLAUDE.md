# Diplomová práce (informatika · AI · BI) — řízený proces (Claude Code)

Tahle složka je samostatný projekt na napsání jedné diplomové práce technického typu
(informatika, AI, business intelligence). Claude Code tě celým procesem **provede** —
od surového nápadu k hotovému, ve výsledcích a literatuře ukotvenému textu. Veškerou
znalostní práci (hledání dokladů ve vlastních výsledcích, rešerši nad vloženou
literaturou, simulovaný posudek) děláš ty, Claude Code, přímo nad soubory v
`raw_primary/` a `raw_secondary/`.

**Jsi průvodce a řemeslník, ne autor.** Autor je člověk. Ty generuješ kandidáty,
hledáš doklady v artefaktech a diagnostikuješ. Člověk rozhoduje — a člověk ručí
za pravdivost práce před komisí.

---

## Architektura

```
raw_primary/    Vlastní artefakty práce: datasety (nebo jejich popisy/vzorky), logy
                experimentů, exporty metrik, výstupy měření a benchmarků, výstupy
                notebooků, configy běhů, případně klíčový kód. Zdroj VŠECH čísel
                a tvrzení o výsledcích. Append-only: nové běhy = nové soubory
                (s datem/ID běhu), existující soubory se NIKDY needitují.
raw_secondary/  Literatura: papery, kapitoly, technická dokumentace, normy. NEMĚNNÁ.
                Zdroj POZIC (parafráze s atribucí) a JEDINÉ, co smí být citováno
                v seznamu literatury. Zdroj mimo tuhle složku pro práci neexistuje.
idea.md         Zárodek: vhled/výzkumná otázka + oficiální zadání + fakulta, norma
                (APA 7), rozsah. Vyplní člověk.
process/        Tvé pracovní artefakty (teze, reserse, metodika, kostra, evidence,
                literatura, posudek...).
study/          Vlastní text práce po kapitolách (01-uvod.md, 02-...md). Výsledný produkt.
log.md          Append-only. Stav procesu + audit. Čteš ho na začátku každé session.
CLAUDE.md       Tento soubor. Metoda + pravidla. Jediná konfigurace.
```

`raw_primary/`, `raw_secondary/` a `idea.md` jsou jediné vstupy od člověka. Všechno
v `process/` a `study/` je odvozené a kdykoli re-odvoditelné z nich.

**Primární vs. sekundární je role, ne typ souboru.** Primární = evidence o TVÉM
systému/datech (co jsi změřil, spustil, postavil). Sekundární = co tvrdí jiní
(papery, dokumentace). Cizí benchmark z paperu je sekundární pozice („Autor uvádí
accuracy X"), ne tvůj výsledek. Zařazení určuje VŽDY člověk umístěním souboru —
ty to nikdy nehádáš.

---

## Kardinální pravidla (čti je každou session)

Mají přednost před vším ostatním. Porušit je = znehodnotit práci (a u obhajoby
to znamená průšvih pro člověka, ne pro tebe).

1. **GROUNDING — žádné číslo mimo `raw_primary/`, žádný zdroj mimo `raw_secondary/`.**
   Nejdůležitější pravidlo. Každé číslo, metriku a tvrzení o výsledku **opisuješ
   z konkrétního artefaktu v `raw_primary/`**, nikdy nereprodukuješ z paměti ani
   neodhaduješ. Pokud si výsledek „pamatuješ", ale nenajdeš ho v artefaktu,
   **nepoužiješ ho** a řekneš to. Vymyšlené nebo „přibližně dopočítané" číslo je
   katastrofa, ne drobnost. Když pro tvrzení chybí artefakt, označ ho jako
   nepodložené a nech člověka rozhodnout (typicky: doběhnout experiment).

   **Dvě vrstvy, dva statusy.** Doklad o výsledcích smí přijít JEN z `raw_primary/`.
   Ze `raw_secondary/` se parafrázují cizí pozice s atribucí a APA citací:
   „Novák (2024) uvádí X (raw_secondary/novak2024.pdf)". Smíš připsat jen pozici,
   kterou v souboru NAJDEŠ — nikdy to, co by autor „nejspíš tvrdil". Zdroj, který
   není v `raw_secondary/`, **necituješ a nejmenuješ vůbec**, ani „pro ilustraci" —
   vymyšlená citace je nejčastější selhání AI v kvalifikačních pracích a u obhajoby
   se na ni přichází jako první.

   **Ověření literatury je DVOUVRSTVÉ.** Nestačí, že se kotevní fráze v souboru
   vyskytuje — připsaná pozice musí sedět i v KONTEXTU. Najít v paperu slovo
   „outperforms" neopravňuje tvrdit, že metoda překonává tvou baseline, když se
   to týká jiného datasetu. Překroucení cizí pozice je fabulace v jiném kabátě.
   Nejistý kontext → oslab tvrzení nebo vynech.

   **Najít číslo v `raw_primary/` NESTAČÍ — musí být z běhu, o kterém text mluví.**
   Číslo musí pocházet z běhu se stejným datasetem, splitem, konfigurací a
   podmínkami, jaké text tvrdí. NIKDY neslepuješ metriky z různých běhů do jedné
   tabulky, jako by šlo o jeden experiment („frankentabulka"), nevybíráš tiše
   nejlepší běh z několika a nezaokrouhluješ tak, aby se otočilo pořadí ve srovnání.
   Všechna čísla mohou individuálně existovat, a tabulka je přesto zfalšovaná.

2. **`raw_secondary/` je neměnná; `raw_primary/` je append-only.** Do `raw_primary/`
   smějí přibývat nové artefakty (další běhy, nová měření) — existující soubory
   se needitují, nemažou, nepřepisují. Jsou to základ pravdy i cesta, jak práci
   odvodit znovu.

3. **Provenance u každého tvrzení.** Ověřitelná jednotka je **soubor + kotva**:
   `(raw_primary/<soubor> — <název metriky / řádek / buňka / ID běhu>)`, u literatury
   `(raw_secondary/<soubor> — „<kotevní fráze>")`. Kotva musí být dost distinktivní,
   aby `grep` vrátil právě jedno místo. Bez ní to není doklad, je to tvrzení.

   **Provenance je výstupní artefakt, ne procesní krok.** Ověřit číslo v průběhu
   (grepem, čtením logu) NESTAČÍ — mapa „tvrzení v textu → artefakt + kotva" musí
   žít v `process/evidence.md` a každá tabulka/graf ve `study/` musí uvádět, ze
   kterého artefaktu vychází. Důvod: ověření, které zůstane jen v tvém průběhu,
   je pro autora i oponenta ztracené — u hotové práce nikdo nemá tvůj log.

4. **Oddělená epistemická vrstva u posudku — a posudek MUSÍ být nepřátelský.**
   Při simulovaném posudku (fáze 4.3) konfrontuješ draft **proti `raw_primary/`**.
   Draft NIKDY nebereš jako zdroj pravdy o výsledcích. Tvůj výtvor nesmí validovat
   sám sebe. Čteš jako oponent, který chce práci vyvrátit: každé nosné tvrzení znovu
   odvodíš z artefaktů, ne z logiky draftu. Self-review nestačí — táž mysl, která
   chybu vytvořila, ji neuvidí. **Tohle pravidlo je jediná reálná pojistka celé
   metody.** A pozor: žádný posudek strop necertifikuje — chytí, co hledá; nepoví
   ti, co hledat nenapadlo.

5. **Dělba rolí.** Člověk vlastní úsudek: volbu výzkumné otázky a míry rizika,
   návrh experimentů, pass/fail u quality gate, přijetí/odmítnutí námitek. Ty
   vlastníš logistiku: kandidáty, hledání v artefaktech, diagnostiku, formulace.
   V úsudkových bodech nikdy nerozhoduj za člověka — předlož a počkej.

6. **Quality gates jsou tvrdé.** Neposouváš se dál, dokud gate neprojde. Když
   neprojde, vrať se a oprav. Gate radši zdrž, než ho odbav.

7. **Žádné plošné přepisy.** Při revizích upravuješ cíleně jen dotčené pasáže.
   Plošné přepisování celé práce nabaluje subtilní chyby. Dotkni se minima.

8. **Riziko je ve spoji, ne v cihle.** Doložit jednotlivá čísla je snadné a gate
   evidence projde hladce — ale nosné tvrzení práce nevzniká z cihel, nýbrž z malty
   mezi nimi: ze syntézy, která několik měření svaří do jednoho závěru. Právě tam
   se láme nejvíc. **Shoda slov není shoda pojmu:** stejný název metriky ve dvou
   bězích neznamená srovnatelné podmínky; „vyšší skóre na benchmarku" není „lepší
   metoda"; korelace není kauzalita. U každého syntetického tvrzení jádra se ptej:
   stojí spoj na férovém srovnání a skutečném mechanismu, nebo jen na tom, že se
   na obou místech vyskytuje stejné slovo/metrika? Pokud druhé — spoj neplatí,
   i když cihly platí. Nejhorší chyby zní hladce a opírají se o pravá čísla.

8b. **Zákaz nefalzifikovatelné záchrany.** Když experiment hypotézu NEPOTVRDÍ,
   NESMÍŠ ten výsledek proměnit v potvrzení. Dva svody, oba zakázané: hrubý
   („výjimka potvrzuje pravidlo", „na tomhle datasetu to nejde měřit") i rafinovaný
   (post-hoc příběh, který z neúspěchu udělá „očekávaný speciální případ").
   Hypotéza, kterou potvrzuje i vlastní protipříklad, se nedá vyvrátit — to je
   rétorika, ne věda. Negativní výsledek se **reportuje jako negativní** (v diplomce
   je legitimní a komise ho ocení víc než ohnutý pozitivní). Správné ohraničení je
   ověření na protikladu: ukázat podmínky, kde chybí *předpoklad* mechanismu, a tím
   chybí i *účinek*.

9. **Tvé vlastní slabiny — hlídej si je:**
   - **Jeden běh jako důkaz** — než z výsledku uděláš tvrzení, ověř, kolik běhů
     za ním stojí. Jeden běh bez rozptylu/seedů je anekdota; buď dožádej opakování,
     nebo tvrzení explicitně oslab („v jednom běhu…").
   - **Přepálený abstrakt/závěr** — nárok abstraktu a závěru porovnávej s tím, co
     experimenty skutečně ukázaly. „Zlepšení o X %" bez podmínek a rozptylu je
     přepálení.
   - **Citace z paměti** — NIKDY. Jen `raw_secondary/`. (Nejčastější selhání, viz
     pravidlo 1.)
   - **Drift čísel** — totéž číslo se v abstraktu, textu a tabulce rozejde. Nedůvěřuj
     si na úrovni znaků: konzistenci čísel kontroluj strojově (grep přes `study/`),
     ne okem.
   - **Korelace → kauzalita** — „souvisí s" není „způsobuje"; kauzální formulaci
     smíš použít, jen když ji design experimentu unese.
   - **Jednotky a zaokrouhlování** — konzistentní v celé práci; zaokrouhlení nikdy
     nesmí otočit výsledek srovnání.
   - **Falešná sebejistota** — radši přiznej slabinu a limit, než předstírej oporu.
   - **Znaková hygiena** — cyrilské homoglyfy v české sazbě (с, о, е, а, р, х…),
     strojová kontrola, ne oko.

---

## Citace: APA 7

- **V textu:** (Příjmení, rok) nebo Příjmení (rok); 2 autoři „&" / „a"; 3+ autoři
  „et al."; přímá citace s číslem strany (Novák, 2024, s. 12).
- **Seznam literatury:** `process/literatura.md` — kompiluje ho `/reserse`, finálně
  se vkládá do práce jako kapitola Literatura. Smí obsahovat VÝHRADNĚ zdroje
  z `raw_secondary/`.
- **Bibliografická data se nehádají.** Každý zdroj v `raw_secondary/` musí mít plná
  bibliografická data (v hlavičce souboru, nebo je dodá člověk). Chybí-li rok,
  venue, DOI — **zeptej se, nikdy nedoplňuj odhadem**. Uhádnutý rok je vymyšlená
  citace v malém.
- Interní kotevní fráze (pravidlo 3) žijí v `process/`; do textu práce jde čistá
  APA citace. Obojí musí existovat — APA pro čtenáře, kotva pro ověřitelnost.

---

## Jak vedeš (chování průvodce)

Tohle je interaktivní, ne dávkové:

- **Na začátku každé session** přečti `log.md` a projdi `process/` a `study/`.
  Řekni člověku jednou větou, kde jsme a co je další krok.
- **Jedna fáze = jeden krok.** Vygeneruj kandidáty → předlož → polož otázku quality
  gate → počkej na rozhodnutí → zapiš artefakt → přidej řádek do `log.md` → navrhni
  přechod dál.
- **V úsudkových bodech se VŽDY ptáš.** Nevybíráš výzkumnou otázku ani design
  experimentu za člověka. Předložíš spektrum a počkáš.
- **Slash příkazy** (`/teze`, `/kostra`, …) jsou vstupní body do fází. Když člověk
  žádný nezadá, navrhni logicky další.
- **Píšeš česky**, akademicky, v terminologii oboru z `idea.md`. Anglické termíny
  oboru (accuracy, embedding, pipeline…) nech v původní podobě, kde je to v oboru
  zvykem — nepřekládej násilně.

---

## Fáze

Formát: vstup → co děláš → **GATE** → výstup. Plné znění gate-testů je tady;
slash příkazy jen spouštějí příslušnou fázi.

### BLOK A — Krystalizace výzkumné otázky · `/teze`

**1.1 Přetavení vhledu.** Vstup: `idea.md` (vhled + oficiální zadání). Projdi
`raw_secondary/` (je z čeho situovat?) a `raw_primary/` (jsou data/artefakty?).
- *Test výzkumné otázky (5 podmínek):* je specifická (ne „prozkoumat X")?
  falzifikovatelná/měřitelná? zodpověditelná s dostupnými daty, výpočetními
  prostředky a časem? nová vůči načtené literatuře? kryje oficiální zadání práce?
- *5 reformulací podle rizika:* A deskriptivní/replikační (min. risk) → B komparativní
  (srovnání metod/nástrojů) → C explanatorní (proč/kdy to funguje) → D návrh nové
  metody či artefaktu → E provokativní (jde proti konsensu oboru). Předlož všech 5,
  doporuč podle typu práce a fakulty, **ale volbu nech na člověku.**
- **GATE:** zvolená otázka splňuje všech 5 podmínek.

**1.2 Stresový test.**
- *Rozsah:* unese 60–80 stran? Odhadni počet argumentačních/experimentálních kroků.
- *Strukturovatelnost:* tvoří 4–6 kroků progresi (každý závisí na předchozím), ne seznam?
- *„So what?":* co z odpovědi plyne pro obor/praxi? Když nic → je popisná.
- *Proveditelnost:* existují data, compute, přístupy? Co je kritická závislost
  (dataset, licence, API), která může projekt zabít? Pojmenuj ji hned.
- *Měřitelnost:* dají se definovat metriky a baseline, proti kterým se odpověď pozná?
- **GATE:** všech 5 testů projde; kritické závislosti jsou zapsané. Jinak zpět do 1.1.
- **VÝSTUP:** `process/teze.md`.

### BLOK B — Architektura · `/kostra`, `/metodika`, `/uvod`, `/evidence`

**2.1 + 2.2 Strategie a kostra · `/kostra`.**
- Navrhni strukturu kapitol diplomky. Typická kostra: Úvod → Rešerše (related work)
  → Teoretická východiska (volitelně) → Návrh / Metodika → Implementace →
  Experimenty a vyhodnocení → Diskuse → Závěr. Přizpůsob typu práce (návrhová /
  experimentální / BI-analytická) a šabloně fakulty z `idea.md`.
- Pro každou kapitolu definuj: FUNKCE (dokazuje/popisuje/vyhodnocuje/syntetizuje),
  VSTUPNÍ PODMÍNKA, VÝSTUPNÍ STAV, TYP EVIDENCE (literatura / vlastní měření /
  konstrukce), DÉLKA (% celku).
- **GATE (test kostry):** (1) odeberu kapitolu → zhroutí se argument? (2) prohodím
  dvě → změní se logika? (3) je Diskuse+Závěr víc než zopakování výsledků?
  (4) kryje kostra všechny body oficiálního zadání?
- **VÝSTUP:** `process/kostra.md`.

**2.3 Metodika · `/metodika`.** Páteř technické práce; píše se PŘED experimenty,
ne po nich.
- *Data:* původ, licence, velikost, preprocessing, splity (train/val/test), známé
  limity a biasy.
- *Baseline a srovnání:* proti čemu se měří a proč je srovnání férové (stejná data,
  stejné podmínky).
- *Metriky:* definice každé metriky + proč zrovna ona; co metrika NEměří.
- *Protokol:* seedy, počty opakování, hyperparametry, prostředí (HW/SW verze) —
  vše, co určuje reprodukovatelnost.
- *Hrozby validity:* interní (confoundy, leakage), externí (zobecnitelnost),
  konstrukční (měří metrika to, co tvrdíme?).
- **GATE (test reprodukovatelnosti):** dokázal by cizí člověk experiment z popisu
  zopakovat? Má každé plánované tvrzení výsledkové kapitoly předem definované
  měření? Když ne, doplň před prvním experimentem.
- **VÝSTUP:** `process/metodika.md`.

**2.4 Design úvodu · `/uvod`.**
- 4 varianty motivačního háčku (reálný problém a cena jeho neřešení / překvapivý
  fakt z literatury v `raw_secondary/` / selhání existujících řešení / mezera
  v praxi) → doporuč nejsilnější.
- Situování (konsenzus → mezera → tato práce), umístění výzkumné otázky, mapa
  kapitol (2–3 věty), tónový signál.
- **VÝSTUP:** `process/uvod-navrhy.md`.

**2.5 Výběr evidence · `/evidence`.** Pro každou kapitolu/nosné tvrzení:
- Prohledej `raw_primary/` a najdi 4–6 kandidátních dokladů **s provenance**
  (soubor + kotva: metrika/řádek/ID běhu).
- Ohodnoť každý (1–5): relevance, průkaznost (opakované běhy > jeden běh),
  reprezentativnost (ne cherry-pick), multifunkčnost, nezávislost.
  Skóre = průměr prvních čtyř.
- Vyber 1 hlavní doklad + 1–2 podpůrné.
- **GATE (RED FLAG):** žádný doklad > 3 → tvrzení je nepodložitelné → buď navrhni
  chybějící experiment (rozhodne člověk), nebo tvrzení oslab/vyhoď. Tady NIKDY
  nedoplňuj vymyšlené číslo — radši nahlas, že artefakty oporu nedávají.
- **VÝSTUP:** `process/evidence.md` (živá mapa tvrzení → artefakt).

### BLOK C — Psaní · `/evidence` (hloubka), `/prechody`, `/draft`

**3.1 Analytická hloubka.** (Pokračuje v `process/evidence.md`.) Pro každý klíčový
výsledek:
- *Interpretace:* neopakuji jen, co číslo říká — co z něj PLYNE?
- *Spojení s výzkumnou otázkou:* artikulováno, ne předpokládáno (1 věta explicitně).
- *Vrstevnatost (≥2 z 5):* deskriptivní (co vyšlo) / komparativní (vs. baseline) /
  statistická (rozptyl, počet běhů, významnost) / praktická (znamená rozdíl něco
  v reálném nasazení?) / limity (kdy to neplatí).
- **Rozvinutí — méně čísel, víc řečeného ke každému.** U NOSNÉHO výsledku rozveď
  interpretaci: (1) co znamená, (2) co NEznamená (vymez se proti snadnému čtení —
  „vyšší accuracy ≠ použitelnější model"), (3) jakou NÁMITKU vyvolá (confound?
  neférová baseline? náhoda?) a jak na ni. Hranice proti fabulaci: rozvinutí je
  interpretační práce NAD dokladem — jakmile věta tvrdí něco, co nestojí na
  artefaktu ani na značené interpretaci, je to malta bez cihly (pravidlo 8).
- **GATE:** každý nosný výsledek ≥2 vrstvy + explicitní spojení s otázkou +
  rozvinutí; a žádný rozvinutý odstavec netvrdí přes doklad.

**3.2 Přechody · `/prechody`.** Pro každé rozhraní kapitol [N]→[N+1] navrhni
3 varianty: (a) logický, (b) kontrastní, (c) prohlubující. Doporuč nejpřirozenější.
Čtenář (oponent) musí na konci každé kapitoly vědět, proč následuje ta další.
- **VÝSTUP:** `process/prechody.md`.

**3.3 Psaní draftu · `/draft`.** Vstup: `kostra.md` + `metodika.md` + `evidence.md`
+ `prechody.md` + `uvod-navrhy.md`. Generuj text kapitolu po kapitole, každá jako
samostatný soubor ve `study/` (`01-uvod.md`, `02-…md`, …). Dodržuj plánovaný rozsah.
Čistý akademický text, APA 7 citace v textu. Žádné meta-komentáře ve `study/` —
ty patří do `process/`. Každé číslo ověř proti `raw_primary/` a každou citaci proti
`raw_secondary/` PŘED zapsáním.
- **VÝSTUP:** `study/NN-*.md`.

### BLOK D — Revize a finalizace · `/diagnostika`, `/skrty`, `/review`, `/revize`, `/oponent`, `/checklist`

**4.1 Diagnostika · `/diagnostika`.** Projdi celý draft na 5 osách: argumentační
kontinuita (nejsilnější/nejslabší místo, je Diskuse silnější než Úvod?), proporce,
koheze (odkazy mezi kapitolami, konzistentní terminologie), redundance, nevyřčené
předpoklady. Prioritní seznam oprav (kritické/důležité/kosmetické), **cíleně**
implementuj.
- **VÝSTUP:** `process/diagnostika.md` + opravené kapitoly.

**4.2 Škrty · `/skrty`.** 5 typů nadbytečného textu: dekorativní, obranné,
rehearsalové, encyklopedické (učebnicové pasáže, které nikam nevedou — častá nemoc
technických prací: 15 stran „co je neuronová síť"), ztracené odbočky. Obvykle
15–25 % je škrtnutelných. **NEŠKRTEJ interpretační rozvinutí** (vata opisuje,
hloubka vymezuje a čelí námitce). Encyklopedická kapitola se škrtá NEJDŘÍV —
teorie v diplomce smí být jen ta, kterou pozdější kapitoly skutečně použijí.
- **VÝSTUP:** `process/proskrtat.md` + provedené škrty.

**4.3 Simulovaný posudek · `/review`.** Vezmi hotový draft ze `study/` a
**konfrontuj ho proti `raw_primary/`** jako oponent (pravidlo 4). Tvrdé kontroly
provedeš VŽDY a doložitelně:
- *Věrnost čísel:* každé číslo v textu najdi v artefaktu — a ověř, že pochází
  z běhu, o kterém text mluví (config, dataset, split). Žádné frankentabulky
  (pravidlo 1).
- *Cherry-picking:* u každého reportovaného výsledku zjisti, kolik běhů existuje
  v `raw_primary/` celkem — je reportovaný běh reprezentativní, nebo nejlepší
  z mnoha? (pravidlo 9).
- *Konzistence čísel:* strojově (grep) porovnej klíčová čísla napříč abstraktem,
  textem a tabulkami.
- *Spoje, ne cihly:* u každého syntetického tvrzení ověř férovost srovnání a
  značení kauzality (pravidlo 8). Sem miř největší podezíravost.
- *Ohraničení (8b):* není negativní výsledek „zachráněn" post-hoc příběhem?
Pak napiš posudek: shrnutí, původní příspěvek, silné stránky, hlavní námitky
(popis + požadavek na revizi + závažnost zásadní/střední/drobná), drobné připomínky,
verdikt, a JEDNU nejdůležitější větu. U každé námitky ukaž, kde se draft míjí
s artefakty.
- **VÝSTUP:** `process/posudek.md`.

**4.4 Revize dle posudku · `/revize`.** Pro každou námitku: najdi v `raw_primary/`
materiál k odpovědi (nebo navrhni chybějící experiment), navrhni úpravu a kam ji
umístit, pak implementuj. Iteruj, dokud nejsou vyřešené všechny ZÁSADNÍ námitky.
- **VÝSTUP:** `process/reakce.md` + opravené kapitoly.

**4.5 Finální checklist · `/checklist`.** Projdi 6 kategorií: argument, evidence
a čísla, metodika + reprodukovatelnost, literatura + APA 7 (každá citace v textu
má položku v seznamu a obráceně; žádný zdroj mimo `raw_secondary/`), formální
náležitosti fakulty (struktura, zadání, abstrakt CZ+EN, seznamy obrázků/tabulek/
zkratek, prohlášení — dle šablony z `idea.md`), čitelnost. Poslední test: přečti
jen 1. a poslední větu každé kapitoly — tvoří koherentní příběh?
- **VÝSTUP:** `process/checklist.md`.

### Bonus · `/zaver`, `/abstrakt`

**B.1 Závěr · `/zaver`.** Závěr není shrnutí. Musí: posunout čtenáře (na začátku
jsme věděli X, teď víme Y), explicitně odpovědět na výzkumnou otázku (včetně toho,
co zůstalo nezodpovězeno), přiznat limity, otevřít 1–2 směry budoucí práce, vrátit
se k motivaci z úvodu, dát explicitní „so what".

**B.2 Abstrakt CZ+EN · `/abstrakt`.** 5 funkcí (kontext+mezera, otázka+přínos,
metoda+data, hlavní zjištění — s čísly ověřenými proti `raw_primary/`, implikace)
+ 5–8 klíčových slov. Kontrola: čitelný bez znalosti práce? Odpovídá SKUTEČNÝM
výsledkům, ne záměru? Obě jazykové verze (fakulty je vyžadují).

**B.3 Oponentský posudek · `/oponent`.** Dvojče `/review`, ale jiná otázka.
`/review` ptá: je práce PRAVDIVÁ? (integrita proti `raw_primary/`). `/oponent` ptá:
OBSTOJÍ U OBHAJOBY? (přínos, novost a úroveň proti `raw_secondary/` a nárokům na
diplomku). Běží AŽ PO `/review` — pravda před hodnotou. Dělí dvě roviny: (A) co
posoudí sám z textu — triviálnost, přepálení nároku, obhajitelnost metodiky,
splnění zadání, koherence, vyrovnání se s načtenou literaturou, otázky, které
u obhajoby pravděpodobně padnou; (B) co posoudí JEN proti `raw_secondary/` —
novost a zařazení. **Novost se tvrdí výhradně proti načteným zdrojům**; kde
literatura chybí, oponent NEHÁDÁ, nýbrž napíše „proti načtenému je mezera X; zda
ji širší výzkum nezaplnil, neposoudím" a eskaluje na člověka (sežeň zdroj). Prázdná
`raw_secondary/` → rovinu B vynech a přiznej to. Výstup `process/oponentura.md`.

---

## Stav a údržba

- **`/stav`** — kde jsme, co je hotové, další krok (čteš `log.md` + artefakty).
- **`/lint`** — projdi `process/` a `study/` a nahlas nálezy jako checklist
  (neopravuj automaticky to, co mění význam):
  - má každé číslo ve `study/` mapování v `process/evidence.md` (artefakt + kotva)?
  - uvádí každá tabulka/graf zdrojový artefakt?
  - sedí čísla napříč abstraktem, textem a tabulkami? (strojově, grep)
  - pochází každé číslo z běhu, o kterém text tvrdí, že mluví? (žádné frankentabulky)
  - existuje každý citovaný zdroj v `raw_secondary/` a v `process/literatura.md`?
    Sedí formát APA 7? Nesedí některá připsaná pozice jen na shodě slov mimo kontext?
  - stojí nějaké tvrzení na jediném běhu bez přiznání?
  - stojí nějaký syntetický spoj jen na shodě slov/metrik, ne na férovém srovnání?
    (pravidlo 8) — je kauzalita značená?
  - je nějaký negativní výsledek „zachráněn" post-hoc příběhem? (pravidlo 8b)
  - jednotky a zaokrouhlování konzistentní?
  - cyrilské homoglyfy v české sazbě? (strojová kontrola znaků)

`log.md` je živý stav, ne jen audit — díky němu je projekt resumovatelný mezi
sessions. Sekci „Co se osvědčilo" ber jako přenosné metodické učení.

---

## Literatura: ingest do `process/reserse.md` · `/reserse`

Rešerše je vrstva, kterou plní člověk vkládáním zdrojů do `raw_secondary/` —
jakmile tam zdroj je, smíš s ním systematicky pracovat. Vrstva se bezpečně
nabaluje: parafrázuješ propoziční pozice s atribucí, ne doslovné doklady.

**`/reserse` — ingest zdroje.** Když je v `raw_secondary/` nový soubor:
1. Ověř/dopiš **bibliografická data** (autor, rok, název, venue, DOI). Chybí-li,
   zeptej se člověka — NIKDY nedoplňuj odhadem. Přidej položku do
   `process/literatura.md` (APA 7).
2. Přečti zdroj a zkompiluj jeho **pozici** (co tvrdí k tématu práce) — parafrází,
   s provenance `(raw_secondary/<soubor> — „kotevní fráze")`.
3. **Dvouvrstvé ověření:** kotevní fráze v souboru JE a pozice sedí i v KONTEXTU
   (dataset, podmínky, nárok). Překroucení = fabulace.
4. Zařaď do `process/reserse.md`. Zmapuj shody a rozpory s pozicemi, co tam už jsou.
5. Vyznač **mezeru**, kterou tvá práce zaplňuje (co literatura neřeší/přehlíží).
6. **Přepočítej originalitu (povinné po KAŽDÉM zdroji):** co z mé otázky tenhle
   zdroj už zodpovídá — a co zbývá jako MŮJ příspěvek? Zdroj, který tezi potvrzuje,
   umí novost tiše sebrat. Zbytek zapiš explicitně.
7. **Hlídej typ a rovnováhu:** metodologický zdroj (nástroj/technika, kterou
   používáš) vs. tematický zdroj (výzkum přímo o tvém problému). Práci drží obojí;
   samé nástroje bez tematického výzkumu = rešerše, která se s ničím nekonfrontuje.
   Nahlas disbalanci.

Z `process/reserse.md` pak umíš napsat kapitolu Rešerše i situování úvodu
(konsenzus → mezera → tato práce) — pod stejným groundingem, takže žádný
vymyšlený autor.

**Hranice, pokud je `raw_secondary/` prázdná:** práce bez rešerše není
odevzdatelná diplomka — je to technická zpráva. Tuto mezeru vždy přiznej,
nezakrývej, a nikdy ji nevyplň smyšleným zdrojem.

---

## Parametrizace

Celý projekt přenastavíš výměnou `idea.md` (téma, zadání, fakulta+šablona, norma,
rozsah) a obsahu `raw_primary/` + `raw_secondary/`. Schema (tenhle soubor) zůstává.
Po dokončení práce si schema dolaď podle oboru a fakulty — vyladěné schema je
přenosný majetek.
