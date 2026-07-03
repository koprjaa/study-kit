# Workflow — detailní popis a skryté příkazy pro agenty

Operační reference ke kitu. Vysvětluje celý běh od vhledu k hotové studii a u každého
kroku ukazuje **skrytý příkaz** — instrukci, kterou agent dostane, když napíšeš slash
příkaz (`/teze` atd.). Ty napíšeš `/teze`; agent dostane celý odstavec instrukcí, který
odkazuje do `CLAUDE.md`. Proto „skryté": vidíš tři znaky, agent dostane celý postup.

Skryté příkazy jsou soubory `.claude/commands/<jméno>.md`. Claude Code i Cursor je
načítají jako vlastní slash příkazy projektu.

---

## 1. Jak celý běh funguje (smyčka)

Workflow není dávkové, je **interaktivní** a vedené agentem:

```
start session → agent přečte log.md + process/ + study/ → řekne, kde jsme a co dál
   ↓
napíšeš slash příkaz (nebo necháš agenta navrhnout další)
   ↓
agent: vygeneruje kandidáty → předloží → u ÚSUDKU se zeptá a POČKÁ
   ↓
ty rozhodneš (teze, riziko, pass/fail gate, přijmout/odmítnout)
   ↓
agent: projde GATE → zapíše artefakt do process/ nebo study/ → přidá řádek do log.md
   ↓
agent navrhne další fázi → (smyčka)
```

**Dělba:** ty vlastníš úsudek (vhled, volba rizika, co je pravda, pass/fail).
Agent vlastní logistiku (kandidáti, hledání v `raw_primary/`, diagnostika, psaní).
V úsudkových bodech agent nikdy nerozhoduje za tebe — předloží a počká.

**Stav** drží `log.md`. Proto je běh resumovatelný: zavřeš a za týden otevřeš,
agent si přečte log a ví, kde jste skončili. Začni kdykoli příkazem `/stav`.

---

## 2. Příprava

```
raw_primary/      primární korpus (texty, které zkoumáš) — vlož, dál needituj
raw_secondary/    sekundární literatura — naplň, nebo nech prázdnou (čistě primární režim)
idea.md           surový vhled + cílový časopis + obor + rozsah — vyplň
```

Pak spusť agenta ve složce (`claude`, nebo otevři v Cursoru) a napiš `/teze`
(nebo „začni"). `CLAUDE.md` se načte jako instrukce automaticky.

---

## 3. Datový tok a stav

```
raw_primary/  ─┐
raw_secondary/ ┼─►  agent (řízený CLAUDE.md)  ──►  process/   (pracovní artefakty)
idea.md       ─┘                                └──►  study/     (hotová studie)
                                                 └──►  log.md    (stav + audit)
```

Vše v `process/` a `study/` je **odvozené a re-odvoditelné** z neměnných `raw_*`
vrstev a `idea.md`. Kdyby studie driftla, smažeš odvozené a odvodíš znovu.

---

## 4. Pipeline krok po kroku

U každé fáze: **příkaz** · co děláš ty · **skrytá instrukce** (co dostane agent,
zkráceně) · rozhodovací bod · **GATE** · artefakt.

### BLOK A — Krystalizace teze

**`/teze`** — fáze 1.1 + 1.2
*Ty:* máš surový vhled v `idea.md`. *Skrytá instrukce:* agent přečte `idea.md`,
prohledá `raw_primary/`, aplikuje test tezovitosti (5 podmínek), předloží **5
reformulací podle rizika (A–E)**, doporučí pro časopis. Pak na zvolené tezi 5
stresových testů (rozsah, strukturovatelnost, „so what", unikátnost, **ukotvitelnost**
= je nosný slovník teze slovníkem textu, nebo importovanou nálepkou?).
*Rozhodnutí:* **volba teze a rizika je tvoje** — agent počká.
*GATE:* teze splní 5 podmínek + 5 testů; u importovaného slovníku zaznamenán závazek
značit interpretační krok od začátku. *Artefakt:* `process/teze.md`.

### BLOK B — Architektura

**`/kostra`** — fáze 2.1 + 2.2
*Skrytá instrukce:* posoudí 5 strategií (kumulativní / dialektická / detektivní /
vrstvená / komparativní), doporučí. Pro každou sekci (5–7) definuje funkci, vstupní
podmínku, výstupní stav, typ evidence, délku (%). *Rozhodnutí:* volba strategie.
*GATE (test kostry):* odeberu sekci → spadne argument? prohodím dvě → změní se logika?
je poslední sekce víc než zopakování teze? *Artefakt:* `process/kostra.md`.

**`/uvod`** — fáze 2.3
*Skrytá instrukce:* 4 varianty háčku (háček z `raw_primary/`, ne z hlavy), doporučí
nejsilnější. Situování (konsenzus → mezera → moje studie), umístění teze, mapa, tón.
Sestaví návrh úvodu. *Artefakt:* `process/uvod-navrhy.md`.

**`/evidence`** — fáze 2.4 + 3.1
*Skrytá instrukce:* pro každou sekci prohledá `raw_primary/`, najde 4–6 kandidátů
**s provenance** (soubor + lokace, doslovně), ohodnotí 1–5 (relevance, přesvědčivost,
reprezentativnost, multifunkčnost, nezávislost), vybere hlavní + podpůrné.
**RED FLAG:** žádná pasáž > 3 → sekce nepodložitelná; nikdy nedoplní vymyšlený citát,
nahlásí, že korpus oporu nedává. Pak 3.1: u každého klíčového citátu 5 testů hloubky
(parafráze, spojení s tezí, vrstevnatost ≥2 z 5, přechod, vzorový odstavec).
*Artefakt:* `process/evidence.md`.

### BLOK C — Psaní

**`/prechody`** — fáze 3.2
*Skrytá instrukce:* pro každé rozhraní sekcí 3 varianty přechodu (logický / kontrastní
/ prohlubující), doporučí nejpřirozenější; hlídá trajektorii čtenáře.
*Artefakt:* `process/prechody.md`.

**`/draft`** — fáze 3.3
*Skrytá instrukce:* z artefaktů píše studii sekci po sekci do `study/` (`01-uvod.md`…).
Čistý akademický text s poznámkami pod čarou; žádné meta-komentáře. **Každý citát před
zapsáním ověří doslovně proti `raw_primary/`; co nenajde, nepoužije.**
*Artefakty:* `study/NN-*.md`.

### BLOK D — Revize a finalizace

**`/diagnostika`** — fáze 4.1
*Skrytá instrukce:* projde draft na 5 osách (kontinuita, proporce, koheze, redundance,
nevyřčené předpoklady), sestaví prioritní seznam oprav (kritické/důležité/kosmetické)
a **cíleně** je implementuje — žádný plošný přepis. *Artefakt:* `process/diagnostika.md`
+ opravené sekce.

**`/skrty`** — fáze 4.2
*Skrytá instrukce:* najde 5 typů nadbytečného textu (dekorativní, obranné, rehearsalové,
encyklopedické, ztracené odbočky), odhadne % škrtnutelného. *Rozhodnutí:* odsouhlasíš
škrty. *Artefakt:* `process/proskrtat.md` + provedené škrty.

**`/review`** — fáze 4.3 — *nejdůležitější epistemický gate*
*Skrytá instrukce:* konfrontuje draft **proti `raw_primary/`** jako odpůrce (ne naopak).
Tři tvrdé kontroly vždy: **věrnost citátů** (doslovnost + kontiguita), **frekvence
„důkazů"** (grep), **spoje, ne cihly** (syntéza stojí na pojmu, ne na shodě slov).
Plus ohraničení teze (pravidlo 8b): je nějaký text „zachráněn" vývojovým příběhem
nebo „výjimkou, co potvrzuje pravidlo"? Napíše posudek s námitkami a 1 nejdůležitější
větou. *Artefakt:* `process/posudek.md`.

**`/revize`** — fáze 4.4
*Skrytá instrukce:* pro každou námitku najde v `raw_primary/` materiál k odpovědi,
navrhne úpravu a implementuje ji; iteruje, dokud nejsou vyřešené všechny ZÁSADNÍ námitky.
*Artefakt:* `process/reakce.md` + opravené sekce.

**`/checklist`** — fáze 4.5
*Skrytá instrukce:* projde 6 kategorií (argument, evidence, teorie, sekundární
literatura, formální, čitelnost — NE počet slov; souvětí je nástroj myšlení, hlídá se,
zda dlouhá věta nese strukturu a dá se přečíst na jeden nádech). Poslední test: 1. + poslední
věta každé sekce tvoří příběh? *Artefakt:* `process/checklist.md`.

### Bonus

**`/zaver`** (B.1) — návrh závěru, který posune čtenáře, otevře perspektivy, vrátí se
k háčku, dá „so what", nabídne 3 varianty poslední věty.
**`/abstrakt`** (B.2) — abstrakt CZ + EN o 5 funkcích + 5–8 klíčových slov; kontrola,
že odpovídá skutečnému obsahu, ne záměru.
**`/oponent`** (B.3) — recenzentský posudek přínosu/novosti/zařazení proti `raw_secondary/`,
spouštěný **po `/review`** (pravda před hodnotou). Novost tvrdí jen vůči načteným zdrojům;
kde obor chybí, přizná „neposoudím" a eskaluje na člověka. *Artefakt:* `process/oponentura.md`.

---

## 5. Podpůrné příkazy (mimo lineární tok)

**`/stav`** — agent přečte `log.md` + `process/` + `study/`, řekne, kde jste a jaký je
další krok. Nic nemění. Spouštěj na začátku session.

**`/lint`** — kontrola integrity (jako checklist, neopravuje automaticky):
poznámky nesou kotevní fráze (ne holé „Tamtéž")? citáty doslovné a souvislé? tvrzení
na opakovaném slově bez frekvenční kontroly? syntetický spoj na shodě slov? teze
„zachráněná" protipříkladem? sekce na jednom citátu? rejstřík mimo cílový časopis?

**`/badani`** — ingest sekundárního zdroje z `raw_secondary/` do `process/badani.md`:
zkompiluje pozici autora (parafráze + provenance + kotevní fráze), zmapuje shody/spory
s ostatními, vyznačí mezeru, kterou teze zaplňuje. Připíše jen to, co v souboru najde;
zdroj mimo `raw_secondary/` nejmenuje. Po pár zdrojích umí napsat situování do úvodu.

---

## 6. Reference skrytých příkazů (co přesně agent dostane)

Doslovné instrukce, na které se slash příkazy rozbalí. Žijí v `.claude/commands/`.
Jsou tenké schválně — detail metody je v `CLAUDE.md`, ony jen spouštějí fázi a
připomínají gate. Jediný zdroj pravdy je `CLAUDE.md`; když měníš metodu, měň ji tam,
ne v příkazech.

| Příkaz | Spouští | Gate / klíčová kontrola | Výstup |
|---|---|---|---|
| `/stav` | orientace | — | (nic) |
| `/teze` | 1.1 + 1.2 | 5 podmínek + 5 testů (vč. ukotvitelnosti) | `process/teze.md` |
| `/kostra` | 2.1 + 2.2 | test kostry (odebrat/prohodit sekci) | `process/kostra.md` |
| `/uvod` | 2.3 | háček z `raw_primary/` | `process/uvod-navrhy.md` |
| `/evidence` | 2.4 + 3.1 | RED FLAG (pasáž > 3); ≥2 z 5 vrstev | `process/evidence.md` |
| `/prechody` | 3.2 | trajektorie čtenáře | `process/prechody.md` |
| `/draft` | 3.3 | citát ověřen proti `raw_primary/` | `study/NN-*.md` |
| `/diagnostika` | 4.1 | 5 os; cílené opravy | `process/diagnostika.md` |
| `/skrty` | 4.2 | 5 typů balastu | `process/proskrtat.md` |
| `/review` | 4.3 | citát+kontiguita, frekvence, spoj, ohraničení (8b) | `process/posudek.md` |
| `/revize` | 4.4 | vyřešeny zásadní námitky | `process/reakce.md` |
| `/oponent` | po 4.3 | přínos/novost/zařazení; novost jen vůči `raw_secondary/` | `process/oponentura.md` |
| `/checklist` | 4.5 | 6 kategorií; příběh z 1.+poslední věty | `process/checklist.md` |
| `/zaver` | B.1 | posun, ne shrnutí | `study/` (závěr) |
| `/abstrakt` | B.2 | odpovídá obsahu, ne záměru; CZ+EN | `study/` (abstrakt) |
| `/badani` | sekundárka | jen co je v `raw_secondary/`; nic nevymýšlet | `process/badani.md` |
| `/lint` | kontrola | provenance v poznámce, kontiguita, spoje, 8b | (checklist) |

---

## 7. Typický průchod (happy path)

```
/stav   →   /teze   →   /kostra   →   /uvod   →   /evidence   →   /prechody
   →   /draft   →   /diagnostika   →   /skrty   →   /review   →   /revize
   →   /checklist   →   /zaver   →   /abstrakt
```

`/oponent` pusť **po `/review`** (pravda před hodnotou): až je studie ověřená proti
`raw_primary/`, oponent posoudí přínos a zařazení proti `raw_secondary/`. Sekundární
literatura kdykoli souběžně: naplň `raw_secondary/` → `/badani` (klidně opakovaně) →
situování se promítne do `/uvod`. `/lint` pusť před `/review` a před odevzdáním. Když
ztratíš nit, `/stav`.

---

## 8. Kde se reálně rozhoduješ (a nesmíš to nechat na agentovi)

Tyhle body jsou tvoje a agent u nich má počkat:

1. **Volba teze a míry rizika** (`/teze`) — žádný gate ti odvahu na verzi D/E nedodá.
2. **Volba strategie** (`/kostra`).
3. **Pass/fail u každého gate** — agent navrhuje, posuzuješ ty.
4. **Odsouhlasení škrtů** (`/skrty`) a **přijetí/odmítnutí námitek** (`/revize`).
5. **Co je pravda** — finální verbatim ověření citátů je nepřenosné; agent ho připraví,
   ale ručíš ty.
6. **Dialog s bádáním** — sekundární zdroje sháníš a vkládáš ty; agent je nevymyslí.
