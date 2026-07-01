# Image Mandal – oppsummering: frakt og produktberikelse

**Sortiment:** Klær / mote
**Tema:** Fraktkostnader (Shopify + Posten Bring) og standardisering/berikelse av produkter
**Datagrunnlag:** To Posten Bring-fakturaer + samtale med Bring/mybring (Svein)

Dette dokumentet oppsummerer alt vi har diskutert, som utgangspunkt for tiltak.

---

## 1. Utgangspunktet

Svein snakket med mybring: **mange pakker sendes feil.** De fleste burde sendes
**til postkasse** – da er prisen ca. **66 kr** mot ca. **220 kr** hvis de sendes
til hentested. Er pakka for stor for postkasse, kommer et gebyr på ca. **60 kr**,
altså ca. **166 kr totalt** – fortsatt billigere enn hentested.

## 2. Hva fakturaene bekrefter

Begge fakturaene viser samme mønster: tilnærmet **alt sendes som «Pakke til hentested»**
(Bring-produkt 5800), i vektgruppe 1–7 og sone 0–1 / 1–2 / 2–3, til ~157–265 kr eks. mva
+ bompenger + pristillegg (drivstoff).

| Faktura | Periode | Antall pakker | Sum inkl. mva | Snitt pr. pakke |
|---|---|---|---|---|
| 1142801356 | 18.–28.05 | 20 | 5 470 kr | ~274 kr |
| 1142817054 | 02.–15.06 | 21 | 5 967 kr | ~284 kr |

**Konklusjon:** den dyre tjenesten brukes som standard for alt, også for lette plagg
som lett kunne gått i postkasse.

## 3. Besparelsespotensial

~40 pakker/mnd. For en moteforretning er de fleste plagg lette (< 1 kg) og postkasse-egnet.
Realistisk kan 70–90 % gå i postkasse.

| Andel til postkasse | Spart pr. pakke | Spart / mnd | Spart / år |
|---|---|---|---|
| 50 % (~20 stk) | ~150–200 kr | ~3 500 kr | ~42 000 kr |
| 75 % (~30 stk) | ~150–200 kr | ~5 250 kr | ~63 000 kr |
| 90 % (~36 stk) | ~150–200 kr | ~6 300 kr | ~75 000 kr |

Dette er den største spaken – større enn selve fraktprisen kunden betaler.

---

## 4. Tiltak (prioritert)

### 4.1 Riktig Bring-tjeneste (viktigst)
Default for lette varer skal være **postkasselevering**, ikke hentested. Hentested brukes
kun når pakka er for stor/tung for postkasse.

| Tjeneste | Bruk for | Ca. kost |
|---|---|---|
| Pakke levert i postkassen | Plagg < ~2 kg som får plass i postkassen | ~66 kr |
| Pakke til hentested | For stort/tungt for postkasse | ~166–220 kr |

### 4.2 Standardvekter per størrelse (klær/mote)
Sett vekt (inkl. emballasje) på hvert produkt så systemet kan velge postkasse automatisk.

| Kategori-tag | Typiske varer | Standardvekt | Tjeneste |
|---|---|---|---|
| `frakt-xs` | Sokker, undertøy, caps, smått tilbehør | 0,15 kg | Postkasse |
| `frakt-s` | T-skjorte, topp, skjorte, skjerf | 0,30 kg | Postkasse |
| `frakt-m` | Bukse, genser, kjole, strikk | 0,60 kg | Postkasse |
| `frakt-l` | Lett jakke, flere plagg, hettegenser | 1,00 kg | Postkasse (hvis tykkelse OK) |
| `frakt-xl` | Tung jakke/kåpe, dunjakke, sko i eske | 1,80 kg | Postkasse-grense / vurder hentested |
| `frakt-xxl` | Vinteryttertøy, støvler, store bulk-ordre | 3,00 kg+ | Hentested |

Regler:
- Vekten inkluderer emballasje – legg gjerne til 50–100 g buffer.
- Flerplaggsordre summeres automatisk → tunge ordrer havner riktig på hentested.
- `frakt-xl` er gråsonen: bruk tykkelse/mål for å avgjøre postkasse vs. hentested.

### 4.3 Fraktpris til kunde
Når reell kost for postkasse er ~66 kr, kan fraktprisen settes lavere og/eller med
**fri frakt over en terskel** (f.eks. 799 kr, justeres mot snittordre).

| Ordrevekt | Frakt til kunde (forslag) | Reell kost |
|---|---|---|
| 0–2,0 kg | 69 kr | ~66 kr |
| 2,0–5,0 kg | 149 kr | ~166 kr |
| Fri frakt over 799 kr ordre | 0 kr | dekkes på margin |

### 4.4 Oppsett i Shopify
- **Alt. A – Bring-app (carrier-calculated):** viser reell Bring-pris, velger
  postkasse/hentested automatisk ut fra vekt/mål. Anbefalt hvis tilgjengelig.
- **Alt. B – Manuelle vektbaserte satser:** fungerer på alle planer; bruk tabellen i 4.3.

---

## 5. Produktberikelse og titler

For at fraktlogikken skal virke – og for produktfeeden – må hvert produkt være riktig beriket.

### Sjekkliste for nye (og eksisterende) produkter
- [ ] **Vekt** satt (bruk kategori fra 4.2, inkl. emballasje)
- [ ] **Mål** (lengde × bredde × tykkelse) – avgjør postkasse vs. hentested i gråsonen
- [ ] **Fraktkategori-tag** (`frakt-xs` … `frakt-xxl`)
- [ ] **Produktkategori / type** riktig satt (for feed / Google Shopping)
- [ ] **Tittel** følger konvensjonen under

### Tittelkonvensjon (mote)
`[Merke] [Produkttype] [Modell/farge] – [nøkkelegenskap]`

Eksempel: `Selected Femme Bukse Vide Sort – Høyt liv`

- Merke først (folk søker på merke)
- Produkttype tidlig (bukse, kjole, genser …)
- Ingen interne koder i tittelen
- Konsistent kasus og rekkefølge på tvers av katalogen

---

## 6. Gjennomføringsrekkefølge

1. Bekreft postkasse-tjeneste og mål-/vektgrenser i mybring-avtalen.
2. Sett standardvekter på eksisterende katalog (bulk via tags/CSV).
3. Konfigurer Shopify-satser (Alt. A eller B) slik at postkasse velges automatisk.
4. Testordre i hver vektklasse – verifiser riktig tjeneste og pris i kassen.
5. Innfør berikelses-sjekklisten for alle nye produkter.
6. Følg opp neste Bring-faktura – andelen «Pakke til hentested» skal falle kraftig.

## 7. Åpne punkter å avklare

- Eksakte cm-/kg-grenser for postkasselevering (bekreftes hos mybring).
- Er Bring-appen tilgjengelig på Shopify-planen (avgjør Alt. A vs. B)?
- Faktisk snittordreverdi (justerer fri-frakt-terskelen).
- Kobling mot produktfeeden (at berikelses-feltene i kap. 5 følger med til feeden).
