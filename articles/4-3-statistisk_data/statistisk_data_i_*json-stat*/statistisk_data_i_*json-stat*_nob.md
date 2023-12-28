---
title: "Statistisk data i *JSON-stat*"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---

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

