---
title: "Innlasting av *JSON*-filer i Python"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

Tenk deg at du har *JSON*-fila `person.json` med følgjande innhald:

```json
{
    "fornavn": "Kari",
    "etternavn": null,
    "alder": 42, 
    "interesser": ["sjakk", "fotografering"],
    "bolig": {
        "type": "leilighet", 
        "størrelse": 100, 
        "sted": "Trondheim"}, 
    "harHusdyr": true
}
```

Korleis kan me leggja desse verdiane i ein variabel i Python? Dersom du har lese førre seksjon, ser du kanskje at eit *JSON*-objekt i praksis er det same som ein *dictionary* i Python? Me ønskjer altså at dataa ovanfor skal leggjast i ein dictionary, og at me deretter kan bruka nøklane til å henta spesifikke verdiar.

For å importera ein *JSON*-fil kan me bruka følgjande kode:


```python
import json
my_file = open("person.json")
my_string = my_file.read()
my_dict = json.loads(my_string)

print(my_dict)
```

{'førenamn': 'Kari', 'etternamn': None, 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'bustad': {'type': 'leilegheit', 'storleik': 100, 'stad': 'Trondheim'}, 'harHusdyr': Tru}


*Funksjonen `json.loads` tek ein tekststreng som parameter og prøver å tolka denne som ein dictionary.*

No har me lagt dataa i ein dictionary som har akkurat same struktur som *JSON*-objektet. Me kan no gjera endra nokre spesifikke verdiar:


```python
old_age = my_dict["alder"] 
new_age = old_age + 10
my_dict["alder"] = new_age
my_dict["interesser"].append("fuglekikking")

print(my_dict)
```

{'førenamn': 'Kari', 'etternamn': None, 'alder': 52, 'interesser': ['sjakk', 'fotografering', 'fuglekikking'], 'bustad': {'type': 'leilegheit', 'storleik': 100, 'stad': 'Trondheim'}, 'harHusdyr': Tru}


Hugs at desse endringane berre finst i variabelen `my_dict`, som er mellombels lagra i minnet til datamaskina når me køyrer programmet. For å lagra dataa permanent, kan me leggja dei i ein *JSON*-fil. I starten av seksjonen importerte me frå *JSON* til dictionary, og no skal me gå den andre vegen. Me byrjar med å konvertera frå dictionary til ein tekststreng:


```python
my_new_string = json.dumps(my_dict, indent=4)
print(my_new_string)
```

    {
"førenamn": "Kari",
"etternamn": null,
"alder": 52
"interesser": [
"sjakk",
"fotografering",
"fuglekikking"
        ],
"bustad": {
"type": "leilegheit",
"st\u00f8rrelse": 100
"stad": "Trondheim"
        },
"harHusdyr": tru
    }


*Merk korleis funksjonen `json.dumps` sørgjer for fin formatering når me bruker tilleggsparameteren `indent=4`. Dette er også nyttig dersom me jobbar med ein stor dictionary og ønskjer å få ei betre oversikt over strukturen.*

No kan me leggja tekststrengen i ein *JSON*-fil:


```python
new_file = open('person_new.json', 'w+')
new_file.write(my_new_string)
new_file.close()
```

For å samanfatta, så har me importert fila `person.json`, gjort nokre endringar, og lagra dei nye dataa under filnamnet `person_new.json`. Me kunne også ha overskrevet den gamle fila med dei nye dataa.

**Aktivitetsforslag.** Ta utgangspunkt i *JSON*-fila du oppretta i *Aktivitetsforslag 1* eller *2* frå seksjonen *Struktur av JSON-filer*. Last inn filene i Python, og prøv deretter å gjera nokre endringar på dataa. Lager til slutt dei oppdaterte datane i ein ny *JSON*-fil (eller overskriv den gamle fila).
