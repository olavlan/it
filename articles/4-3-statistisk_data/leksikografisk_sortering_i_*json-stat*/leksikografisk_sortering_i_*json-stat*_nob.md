---
title: "Leksikografisk sortering i *JSON-stat*"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---

Følgende liste viser hvordan verdiene er sortert: 

```
Indeks  Kommune Årstall   value
0       Drammen    2014   96605
1       Drammen    2015   97771
2       Drammen    2016   98930
3       Drammen    2017   99734
4       Drammen    2018  100302
5       Drammen    2019  100581
6       Drammen    2020  101386
7       Drammen    2021  101859
8       Drammen    2022  102273
9       Drammen    2023  103291
10  Fredrikstad    2014   77591
11  Fredrikstad    2015   78159
12  Fredrikstad    2016   78967
13  Fredrikstad    2017   80121
14  Fredrikstad    2018   80977
15  Fredrikstad    2019   81772
16  Fredrikstad    2020   82385
17  Fredrikstad    2021   83193
18  Fredrikstad    2022   83892
19  Fredrikstad    2023   84444
20       Halden    2014   30132
21       Halden    2015   30328
22       Halden    2016   30544
23       Halden    2017   30790
24       Halden    2018   31037
25       Halden    2019   31177
26       Halden    2020   31373
27       Halden    2021   31387
28       Halden    2022   31444
29       Halden    2023   31730
30         Moss    2014   46409
31         Moss    2015   47044
32         Moss    2016   47640
33         Moss    2017   48154
34         Moss    2018   48671
35         Moss    2019   48871
36         Moss    2020   49273
37         Moss    2021   49668
38         Moss    2022   50290
39         Moss    2023   51240
40    Sarpsborg    2014   54059
41    Sarpsborg    2015   54192
42    Sarpsborg    2016   54678
43    Sarpsborg    2017   55127
44    Sarpsborg    2018   55543
45    Sarpsborg    2019   55997
46    Sarpsborg    2020   56732
47    Sarpsborg    2021   57372
48    Sarpsborg    2022   58182
49    Sarpsborg    2023   59038
```

Her ser vi at lista er sortert *primært* etter kommune og *sekundært* etter årstall. Derfor satte vi "Kommune" som første dimensjon og "Årstall" som andre dimensjon i attributtet "id": 

```json 
"id": ["Kommune", "Årstall"]
```

*Dersom vi hadde sortert primært etter årstall, måtte "Årstall" vært første dimensjon og derfor kommet først i lista.*

Det er viktig at sorteringen følger et slikt mønster, som kalles *leksikografisk sortering*. Kanskje du ser at det minner om alfabetisk sortering? For å forstå leksikografisk sortering, kan vi gi to eksempler på rekkefølger som **ikke** er lov. Det første eksempelet er: 

```
0       Drammen    2014   96605
1       Drammen    2015   97771
2   Fredrikstad    2014   77591
3       Drammen    2016   98930
...
```
Dette er **ikke** leksikografisk sortering fordi alle registreringer for Drammen må komme etter hverandre. Vi har lov til å flytte Fredrikstad foran Drammen, men da må vi flytte **alle** verdiene for Fredrikstad foran **alle** verdiene for Drammen.   

Det andre ekempelet er:
```
0       Drammen    2014   96605
1       Drammen    2015   97771
2       Drammen    2016   98930
...
10  Fredrikstad    2023   77591
11  Fredrikstad    2022   78159
12  Fredrikstad    2021   78967
```
Dette er **ikke** leksikografisk sortering fordi årstallene alltid må komme i samme rekkefølge. Vi kan bestemme selv hva rekkefølgen skal være, men vi må være konsekvente. 

Innad i hver dimensjon har vi altså lov til å velge rekkefølgen av kategorier, og deretter sortere verdiene leksikografisk etter denne rekkefølgen. Kommunene kommer i følgende rekkefølge: 

1. Drammen
2. Fredrikstad
3. Halden
4. Moss
5. Sarpsborg. 

Attributtet "index" brukes for å registrere rekkefølgen av kategorier: 

```json 
"id": ["Kommune", "Årstall"]
"size": [5, 10]
"dimension": {
    "Kommune": {
        "category": {
            "index": {
                "0101": 2,
                "0104": 3,
                "0105": 4,
                "0106": 1,
                "0602": 0
            }
            "label": {
                "0101": "Halden",
                "0104": "Moss", 
                "0105": "Sarpsborg",
                "0106": "Fredrikstad",
                "0602": "Drammen"
            }
        }
    }
}

```
Nå kan vi for eksempel lese at kategorien "0602" har navnet "Drammen" og indeksen 0; dermed vet vi at Drammen er den første kommunen i sorteringen! Hva er den neste kommunen? 

Vi må også gi rekkefølgen av kategoriene i "Årstall". Det virker kanskje åpenbart at årstallene kommer kronologisk, men vi må spesifisere dette:

```json 
"Årstall": {
    "category": {
        "index": [
            "14",
            "15",
            "16",
            "17", 
            "18",
            "19",
            "20",
            "21",
            "22",
            "23"
        ]
        "label": {
            "14": "2014",
            "15": "2015",
            "16": "2016",
            "17": "2017",
            "18": "2018",
            "19": "2019",
            "20": "2020",
            "21": "2021",
            "22": "2022",
            "23": "2023"
        }
    }
}
```
Her ser vi at det holder å plassere nøklene i en liste dersom vi sørger for at rekkefølgen er riktig! Det er altså to måter å spesifisere rekkefølgen til kategoriene, og det er viktig å kjenne til begge. Sammenlign gjerne de to måtene, og tenk over hvordan du kunne ha registrert rekkefølgen av kommuner som en sortert liste av nøkler. 

Nå har vi registrert befolkningsdataene i et *JSON-stat*-objekt: 

```json
{
    "version": "2.0",
    "class": "dataset",
    "label": "Befolkningstall i fem kommuner i perioden 2014-2023",

    "id": ["Kommune", "Årstall"],
    "size": [5, 10],
    "dimension": {
        "Kommune": {
            "category": {
                "index": {
                    "0101": 2,
                    "0104": 3,
                    "0105": 4,
                    "0106": 1,
                    "0602": 0
                },
                "label": {
                    "0101": "Halden",
                    "0104": "Moss", 
                    "0105": "Sarpsborg",
                    "0106": "Fredrikstad",
                    "0602": "Drammen"
                }
            }
        },
        "Årstall": {
            "category": {
                "index": [
                    "14",
                    "15",
                    "16",
                    "17", 
                    "18",
                    "19",
                    "20",
                    "21",
                    "22",
                    "23"
                ],
                "label": {
                    "14": "2014",
                    "15": "2015",
                    "16": "2016",
                    "17": "2017",
                    "18": "2018",
                    "19": "2019",
                    "20": "2020",
                    "21": "2021",
                    "22": "2022",
                    "23": "2023"
                }
            }
        }
    },

    "value": [ 
        96605,97771,98930,99734,100302,100581,101386,101859,102273,103291,
        77591,78159,78967,80121,80977,81772,82385,83193,83892,84444,
        30132,30328,30544,30790,31037,31177,31373,31387,31444,31730,
        46409,47044,47640,48154,48671,48871,49273,49668,50290,51240,
        54059,54192,54678,55127,55543,55997,56732,57372,58182,59038
    ]   
}
```

Det er ikke like lett å lese som en tabell; hvordan kan vi for eksempel hente befolkningstallet i Moss i 2015? Dimensjonsdataene forteller oss at Moss er den fjerde kommunen, så tre kommuner registrert før Moss; hver av disse kommunene har ti verdier, så det er $3\cdot 10 = 30$ verdier før Moss. Siden vi ønsker det andre årstallet, må vi hente verdi nummer $30 + 2 = 32$. Det 32. tallet i lista er 47044!

Det er viktig å forstå Iutregningen ovenfor, altså hvordan vi bruker dimensjonsdataene til å finne spesifikke verdier. Forsøk for eksempel å finne befolkningstallet til følgende kategorier, eller velg kategorier selv: 

* Fredrikstad, 2018
* Sarpsborg, 2014
* Drammen, 2023

I neste seksjon skal vi skrive et Python-program som gjør utregningen for oss!

**Aktivitetsforslag.** 

1. Finn en tabell med data som du finner interessant, helst med flere rader og kolonner (det vil si to dimensjoner og flere kategorier i hver av dem). For eksempel kan du bruke søkefraser som "life expectancy by country and sex", eller søke på *Wikipedia*, som har mange tabeller. 
2. Registrer dataene du fant etter *JSON-stat*-standarden; kopier strukturen under og fyll inn verdier.

```json
    {
    "version": "2.0",
    "class": "dataset",
    "label": "", 

    "id": ["Dimension1", "Dimension2"],
    "size": [], 
    "dimension": {
        "Dimension1": {
            "category": {
                "index": {}
                "label": {}
            }
        },
        "Dimension2": {
            "category": {
                "index": {}
                "label": {}
            }
        } 
    }

    "value": []
}
```

Tips: 
* Hvis tabellen er for stor, kan du gjøre et utvalg av rader og kolonner (altså et utvalg av kategorier).
* Når du legger inn verdiene i attributtet "value", må du huske at de skal være leksikografisk sortert i henhold til dimensjonsdataene. 

