---
title: "Statistikk i *JSON*"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---

Følgjande tabell viser talet på innbyggjarar i fem kommunar dei siste ti åra:

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

Korleis ville du lagra desse dataa i *JSON*? Prøv gjerne sjølv før du går vidare til neste avsnitt!

Når me skal registrera det første talet i tabellen, altså 96605, må me kopla det til rett kommune og årstal. Det kan gjerast med eit objekt:

```json
[
    {
        "kommune": "Drammen",
        "årstall": "2014",
        "befolkningstall": 96605
    }
]
```

Merk at me definert ei liste der me kan halda fram med å leggja til objekt heilt til me har registrert alle verdiane i tabellen.

Ei anna moglegheit er å oppretta eit objekt som inneheld alle verdiar som er tilknytta ein kommune:

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

Ved å oppretta ei liste kan me leggja til dei fire andre kommunane på same måte.

Ei tredje moglegheit er å oppretta eit objekt som inneheld alle verdiar knytt til eit årstal:

```json 
"2014": {
    "Drammen": 96605,
    "Fredrikstad": 77591,
    "Halden": 30132,
    "Moss": 46409,
    "Sarpsborg": 54059
}
```

Ei ulempe ved desse måtane er at me bruker meir lagringsplass ein nødendig, fordi me repeterer årstala og/eller kommunenamna mange gonger.

Den største ulempa med desse måtane er at dei ikkje følgjer ein *standard*. Viss alle som publiserer statistikk gjer det på sin eigen måte, blir ein nøydd til å studera *JSON*-strukturen og nøklane kvar gong ein hentar data frå ei ny kjelde. Og når ein skal skriva eit program for å lesa og behandla *JSON*-dataa, må ein skriva spesifikk kode, som ikkje vil fungera når ein har nye data frå ei ny kjelde.

Ei løysing på dette problemet er å bli samde om at statistisk data i *JSON* berre bør registrerast på éin måte, altså etter nokre gitte reglar. Dersom ein lykkast i å etablera nokre reglar som får stor utbreiing, blir desse reglane kalla for ein *standard*. [*JSON-stat*](https://json-stat.org/) er ein *standard* for korleis statistikk skal registrerast i *JSON*.

La oss gå tilbake til befolkningstala; desse dataa er henta frå *Statistisk sentralbyrå* (*SSB*), og er eit utsnitt frå ein større tabell som inneheld alle kommunar og alle årstal frå og med 1986. På [denne](https://data.ssb.no/api/v0/dataset/26975?lang=no) sidan lèt *SSB* oss lasta ned dataa i to format; *JSON-stat* eller *CSV*. Viss du opnar *JSON-stat*-fila, vil du sjå at det er ein heilt vanleg *JSON*-fil, med attributt, objekt og lister. Men i denne fila er det ikkje lett å finna anntall innbyggjarar i Moss i 2021! Det er fordi *JSON*-fila følgjer nokre spesielle reglar for korleis tala skal registrerast, og desse reglane er definerte av *JSON-stat*.

Poenget med *JSON-stat* er ikkje at det skal vera lettlest for menneske, men at me alltid veit korleis *JSON*-fila er strukturert, og ikkje treng å skriva heilt ny kode kvar gong me skal henta og behandla nye data. Eit anna poeng med *JSON-stat* er å lagra statistisk data i *JSON* på ein plassbesparande måte; me unngår repitisjoner som i døma ovanfor.

I neste seksjon skal me sjå korleis me kan lagra kommunedataa i *JSON* ved å følgja standarden *JSON-stat*!

