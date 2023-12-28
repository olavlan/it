---
title: "Innlasting av *JSON*-filer i Python"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

Tenk deg at du har *JSON*-filen `person.json` med følgende innhold: 

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

Hvordan kan vi legge disse verdiene i en variabel i Python? Dersom du har lest forrige seksjon, ser du kanskje at et *JSON*-objekt i praksis er det samme som en *dictionary* i Python? Vi ønsker altså at dataene ovenfor skal legges i en dictionary, og at vi deretter kan bruke nøklene til å hente spesifikke verdier.

For å importere en *JSON*-fil kan vi bruke følgende kode:


```python
import json
my_file = open("person.json")
my_string = my_file.read()
my_dict = json.loads(my_string)

print(my_dict)
```

    {'fornavn': 'Kari', 'etternavn': None, 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'bolig': {'type': 'leilighet', 'størrelse': 100, 'sted': 'Trondheim'}, 'harHusdyr': True}


*Funksjonen `json.loads` tar en tekststreng som parameter og forsøker å tolke denne som en dictionary.*

Nå har vi lagt dataene i en dictionary som har akkurat samme struktur som *JSON*-objektet. Vi kan nå gjøre endre noen spesifikke verdier: 


```python
old_age = my_dict["alder"] 
new_age = old_age + 10
my_dict["alder"] = new_age
my_dict["interesser"].append("fuglekikking")

print(my_dict)
```

    {'fornavn': 'Kari', 'etternavn': None, 'alder': 52, 'interesser': ['sjakk', 'fotografering', 'fuglekikking'], 'bolig': {'type': 'leilighet', 'størrelse': 100, 'sted': 'Trondheim'}, 'harHusdyr': True}


Husk at disse endringene kun finnes i variabelen `my_dict`, som er midlertidig lagret i datamaskinens minne når vi kjører programmet. For å lagre dataene permanent, kan vi legge dem i en *JSON*-fil. I starten av seksjonen importerte vi fra *JSON* til dictionary, og nå skal vi gå den andre veien. Vi begynner med å konvertere fra dictionary til en tekststreng:


```python
my_new_string = json.dumps(my_dict, indent=4)
print(my_new_string)
```

    {
        "fornavn": "Kari",
        "etternavn": null,
        "alder": 52,
        "interesser": [
            "sjakk",
            "fotografering",
            "fuglekikking"
        ],
        "bolig": {
            "type": "leilighet",
            "st\u00f8rrelse": 100,
            "sted": "Trondheim"
        },
        "harHusdyr": true
    }


*Merk hvordan funksjonen `json.dumps` sørger for pen formatering når vi bruker tilleggsparameteren `indent=4`. Dette er også nyttig dersom vi jobber med en stor dictionary og ønsker å få en bedre oversikt over strukturen.*

Nå kan vi legge tekststrengen i en *JSON*-fil:


```python
new_file = open('person_new.json', 'w+')
new_file.write(my_new_string)
new_file.close()
```

For å oppsummere, så har vi importert filen `person.json`, gjort noen endringer, og lagret de nye dataene under filnavnet `person_new.json`. Vi kunne også ha overskrevet den gamle filen med de nye dataene. 

**Aktivitetsforslag.** Ta utgangspunkt i *JSON*-filen du opprettet i *Aktivitetsforslag 1* eller *2* fra seksjonen *Struktur av JSON-filer*. Last inn filene i Python, og forsøk deretter å gjøre noen endringer på dataene. Lagre til slutt de oppdaterte datene i en ny *JSON*-fil (eller overskriv den gamle filen). 
