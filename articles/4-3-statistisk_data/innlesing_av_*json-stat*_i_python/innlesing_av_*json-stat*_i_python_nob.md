---
title: "Innlesing av *JSON-stat* i Python"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---

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

