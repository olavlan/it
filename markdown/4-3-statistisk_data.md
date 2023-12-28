# Behandling av statistisk data

## Statistikk i *JSON*

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

## Statistisk data i *JSON-stat*

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

Vi skal nå bruke *JSON-stat* til å registrere dataene i denne tabellen. Grunnidéen i *JSON-stat* er å gjøre dataene *flate*. Det betyr rett og slett at vi plasserer alle verdiene i en liste: 

```json
[ 
    96605,97771,98930,99734,100302,100581,101386,101859,102273,103291,
    77591,78159,78967,80121,80977,81772,82385,83193,83892,84444,
    30132,30328,30544,30790,31037,31177,31373,31387,31444,31730,
    46409,47044,47640,48154,48671,48871,49273,49668,50290,51240,
    54059,54192,54678,55127,55543,55997,56732,57372,58182,59038
]
```
Her har vi brukt linjeskift slik at det fortsatt ser ut som en tabell med rader og kolonner, men egentlig er det bare en enkel liste med tall. Nå må vi legge til informasjon som gjør det mulig å koble verdiene til årstall og kommune; *JSON-stat* gir en oppskrift for hvordan vi skal gjøre dette. 

Målet i denne seksjonen er å opprette et *JSON-stat*-objekt som inneholder befolkningsstatistikken. Et *JSON-stat*-objekt har følgende struktur: 

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

*Du kan kopiere denne strukturen når du skal opprette ditt eget *JSON-stat*-objekt.*

Vi kan si at *JSON-stat*-objektet består av tre deler: 

- Metadata
- Dimensjonsdata
- Verdier

**Metadata** er de tre første linjene av objektet: 

```json
"version": "2.0",
"class": "dataset",
"label": ""
```

Metadata brukes for å gi relevant bakgrunnsinformasjon; de to første attributtene er obligatoriske og forteller hvilken utgave av *JSON-stat* vi bruker. Det siste attributtet er valgfritt og brukes for å gi en tittel til statistikken:

```json 
"label": "Befolkningstall i fem kommuner i perioden 2014-2023"
```

Det finnes andre valgfrie attributter vi kan legge til for å gi bakgrunnsinformasjon om statistikken.

**Dimensjonsdata** gir informasjon som kobler tallverdiene til *kategorier*. Når vi har fylt inn dimensjonsdata, vil det for eksempel være mulig å koble den 37. verdien  til kategoriene "2021" og "Fredrikstad". 

Dimensjonsdataene består av attributtene "id", "size" og "dimension". I attributtet "dimension"  finner vi et nytt objekt med en spesifikk struktur, som vi skal forklare nøye i denne seksjonen. 

For å registrere **verdier** brukes attributtet "value", som skal inneholde en liste av verdier: 

```json
"value": [ 
    96605,97771,98930,99734,100302,100581,101386,101859,102273,103291,
    77591,78159,78967,80121,80977,81772,82385,83193,83892,84444,
    30132,30328,30544,30790,31037,31177,31373,31387,31444,31730,
    46409,47044,47640,48154,48671,48871,49273,49668,50290,51240,
    54059,54192,54678,55127,55543,55997,56732,57372,58182,59038
]
```

Den enkleste oppgaven er altså å registrere alle verdiene! Det som gjenstår er dimensjonsdataene, som kobler verdiene til riktige kategorier. Hver verdi kan kobles til én kommune og ett årstall; derfor sier vi at "Kommune" og "Årstall" er *dimensjonene* til datasettet. For å registrere dimensjonene bruker vi attributtet "id": 

```json
"id": ["Kommune", "Årstall"]
```

Dataene vårt har altså to dimensjoner, men det finnes ingen begrensing på antall dimensjoner. Tenk deg at at tabellen inneholdt antall mennn og antall kvinner i hver kolonne. Da ville tabellen hatt dobbelt så mange verdier, og vi kunne sagt at hver verdi kan kobles til en kommune, et årstall og et kjønn.  Vi ville altså hatt tre dimensjoner, og listen av dimensjoner kunne vært skrevet som `["Kommune", "Årstall", "Kjønn"]`. 

Videre må vi opprette attributtet "size", som forteller antall kategorier i hver dimensjon: 

```json
"id": ["Kommune", "Årstall"]
"size": [5, 10]
```

Den første dimensjonen har 5 *kategorier* (fem kommuner) den andre dimensjonen har 10 *kategorier* (ti årstall). 

Videre må vi fortelle hva som er kategoriene i hver dimensjon, og til dette brukes attributtet "dimension". Vi begynner med kategoriene i "Kommune": 

```json
"id": ["Kommune", "Årstall"]
"size": [5, 10]
"dimension":
    "Kommune": {
        "category": {
            "label": {
                "0101": "Halden",
                "0104": "Moss", 
                "0105": "Sarpsborg",
                "0106": "Fredrikstad",
                "0602": "Drammen"
            }
        }
    }
```

Her ser vi at hver kategori må ha både en nøkkel og et navn. Det er fordi to kategorier i prinsippet kan ha samme navn, og da må de kunne skilles med unike nøkler. Her har vi brukt [kommunenumre](https://snl.no/kommunenummer) som nøkler, fordi vi vet at hver kommune har et unikt kommunenummer. 

Du lurer kanskje på hva som er poenget med alle attributtene som *JSON-stat* krever? 

* Poenget med nøkkelen "dimension" er å fortelle at i dette attributtet finner man informasjon om dimensjonene. 
* Poenget med nøkkelen "Kommune" er å fortelle at i dette attributtet finner man informasjon om dimensjonen "Kommune".
* Poenget med nøklene "category" og "label" er å spesifisere **hvilken** informasjon vi gir om dimensjonen "Kommune". I dette tilfellet ønsker vi å liste *kategoriene* i dimensjonen, og vi ønsker å gi *navn* (*label*) til hver kategori. 

La oss nå liste kategoriene i "Årstall" på akkurat samme måte:

```json
"Årstall": {
    "category": {
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

La oss oppsummere det vi har gjort før vi går videre: 

* Registrert at første dimensjon er "Kommune" og at andre dimensjon er "Årstall".
* Registrert navnet til alle kategoriene, det vil si de fem kommunene og de ti årstallene. 

Er vi ferdige? Nei, for vi må også fortelle hvordan lista av verdier er sortert, altså hva som er rekkefølgen av kommuner og årstall. Det skal vi se på i neste seksjon!

## Leksikografisk sortering i *JSON-stat*

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

## Innlesing av *JSON-stat* i Python

Vi oppretter nå filen `befolkning.json` og limer inn *JSON-stat*-objektet fra forrige seksjon:

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

Det første steget er å legge filinnholdet i en *dictionary*. Dette gjøres med Python-pakken `json`: 


```python
import json

with open("befolkning.json") as file:
    dataset = json.load(file)
```

Vi skal nå fordele de ulike dataene i variabler, slik at vi får litt bedre oversikt. Som nevnt i forrige seksjon består `JSON-stat`-objektet av metadata, dimensjonsdata og verdier. Vi vet at det finnes to dimensjoner, og at vi kan hente navnet til dimensjonene, som finnes i attributtet "id": 


```python
dim1_name = dataset["id"][0]
dim2_name = dataset["id"][1]
print(dim1_name)
print(dim2_name)
```

    Kommune
    Årstall


*Vi bør egentlig ta høyde for at datasettet kan ha flere enn to dimensjoner, men for å forenkle presentasjonen skal vi begrense oss til 2-dimensjonale datasett.*

Videre kan vi hente størrelsen til dimensjonene, som finnes i attributtet "size": 


```python
dim1_size = dataset["size"][0]
dim2_size = dataset["size"][1]
print(dim1_size)
print(dim2_size)
```

    5
    10


I neste omgang kan vi hente kategoriene i hver dimensjon. For å hente kommunenavnene, må vi gå inn på attributtene "dimension" -> "Kommune" -> "category" -> "label". Husk at vi ikke bør skrive tekststrengen "Kommune" direkte, men heller bruke variabelen vi definerte tidligere, slik at programmet fungerer på andre `JSON-stat`-filer, der navnene på dimensjonene antagelig vi være noe annet! For å hente kommunenavnene gjør vi altså følgende: 


```python
dim1_categories = dataset["dimension"][dim1_name]["category"]["label"]
print(dim1_categories)
```

    {'0101': 'Halden', '0104': 'Moss', '0105': 'Sarpsborg', '0106': 'Fredrikstad', '0602': 'Drammen'}


Nå kan vi også hente rekkefølgen av kommuner, som ligger i attributtet "index" i stedet for "label": 


```python
dim1_categories_index = dataset["dimension"][dim1_name]["category"]["index"]
print(dim1_categories_index)
```

    {'0101': 2, '0104': 3, '0105': 4, '0106': 1, '0602': 0}


For å hente kategoriene i den andre dimensjonen, altså "Årstall", gjør vi i utgangspunktet akkurat det samme: 


```python
dim2_categories = dataset["dimension"][dim2_name]["category"]["label"]
dim2_categories_sorted = dataset["dimension"][dim2_name]["category"]["index"]
print(dim2_categories)
print(dim2_categories_sorted)
```

    {'14': '2014', '15': '2015', '16': '2016', '17': '2017', '18': '2018', '19': '2019', '20': '2020', '21': '2021', '22': '2022', '23': '2023'}
    ['14', '15', '16', '17', '18', '19', '20', '21', '22', '23']


Her ser vi imidlertid at rekkefølgen av årstall er gitt som en sortert liste. Det kan være nyttig å ha rekkefølgen på samme format som vi hadde for kommunene. 


```python
i = 0
temp = {}
for c in dim2_categories_sorted:
    temp[c] = i
    i += 1

dim2_categories_index = temp
print(dim2_categories_index)
```

    {'14': 0, '15': 1, '16': 2, '17': 3, '18': 4, '19': 5, '20': 6, '21': 7, '22': 8, '23': 9}


Til slutt kan vi legge listen av verdier i en variabel:


```python
values = dataset["value"]
print(values)
```

    [96605, 97771, 98930, 99734, 100302, 100581, 101386, 101859, 102273, 103291, 77591, 78159, 78967, 80121, 80977, 81772, 82385, 83193, 83892, 84444, 30132, 30328, 30544, 30790, 31037, 31177, 31373, 31387, 31444, 31730, 46409, 47044, 47640, 48154, 48671, 48871, 49273, 49668, 50290, 51240, 54059, 54192, 54678, 55127, 55543, 55997, 56732, 57372, 58182, 59038]


Nå har vi følgende variabler: 

* `dim1_navn`, `dim1_size`, `dim1_categories`, `dim1_categories_index`
* `dim2_navn`, `dim2_size`, `dim2_categories`, `dim2_categories_index`
* `values`

Sjekk gjerne at du vet hva disse variablene inneholder før du leser videre.

La oss si at vi ønsker å hente befolkningstallet i Halden i 2016; vi vet at denne verdien ligger i lista `values`, men hvordan finner vi den? For å repetere hvordan lista av verdier er sortert, kan vi først telle oss fram til den riktige verdien: 

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
```

Vi finner altså den riktige verdien på indeks 22: 


```python
print(values[22])
```

    30544


Hvis vi studerer tabellen over, kommer vi fram til følgende regnestykke for å finne riktig indeks:

$22$   
$= 2 \cdot 10 + 2$    
$= (\text{antall kommuner før Halden}) \cdot (\text{antall årstall totalt}) \quad + \quad (\text{antall årstall før 2016})$    
$= \ ($ `dim1_categories_index["0101"]` $- 1)\ \cdot$ `dim2_size` $\quad + \quad ($ `dim2_categories_index["16"]` $- 1)$

Denne siste linjen kan vi bruke for å skrive et program som henter riktig verdi: 


```python
desired_kommune = "0101"
desired_year = "16"

index = (dim1_categories_index[desired_kommune]) * dim2_size + (dim2_categories_index[desired_year])

print(index)
print(values[index])
```

    22
    30544


Vi kan nå lage en funksjon som finner riktig indeks for et hvilket som helst kommunenummer og årstall:


```python
def get_index(dim1_desired_category, dim2_desired_category):
    index = (dim1_categories_index[dim1_desired_category]) * dim2_size + (dim2_categories_index[dim2_desired_category])
    return index
```

Til slutt kan vi lage en funskjon som gir innbyggertallet for en gitt kombinasjon av kommune og år: 


```python
def get_population(kommunenummer, year): 
    index = get_index(kommunenummer, year)
    return values[index]
```

Nå kan vi lett hente befolkningstallet som hører til følgende kategorier: 

* Fredrikstad, 2018 ("0106", "18")
* Sarpsborg, 2014 ("0105", "14")
* Drammen, 2023 ("0602", "23")

Vi trenger bare å bruke funksjonen `get_population` med riktige parametre: 


```python
print(get_population("0106", "18"))
print(get_population("0105", "14"))
print(get_population("0602", "23"))
```

    80977
    54059
    103291


**Aktivitetsforslag.** Ta utgangspunkt i *JSON-stat*-filen du lagde i aktiviteten fra forrige seksjon. Skriv en funksjon som i eksempelet over; parametrene skal være gitte kategorier, og funksjonen skal returnere verdien som er tilknyttet disse kategoriene. 

## Innlesing av JSON-stat med pandas


```python
from pyjstat import pyjstat

with open("befolkning.json") as file:
    dataset = pyjstat.Dataset.read(file)

df = dataset.write('dataframe')
print(df)
```

## Behandling av data fra *SSB*

I denne seksjonen skal vi behandle data som er lagret etter *JSON-stat*-standarden. Vi skal hente ferdige datasett publisert av *SSB*, som ligger [her](https://data.ssb.no/api/). 

**Versjoner av *JSON*-stat.** I seksjonen om *JSON-stat* forklarte vi strukturen til et *JSON-stat*-objekt basert på den nyeste versjonen, *JSON-stat* 2.0. Dette registrerte vi også som første attributt i objektet: 

```json
"version": "2.0"
```

*SSB* benytter imidlertid en eldre versjon av *JSON-stat*. Måten å registrere data på er helt likt, men attributtene er organisert litt annerledes. Følgende viser strukturen til ny og gammel *JSON-stat*.


***JSON-stat* 2.0**:

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
***JSON-stat* brukt av SSB:**

```json
{
    "dataset": {
        
        "label": ""
        
        "dimension": {
            "id": ["Dimension1", "Dimension2"],
            "size": [], 
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
        
        "value": []
    }
}
```

Det er to hovedforskjeller:

1. I *JSON-stat* brukt av *SSB* plasseres alt inni attributtet "dataset". 
2. I *JSON-stat* brukt av *SSB* plasseres alle dimensjonsdata i attributtet "dimension". Dette inkluderer "id" og "size". 

## Visualisering med koropletkart

Mulighet for å nevne GeoJSON, en standard for å lagre geografisk informasjon, slik som avgrensing av et område. Finnes åpne GeoJSON-data for kommunegrensene i Norge, som kan kombineres med kommunedata fra SSB og kartverktøyet folium. Eksempel: vise befolkningsdata i kommuner på kart med fargekoder. 
