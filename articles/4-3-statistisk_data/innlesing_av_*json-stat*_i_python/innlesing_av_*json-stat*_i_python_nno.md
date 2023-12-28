---
title: "Innlesing av *JSON-stat* i Python"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---

Me opprettar no fila `befolkning.json` og limer inn *JSON-stat*-objektet frå førre seksjon:

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

Det første steget er å leggja filinnhaldet i ein *dictionary*. Dette blir gjort med Python-pakken `json`:


```python
import json

with open("befolkning.json") as file:
    dataset = json.load(file)
```

Me skal no fordela dei ulike dataa i variablar, slik at me får litt betre oversikt. Som nemnt i førre seksjon består `JSON-stat`-objektet av metadata, dimensjonsdata og verdiar. Me veit at det finst to dimensjonar, og at me kan henta namnet til dimensjonane, som finst i attributtet "id":


```python
dim1_name = dataset["id"][0]
dim2_name = dataset["id"][1]
print(dim1_name)
print(dim2_name)
```

Kommune
Årstal


*Me bør eigentleg ta høgd for at datasettet kan ha fleire enn to dimensjonar, men for å forenkla presentasjonen skal me avgrensa oss til 2-dimensjonale datasett.*

Vidare kan me henta storleiken til dimensjonane, som finst i attributtet "size":


```python
dim1_size = dataset["size"][0]
dim2_size = dataset["size"][1]
print(dim1_size)
print(dim2_size)
```

    5
    10


I neste omgang kan me henta kategoriane i kvar dimensjon. For å henta kommunenamna, må me gå inn på attributta "dimension" -> "Kommune" -> "category" -> "label". Hugs at me ikkje bør skriva tekststrengen "Kommune" direkte, men heller bruka variabelen me definerte tidlegare, slik at programmet fungerer på andre `JSON-stat`-filer, der namna på dimensjonane antakeleg me vera noko anna! For å henta kommunenamna gjer me altså følgjande:


```python
dim1_categories = dataset["dimension"][dim1_name]["category"]["label"]
print(dim1_categories)
```

{'0101': 'Halden', '0104': 'Moss', '0105': 'Sarpsborg', '0106': 'Fredrikstad', '0602': 'Drammen'}


No kan me også henta rekkjefølgja av kommunar, som ligg i attributtet "index" i staden for "label":


```python
dim1_categories_index = dataset["dimension"][dim1_name]["category"]["index"]
print(dim1_categories_index)
```

    {'0101': 2, '0104': 3, '0105': 4, '0106': 1, '0602': 0}


For å henta kategoriane i den andre dimensjonen, altså "Årstall", gjer me i utgangspunktet akkurat det same:


```python
dim2_categories = dataset["dimension"][dim2_name]["category"]["label"]
dim2_categories_sorted = dataset["dimension"][dim2_name]["category"]["index"]
print(dim2_categories)
print(dim2_categories_sorted)
```

    {'14': '2014', '15': '2015', '16': '2016', '17': '2017', '18': '2018', '19': '2019', '20': '2020', '21': '2021', '22': '2022', '23': '2023'}
    ['14', '15', '16', '17', '18', '19', '20', '21', '22', '23']


Her ser me likevel at rekkjefølgja av årstal er gitt som ei sortert liste. Det kan vera nyttig å ha rekkjefølgja på same format som me hadde for kommunane.


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


Til slutt kan me leggja lista av verdiar i ein variabel:


```python
values = dataset["value"]
print(values)
```

    [96605, 97771, 98930, 99734, 100302, 100581, 101386, 101859, 102273, 103291, 77591, 78159, 78967, 80121, 80977, 81772, 82385, 83193, 83892, 84444, 30132, 30328, 30544, 30790, 31037, 31177, 31373, 31387, 31444, 31730, 46409, 47044, 47640, 48154, 48671, 48871, 49273, 49668, 50290, 51240, 54059, 54192, 54678, 55127, 55543, 55997, 56732, 57372, 58182, 59038]


No har me følgjande variablar:

* `dim1_navn`, `dim1_size`, `dim1_categories`, `dim1_categories_index`
* `dim2_navn`, `dim2_size`, `dim2_categories`, `dim2_categories_index`
* `values`

Sjekk gjerne at du veit kva desse variablane inneheld før du les vidare.

La oss seia at me ønskjer å henta befolkningstalet i Halden i 2016; me veit at denne verdien ligg i lista `values`, men korleis finn me den? For å repetera korleis lista av verdiar er sorterte, kan me først telja oss fram til den rette verdien:

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

Me finn altså den rette verdien på indeks 22:


```python
print(values[22])
```

    30544


Viss me studerer tabellen over, kjem me fram til følgjande reknestykke for å finna rett indeks:

$22$   
$= 2 \cdot 10 + 2$
$= (\text{antall kommuner før Halden}) \cdot (\text{antall årstall totalt}) \quad + \quad (\text{antall årstall før 2016})$
$= \ ($ `dim1_categories_index["0101"]` $- 1)\ \cdot$ `dim2_size` $\quad + \quad ($ `dim2_categories_index["16"]` $- 1)$

Denne siste linja kan me bruka for å skriva eit program som hentar rett verdi:


```python
desired_kommune = "0101"
desired_year = "16"

index = (dim1_categories_index[desired_kommune]) * dim2_size + (dim2_categories_index[desired_year])

print(index)
print(values[index])
```

    22
    30544


Me kan nå laga ein funksjon som finn rett indeks for eit kva som helst kommunenummer og årstal:


```python
def get_index(dim1_desired_category, dim2_desired_category):
    index = (dim1_categories_index[dim1_desired_category]) * dim2_size + (dim2_categories_index[dim2_desired_category])
    return index
```

Til slutt kan me laga ein funskjon som gir innbyggartalet for ein gitt kombinasjon av kommune og år:


```python
def get_population(kommunenummer, year): 
    index = get_index(kommunenummer, year)
    return values[index]
```

No kan me lett henta befolkningstalet som høyrer til følgjande kategoriar:

* Fredrikstad, 2018 ("0106", "18")
* Sarpsborg, 2014 ("0105", "14")
* Drammen, 2023 ("0602", "23")

Me treng berre å bruka funksjonen `get_population` med rette parametrar:


```python
print(get_population("0106", "18"))
print(get_population("0105", "14"))
print(get_population("0602", "23"))
```

    80977
    54059
    103291


**Aktivitetsforslag.** Ta utgangspunkt i *JSON-stat*-fila du laga i aktiviteten frå førre seksjon. Skriv ein funksjon som i dømet over; parametrane skal vera gitte kategoriar, og funksjonen skal returnera verdien som er tilknytta desse kategoriane.

