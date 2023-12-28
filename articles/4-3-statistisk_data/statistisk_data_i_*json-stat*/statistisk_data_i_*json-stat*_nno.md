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

Me skal no bruka *JSON-stat* til å registrera dataa i denne tabellen. Grunnidéen i *JSON-stat* er å gjera dataa *flate*. Det betyr rett og slett at me plasserer alle verdiane i ei liste:

```json
[ 
    96605,97771,98930,99734,100302,100581,101386,101859,102273,103291,
    77591,78159,78967,80121,80977,81772,82385,83193,83892,84444,
    30132,30328,30544,30790,31037,31177,31373,31387,31444,31730,
    46409,47044,47640,48154,48671,48871,49273,49668,50290,51240,
    54059,54192,54678,55127,55543,55997,56732,57372,58182,59038
]
```
Her har me brukt linjeskift slik at det framleis ser ut som ein tabell med rader og kolonnar, men eigentleg er det berre ei enkel liste med tal. No må me leggja til informasjon som gjer det mogleg å kopla verdiane til årstal og kommune; *JSON-stat* gir ei oppskrift for korleis me skal gjera dette.

Målet i denne seksjonen er å oppretta eit *JSON-stat*-objekt som inneheld befolkningsstatistikken. Eit *JSON-stat*-objekt har følgjande struktur:

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

*Du kan kopiera denne strukturen når du skal oppretta ditt eige *JSON-stat*-objekt.*

Me kan seia at *JSON-stat*-objektet består av tre delar:

- Metadata
- Dimensjonsdata
- Verdiar

**Metadata** er dei tre første linjene av objektet:

```json
"version": "2.0",
"class": "dataset",
"label": ""
```

Metadata blir brukt for å gi relevant bakgrunnsinformasjon; dei to første attributta er obligatoriske og fortel kva utgåve av *JSON-stat* me bruker. Det siste attributtet er valfritt og blir brukt for å gi ein tittel til statistikken:

```json 
"label": "Befolkningstall i fem kommuner i perioden 2014-2023"
```

Det finst andre valfrie attributt me kan leggja til for å gi bakgrunnsinformasjon om statistikken.

**Dimensjonsdata** gir informasjon som koplar talverdiane til *kategoriar*. Når me har fylt inn dimensjonsdata, vil det til dømes vera mogleg å kopla den 37. verdien  til kategoriane "2021" og "Fredrikstad".

Dimensjonsdataa består av attributta "id", "size" og "dimension". I attributtet "dimension"  finn me eit nytt objekt med ein spesifikk struktur, som me skal forklara nøye i denne seksjonen.

For å registrera **verdiar** blir brukt attributtet "value", som skal innehalda ei liste av verdiar:

```json
"value": [ 
    96605,97771,98930,99734,100302,100581,101386,101859,102273,103291,
    77591,78159,78967,80121,80977,81772,82385,83193,83892,84444,
    30132,30328,30544,30790,31037,31177,31373,31387,31444,31730,
    46409,47044,47640,48154,48671,48871,49273,49668,50290,51240,
    54059,54192,54678,55127,55543,55997,56732,57372,58182,59038
]
```

Den enklaste oppgåva er altså å registrera alle verdiane! Det som står att er dimensjonsdataa, som koplar verdiane til rette kategoriar. Kvar verdi kan koplast til éin kommune og eitt årstal; derfor seier me at "Kommune" og "Årstall" er *dimensjonane* til datasettet. For å registrera dimensjonane bruker me attributtet "id":

```json
"id": ["Kommune", "Årstall"]
```

Dataa vårt har altså to dimensjonar, men det finst inga avgrensing på talet på dimensjonar. Tenk deg at at tabellen inneheldt talet på mennn og talet på kvinner i kvar kolonne. Då ville tabellen hatt dobbelt så mange verdiar, og me kunne sagt at kvar verdi kan koplast til ein kommune, eit årstal og eit kjønn.  Me ville altså hatt tre dimensjonar, og lista av dimensjonar kunne vore skrive som `["Kommune", "Årstall", "Kjønn"]`.

Vidare må me oppretta attributtet "size", som fortel talet på kategoriar i kvar dimensjon:

```json
"id": ["Kommune", "Årstall"]
"size": [5, 10]
```

Den første dimensjonen har 5 *kategoriar* (fem kommunar) den andre dimensjonen har 10 *kategoriar* (ti årstal).

Vidare må me fortelja kva som er kategoriane i kvar dimensjon, og til dette blir attributtet brukt "dimension". Me byrjar med kategoriane i "Kommune":

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

Her ser me at kvar kategori må ha både ein nøkkel og eit namn. Det er fordi to kategoriar i prinsippet kan ha same namn, og då må dei kunna skiljast med unike nøklar. Her har me brukt [kommunenummer](https://snl.no/kommunenummer) som nøklar, fordi me veit at kvar kommune har eit unikt kommunenummer.

Du lurer kanskje på kva som er poenget med alle attributta som *JSON-stat* krev?

* Poenget med nøkkelen "dimension" er å fortelja at i dette attributtet finn ein informasjon om dimensjonane.
* Poenget med nøkkelen "Kommune" er å fortelja at i dette attributtet finn ein informasjon om dimensjonen "Kommune".
* Poenget med nøklane "category" og "label" er å spesifisera **kva** informasjon me gir om dimensjonen "Kommune". I dette tilfellet ønskjer me å lista *kategoriane* i dimensjonen, og me ønskjer å gi *namn* (*label*) til kvar kategori.

La oss no lista kategoriane i "Årstall" på akkurat same måte:

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

La oss samanfatta det me har gjort før me går vidare:

* Registrert at første dimensjon er "Kommune" og at andre dimensjon er "Årstall".
* Registrert namnet til alle kategoriane, det vil seia dei fem kommunane og dei ti årstala.

Er me ferdige? Nei, for me må også fortelja korleis lista av verdiar er sorterte, altså kva som er rekkjefølgja av kommunar og årstal. Det skal me sjå på i neste seksjon!

