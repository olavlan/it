---
title: "Dictionary i Python"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

Du er antakeleg vand til å bruka lister i Python:


```python
my_list = ["Oslo", "Tønsberg", "Mandal", "Hammerfest"]
```

Kvart element i lista har ein unik *indeks*:

```
0: "Oslo"
1: "Tønsberg"
2: "Mandal"
3: "Hammerfest"
```

Desse indeksane gjer at me kan finna igjen spesifikke element i lista:


```python
a = my_list[0]
b = my_list[2]

print(a)
print(b)
```

Oslo
Mandal


Me kan seia at 0 er *nøkkelen* som gir oss det første elementet i lista, altså "Oslo". I ei liste må me bruka heiltala $0, 1, 2, 3, ...$ som nøklar. Men kva om me ønskjer å bruka andre nøklar, som til dømes:

```
"hovedstad": "Oslo"
"eldst": "Tønsberg"
"sørligst": "Mandal"
"nordligst": "Hammerfest"
```

Me kan gjera dette ved å bruka ein *dictionary*. For å oppretta ein dictionary bruker me krøllparentesane `{}`, og kvar verdi må knytast til ein nøkkel:


```python
my_dict = {"hovedstad": "Oslo", "eldst": "Tønsberg", "sørligst": "Mandal", "nordligst": "Hammerfest"}
```

No kan me henta verdiar ved å bruka dei eigendefinerte nøklane våre:


```python
a = my_dict["hovedstad"]
b = my_dict["sørligst"]

print(a)
print(b)
```

Oslo
Mandal


La oss sjå på eit anna døme. I Python kan elementa i ei liste vera kva som helst, også nye lister:


```python
person = ["Kari", None, 42, ["sjakk", "fotografering"], ["leilighet", 100, "Trondheim"], True]
```

Denne lista er meint å gi informasjon om ein person, men det er uklart kva dei ulike verdiane betyr. I tillegg må me bruka talindeksar for å henta ut spesifikke verdiar:


```python
bosted = person[4][2]
print(bosted)
```

Trondheim


Her er det mykje meir formålstenleg å bruka ein dictionary, fordi me kan leggja inn verdiane med nøklar:


```python
person = {"fornavn": "Kari", "alder": 42}
```

Igjen kan me tenkja på nøklane "førenamn" og "alder" som eigendefinerte indeksar. I ei liste ville indeksane vore 0 og 1, medan i ein dictionary kan me bruka valfrie tekststrenger. Deretter kan me "slå opp" på desse strengene for å henta verdiane me ønskjer. Ein dictionary er altså eit slags oppslagsverk, akkurat som namnet antydar.

For å leggja inn fleire verdiar i ein dictionary treng me berre å oppretta nye nøklar:


```python
person["interesser"] = ["sjakk", "fotografering"]
person["harHusdyr"] = True
print(person)
```

{'førenamn': 'Kari', 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'harHusdyr': Tru}


Me kan leggja inn kva som helst, til og med ein ny dictionary:


```python
person["bolig"] = {"type": "leilighet", "størrelse": 100, "sted": "Trondheim"}
print(person)
```

{'førenamn': 'Kari', 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'harHusdyr': Tru, 'bustad': {'type': 'leilegheit', 'storleik': 100, 'stad': 'Trondheim'}}


For å henta verdien "Trondheim", må me først gå inn på nøkkelen "bustad", og deretter på nøkkelen "stad":


```python
print(person["bolig"]["sted"])
```

Trondheim


Det er ikkje noko i vegen for å oppretta ei liste der kvart element er ein dictionary:


```python
person1 = {"navn": "Ola Nordmann", "alder": 17}
person2 = {"navn": "Kari Hansen", "alder": 42}
person3 = {"navn": "Per Hansen", "alder": 64}

people = [person1, person2, person3]
```

For å henta spesifikke verdiar kan me bruka ei blanding av talindeksar og nøklar:


```python
name = people[2]["navn"]
print(name)
```

Per Hansen


Me kan også gå gjennom lista med ei løkke:


```python
for person in people:
    print(person["navn"])
```

Ola Nordmann
Kari Hansen
Per Hansen


Kva hadde skjedd viss ein dictionary mangla nøkkelen "namn"? Då ville me fått ei feilmelding! Derfor må me vera sikre på at dei same nøklane finst i kvar dictionary. Sagt på ein annan måte bør lista innehalda objekt av same type. I vårt døme har me ei liste av personobjekt.

For å samanfatta kan me seia at data bør leggjast i ein dictionary når me ønskjer å slå opp spesifikke verdiar. Ei liste er berre eigna dersom kvart element er av same type og me skal gjera den same operasjonen på kvart element (ved å bruka ei løkke).

Me har også sett at ei liste kan innehalda dictionary-elementer, og ein dictionary kan innehalda lister!

**Aktivitetsforslag.** Ta utgangspunkt i *Aktivitetsforslag 1* eller *2* frå seksjonen *Struktur av JSON-filer*. Legg alle eller delar av dataa i ein dictionary (eventuelt ei liste der kvart element er ein dictionary). Sørg for at dataa er strukturerte på same måte, med dei same nøklane. Prøv deretter å henta nokre spesifikke verdiar, og eksperiment også med løkker dersom du har lister.

