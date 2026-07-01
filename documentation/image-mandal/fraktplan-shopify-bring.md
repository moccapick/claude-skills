# Fraktplan – Image Mandal (Shopify + Posten Bring)

**Sortiment:** Klær / mote
**Status:** Utkast til gjennomføring
**Bakgrunn:** Fakturaanalyse (Posten Bring) + samtale med Bring/mybring viser at
tilnærmet alle pakker sendes som «Pakke til hentested» – som er den dyre tjenesten.

> ⚠️ **Verifiser mål- og vektgrenser med mybring før endelig oppsett.** Prisene og
> vektintervallene under er basert på fakturaene og samtalen; de eksakte cm-/kg-grensene
> for postkasselevering bør bekreftes i mybring-avtalen.

---

## 1. Problemet i tall

Begge fakturaene viser samme mønster: nesten alt går som **«5800 Pakke til hentested»**.

| Faktura | Periode | Antall pakker | Sum inkl. mva | Snitt pr. pakke |
|---|---|---|---|---|
| 1142801356 | 18.–28.05 | 20 | 5 470 kr | ~274 kr |
| 1142817054 | 02.–15.06 | 21 | 5 967 kr | ~284 kr |

Linjene ligger i vektgruppe 1–7, sone 0–1 / 1–2 / 2–3, til ~157–265 kr eks. mva
+ bompenger + pristillegg (drivstoff).

**Kjernefunn (fra Svein/Bring):** de fleste av disse burde gått **til postkasse (~66 kr)**,
ikke til hentested (~220 kr). Er pakka for stor for postkasse er det ~60 kr gebyr → ~166 kr,
altså fortsatt billigere enn hentested.

### Besparelsespotensial
~40 pakker/mnd. For en moteforretning er de aller fleste plagg lette (< 1 kg) og
**postkasse-egnet**. Realistisk kan 70–90 % gå i postkasse.

| Andel til postkasse | Spart pr. pakke | Spart / mnd | Spart / år |
|---|---|---|---|
| 50 % (~20 stk) | ~150–200 kr | ~3 500 kr | ~42 000 kr |
| 75 % (~30 stk) | ~150–200 kr | ~5 250 kr | ~63 000 kr |
| 90 % (~36 stk) | ~150–200 kr | ~6 300 kr | ~75 000 kr |

Dette er den største spaken – større enn selve fraktprisen kunden betaler.

---

## 2. Riktig Bring-tjeneste (viktigst)

Default for lette varer skal være **postkasselevering**, ikke hentested.

| Tjeneste | Bruk for | Ca. kost | Kommentar |
|---|---|---|---|
| **Pakke levert i postkassen** | Plagg < ~2 kg som får plass i postkassen | ~66 kr | Standard for de fleste moteordrer |
| **Pakke til hentested** | For stort/tungt for postkasse (> ~2 kg, tykke/store) | ~166–220 kr | Kun når postkasse ikke er mulig |

Rekkefølgen i Shopify skal være: **billigste egnede tjeneste velges automatisk** ut fra
produktets vekt/mål. Det krever korrekte vekter (kap. 3).

---

## 3. Standardvekter per størrelse (klær/mote)

Sett en av disse vektene på hvert produkt (inkl. emballasje). Målet er at systemet skal
kunne velge postkasse for alt som er lett nok.

| Kategori-tag | Typiske varer | Standardvekt | Tjeneste |
|---|---|---|---|
| `frakt-xs` | Sokker, undertøy, caps, smått tilbehør | 0,15 kg | Postkasse |
| `frakt-s` | T-skjorte, topp, skjorte, skjerf | 0,30 kg | Postkasse |
| `frakt-m` | Bukse, genser, kjole, strikk | 0,60 kg | Postkasse |
| `frakt-l` | Lett jakke, flere plagg, hettegenser | 1,00 kg | Postkasse (hvis tykkelse OK) |
| `frakt-xl` | Tung jakke/kåpe, dunjakke, sko i eske | 1,80 kg | Postkasse-grense / vurder hentested |
| `frakt-xxl` | Vinteryttertøy, støvler, store bulk-ordre | 3,00 kg+ | Hentested |

**Regler:**
- Vekten skal inkludere emballasje (pose/eske). Legg gjerne til 50–100 g buffer.
- Flerplaggsordre summeres automatisk av Shopify → tunge ordrer havner riktig på hentested.
- `frakt-xl` er gråsonen: bruk mål (tykkelse) som avgjør postkasse vs. hentested.

---

## 4. Oppsett i Shopify

**Alternativ A – Bring-app (carrier-calculated rates):** viser reell Bring-pris i kassen,
velger postkasse/hentested automatisk ut fra vekt/mål. Anbefalt hvis appen er tilgjengelig
på abonnementet.

**Alternativ B – Manuelle vektbaserte satser** (fungerer på alle planer):

| Ordrevekt | Frakt til kunde | Reell kost | Margin |
|---|---|---|---|
| 0–2,0 kg | 69 kr | ~66 kr | ~0 |
| 2,0–5,0 kg | 149 kr | ~166 kr | subsidiert |
| Fri frakt over | 799 kr ordre | – | markedsføring |

- **Fri frakt over 799 kr** (juster mot snittordre) gir insentiv til større handlekurv og
  dekker fraktkost på margin.
- Satsene over er utgangspunkt – juster mot faktisk snittkost når postkasse er innført.

---

## 5. Berikelse av nye produkter (sjekkliste)

Hvert nytt produkt må ha dette før publisering/feed:

- [ ] **Vekt** satt (bruk en av kategoriene i kap. 3, inkl. emballasje)
- [ ] **Mål** (lengde × bredde × tykkelse) – avgjør postkasse vs. hentested i gråsonen
- [ ] **Fraktkategori-tag** (`frakt-xs` … `frakt-xxl`)
- [ ] **Produktkategori / type** riktig satt (for feed/Google Shopping)
- [ ] **Tittel** følger konvensjonen under

### Tittelkonvensjon (mote)
`[Merke] [Produkttype] [Modell/farge] – [nøkkelegenskap]`

Eksempel: `Selected Femme Bukse Vide Sort – Høyt liv`

- Merke først (folk søker på merke)
- Produkttype tidlig (bukse, kjole, genser …)
- Unngå interne koder i tittelen
- Konsistent kasus og rekkefølge på tvers av katalogen

---

## 6. Gjennomføringsrekkefølge

1. **Bekreft postkasse-tjeneste og grenser** i mybring-avtalen.
2. **Sett standardvekter** på eksisterende katalog (bulk via tags/CSV-eksport).
3. **Konfigurer Shopify-satser** (Alt. A eller B) slik at postkasse velges automatisk.
4. **Testordre** i hver vektklasse – verifiser at riktig tjeneste og pris vises.
5. **Innfør berikelses-sjekklisten** for alle nye produkter.
6. **Følg opp neste Bring-faktura** – andelen «Pakke til hentested» skal falle kraftig.

---

## 7. Åpne punkter

- Eksakte cm-/kg-grenser for postkasselevering (bekreftes hos mybring).
- Er Bring-appen tilgjengelig på Shopify-planen (avgjør Alt. A vs. B)?
- Faktisk snittordreverdi (justerer fri-frakt-terskel).
- Kobling mot produktfeeden (berikelse av vekt/mål/kategori/tittel før publisering).
