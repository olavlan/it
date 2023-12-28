---
title: "Dictionary i Python"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

Du er antagelig vant til å bruke lister i Python:


```python
my_list = ["Oslo", "Tønsberg", "Mandal", "Hammerfest"]
```

Hvert element i lista har en unik *indeks*: 

```
0: "Oslo"
1: "Tønsberg"
2: "Mandal"
3: "Hammerfest"
```

Disse indeksene gjør at vi kan finne igjen spesifikke elementer i lista: 


```python
a = my_list[0]
b = my_list[2]

print(a)
print(b)
```

    Oslo
    Mandal


Vi kan si at 0 er *nøkkelen* som gir oss det første elementet i lista, altså "Oslo". I en liste må vi bruke heltallene $0, 1, 2, 3, ...$ som nøkler. Men hva om vi ønsker å bruke andre nøkler, som for eksempel:

```
"hovedstad": "Oslo"
"eldst": "Tønsberg"
"sørligst": "Mandal"
"nordligst": "Hammerfest"
```

Vi kan gjøre dette ved å bruke en *dictionary*. For å opprette en dictionary bruker vi krøllparentesene `{}`, og hver verdi må tilknyttes en nøkkel:


```python
my_dict = {"hovedstad": "Oslo", "eldst": "Tønsberg", "sørligst": "Mandal", "nordligst": "Hammerfest"}
```

Nå kan vi hente verdier ved å bruke våre egendefinerte nøkler: 


```python
a = my_dict["hovedstad"]
b = my_dict["sørligst"]

print(a)
print(b)
```

    Oslo
    Mandal


La oss se på et annet eksempel. I Python kan elementene i en liste være hva som helst, også nye lister:


```python
person = ["Kari", None, 42, ["sjakk", "fotografering"], ["leilighet", 100, "Trondheim"], True]
```

Denne listen er ment å gi informasjon om en person, men det er uklart hva de ulike verdiene betyr. I tillegg må vi bruke tallindekser for å hente ut spesifikke verdier:


```python
bosted = person[4][2]
print(bosted)
```

    Trondheim


Her er det mye mer hensiktsmessig å bruke en dictionary, fordi vi kan legge inn verdiene med nøkler: 


```python
person = {"fornavn": "Kari", "alder": 42}
```

Igjen kan vi tenke på nøklene "fornavn" og "alder" som egendefinerte indekser. I en liste ville indeksene vært 0 og 1, mens i en dictionary kan vi bruke valgfrie tekststrenger. Deretter kan vi "slå opp" på disse strengene for å hente verdiene vi ønsker. En dictionary er altså et slags oppslagsverk, akkurat som navnet antyder.

For å legge inn flere verdier i en dictionary trenger vi bare å opprette nye nøkler: 


```python
person["interesser"] = ["sjakk", "fotografering"]
person["harHusdyr"] = True
print(person)
```

    {'fornavn': 'Kari', 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'harHusdyr': True}


Vi kan legge inn hva som helst, til og med en ny dictionary:


```python
person["bolig"] = {"type": "leilighet", "størrelse": 100, "sted": "Trondheim"}
print(person)
```

    {'fornavn': 'Kari', 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'harHusdyr': True, 'bolig': {'type': 'leilighet', 'størrelse': 100, 'sted': 'Trondheim'}}


For å hente verdien "Trondheim", må vi først gå inn på nøkkelen "bolig", og deretter på nøkkelen "sted":


```python
print(person["bolig"]["sted"])
```

    Trondheim


Det er ikke noe i veien for å opprette en liste der hvert element er en dictionary:


```python
person1 = {"navn": "Ola Nordmann", "alder": 17}
person2 = {"navn": "Kari Hansen", "alder": 42}
person3 = {"navn": "Per Hansen", "alder": 64}

people = [person1, person2, person3]
```

For å hente spesifikke verdier kan vi bruke en blanding av tallindekser og nøkler: 


```python
name = people[2]["navn"]
print(name)
```

    Per Hansen


Vi kan også gå gjennom lista med en løkke:


```python
for person in people:
    print(person["navn"])
```

    Ola Nordmann
    Kari Hansen
    Per Hansen


Hva hadde skjedd hvis en dictionary manglet nøkkelen "navn"? Da ville vi fått en feilmelding! Derfor må vi være sikre på at de samme nøklene finnes i hver dictionary. Sagt på en annen måte bør lista inneholde objekter av samme type. I vårt eksempel har vi en liste av personobjekter. 

For å oppsummere kan vi si at data bør legges i en dictionary når vi ønsker å slå opp spesifikke verdier. En liste er kun egnet dersom hvert element er av samme type og vi skal gjøre den samme operasjonen på hvert element (ved å bruke en løkke). 

Vi har også sett at en liste kan inneholde dictionary-elementer, og en dictionary kan inneholde lister!

**Aktivitetsforslag.** Ta utgangspunkt i *Aktivitetsforslag 1* eller *2* fra seksjonen *Struktur av JSON-filer*. Legg alle eller deler av dataene i en dictionary (eventuelt en liste der hvert element er en dictionary). Sørg for at dataene er strukturert på samme måte, med de samme nøklene. Forsøk deretter å hente noen spesifikke verdier, og eksperimenter også med løkker dersom du har lister. 

