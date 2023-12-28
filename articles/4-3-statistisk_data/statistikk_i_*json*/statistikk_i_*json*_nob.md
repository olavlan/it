---
title: "Statistikk i *JSON*"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---

Følgende tabell viser antall innbyggere i fem kommuner de siste ti årene: 

|          | **Drammen** | **Fredrikstad** | **Halden** | **Moss** | **Sarpsborg** |
|----------|-------------|-----------------|------------|----------|---------------|
| **2014** |       96605 |           77591 |      30132 |    46409 |         54059 |
| **2015** |       97771 |           78159 |      30328 |    47044 |         54192 |
| **2016** |       98930 |           78967 |      30544 |    47640 |         54678 |
| **2017** |       99734 |           80121 |      30790 |    48154 |         55127 |
| **2018** |      100302 |           80977 |      31037 |    48671 |         55543 |
| **2019** |      100581 |           81772 |      31177 |    48871 |         55997 |
| **2020** |      101386 |           82385 |      31373 |    49273 |         56732 |
| **2021** |      101859 |           83193 |      31387 |    49668 |         57372 |
| **2022** |      102273 |           83892 |      31444 |    50290 |         58182 |
| **2023** |      103291 |           84444 |      31730 |    51240 |         59038 |

Hvordan ville du lagret disse dataene i *JSON*? Prøv gjerne selv før du går videre til neste avsnitt!

Når vi skal registrere det første tallet i tabellen, altså 96605, må vi koble det til riktig kommune og årstall. Det kan gjøres med et objekt: 

```json
[
    {
        "kommune": "Drammen",
        "årstall": "2014",
        "befolkningstall": 96605
    }
]
```

Merk at vi definert en liste der vi kan fortsette å legge til objekter helt til vi har registrert alle verdiene i tabellen.

En annen mulighet er å opprette et objekt som inneholder alle verdier som er tilknyttet en kommune: 

```json
"Halden": {
    "2014": 30132, 
    "2015": 30328,
    "2016": 30544, 
    "2017": 30790,
    "2018": 31037,
    "2019": 31177,
    "2020": 31373,
    "2021": 31387,
    "2022": 31444,
    "2023": 31730
}
```

Ved å opprette en liste kan vi legge til de fire andre kommunene på samme måte. 

En tredje mulighet er å opprette et objekt som inneholder alle verdier tilknyttet et årstall:

```json 
"2014": {
    "Drammen": 96605,
    "Fredrikstad": 77591,
    "Halden": 30132,
    "Moss": 46409,
    "Sarpsborg": 54059
}
```

En ulempe ved disse måtene er at vi bruker mer lagringsplass en nødendig, fordi vi repeterer årstallene og/eller kommunenavnene mange ganger. 

Den største ulempen med disse måtene er at de ikke følger en *standard*. Hvis alle som publiserer statistikk gjør det på sin egen måte, blir man nødt til å studere *JSON*-strukturen og nøklene hver gang man henter data fra en ny kilde. Og når man skal skrive et program for å lese og behandle *JSON*-dataene, må man skrive spesifikk kode, som ikke vil fungere når man har nye data fra en ny kilde.  

En løsning på dette problemet er å bli enige om at statistisk data i *JSON* kun bør registreres på én måte, altså etter noen gitte regler. Dersom man lykkes i å etablere noen regler som får stor utbredelse, kalles disse reglene for en *standard*. [*JSON-stat*](https://json-stat.org/) er en *standard* for hvordan statistikk skal registreres i *JSON*. 

La oss gå tilbake til befolkningstallene; disse dataene er hentet fra *Statistisk sentralbyrå* (*SSB*), og er et utsnitt fra en større tabell som inneholder alle kommuner og alle årstall fra og med 1986. På [denne](https://data.ssb.no/api/v0/dataset/26975?lang=no) siden lar *SSB* oss laste ned dataene i to formater; *JSON-stat* eller *CSV*. Hvis du åpner *JSON-stat*-filen, vil du se at det er en helt vanlig *JSON*-fil, med attributter, objekter og lister. Men i denne filen er det ikke lett å finne anntall innbyggere i Moss i 2021! Det er fordi *JSON*-filen følger noen spesielle regler for hvordan tallene skal registreres, og disse reglene er definert av *JSON-stat*.

Poenget med *JSON-stat* er ikke at det skal være lettlest for mennesker, men at vi alltid vet hvordan *JSON*-filen er strukturert, og ikke trenger å skrive helt ny kode hver gang vi skal hente og behandle nye data. Et annet poeng med *JSON-stat* er å lagre statistisk data i *JSON* på en plassbesparende måte; vi unngår repitisjoner som i eksemplene ovenfor. 

I neste seksjon skal vi se hvordan vi kan lagre kommunedataene i *JSON* ved å følge standarden *JSON-stat*!

