---
title: "Handtering av dato og tid"
belongs_to_chain: "Databehandling"
figures_to_include:
---

Tenk deg at me ønskjer å finna ut kor mange som syklar mellom 7 og 10 på kvardagar. Då må me gå gjennom alle sykkelturar, og trekkja ut turane som tilfredsstiller krava.

La oss først sjekka om ein spesifikk tur tilfredsstiller krava:


```python
print(json.dumps(trips[800], indent=4))
```

    {
"started_at": "2023-07-01 09:32:13.801000+00:00",
"ended_at": "2023-07-01 09:33:45.726000+00:00",
"duration": 91
"start_station_id": "449",
"start_station_name": "Rusel\u00f8kkg\u00e5rden",
"start_station_description": "langs L\u00f8kkeveien",
"start_station_latitude": 59.91357497092093
"start_station_longitude": 10.726229742333288
"end_station_id": "449",
"end_station_name": "Rusel\u00f8kkg\u00e5rden",
"end_station_description": "langs L\u00f8kkeveien",
"end_station_latitude": 59.91357497092093
"end_station_longitude": 10.726229742333288
    }


Kva må me få programmet vårt til å gjera? Me må sjekka om datostrengen *2023-07-01 09:32:13.801000+00:00* tilfredsstiller krava, nemleg at det er ein kvardag og mellom klokka 7 og 10!

Korleis trekkjer me informasjon ut av datostrengen? Til dømes kan me enkelt henta årstalet:


```python
my_date_string = "2023-07-01 09:32:13.801000+00:00"
year = int(my_date_string[:4])
print(year)
```

    2023


Her har me henta ut dei fire første teikna i datostrengen, og konvertert det til eit heiltal. Denne metoden vil alltid fungera, fordi alle datostrengne er skrive i same format. Å henta ut informasjon frå strenger blir kalla *parsing*.

Det finst mange Python-pakkar som kan brukast til parsing av bestemde format. Ved å søkja etter *python parse data and time*, vil du antakeleg komma over pakken [*datetime*](https://docs.python.org/3/library/datetime.html).

Ein vanleg virkemåte for slike pakkar er å  konvertera ein streng til eit objekt. I vårt tilfelle kan me bruka *datetime* til å konvertera ein datostreng til eit Python-objekt:


```python
from datetime import datetime
my_date_object = datetime.fromisoformat("2023-07-01 09:32:13.801000+00:00")
```

Eit Python-objekt er kort sagt ei eining som består av variablar og funksjonar. Objektet `my_date_object` består til dømes av følgjande variablar:


```python
print(my_date_object.year)
print(my_date_object.month)
print(my_date_object.day)
print(my_date_object.hour)
print(my_date_object.minute)
```

    2023
    7
    1
    9
    32


Objektet har også funksjonar som utfører operasjonar på desse variablane. Det finst ein funksjon som reknar ut vekedagen til datostrengen:


```python
print(my_date_object.weekday())
```

    5


Her må me lesa [dokumentasjonen](https://docs.python.org/3/library/datetime.html#datetime.datetime.weekday) for å forstå at vekedagane er nummererte frå 0 til 6. Talet 5 betyr altså laurdag, så me kan konkludera med at denne spesifikke turen ikkje skjedde på ein kvardag!

No kan me gå gjennom alle sykkelturar og dela dei inn i to lister, avhengig av om turen skjedde på kvardag eller helg:


```python
weekday_trips = []
weekend_trips = []

n = len(trips)
for i in range(n):
    date_string = trips[i]["started_at"]
    date_object = datetime.fromisoformat(date_string)
    if date_object.weekday() < 5: 
        weekday_trips.append(i)
    else:
        weekend_trips.append(i)

print(weekday_trips[:10])
print(weekend_trips[:10])
```

    [6989, 6990, 6991, 6992, 6993, 6994, 6995, 6996, 6997, 6998]
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]


Her har me laga to lister, `weekday_trips` og `weekend_trips`, og me har skrive ut dei ti første turane i kvar liste. I desse listene har me berre lagra indeksen til turane. Kvifor det? Vel, dersom me ønskjer meir informasjon om ein bestemd tur i lista, til dømes tur nummer 6989, kan me alltid henta dette i variabelen `trips`:


```python
print(trips[6989])
```

{'started_at': '2023-07-03 03:06:45.130000+00:00', 'ended_at': '2023-07-03 03:13:54.871000+00:00', 'duration': 429, 'start_station_id': '403', 'start_station_name': 'Parkveien', 'start_station_description': 'ved trikkestoppet', 'start_station_latitude': 59.921768, 'start_station_longitude': 10.730476, 'end_station_id': '609', 'end_station_name': 'Fred Olsens gate', 'end_station_description': 'ved Karl Johans gate', 'end_station_latitude': 59.9110506, 'end_station_longitude': 10.7493737}


No bruker me same metode til å henta alle turar som starta mellom 7 og 10:


```python
morning_trips = []

n = len(trips)
for i in range(n):
    date_string = trips[i]["started_at"]
    date_object = datetime.fromisoformat(date_string)
    if date_object.hour >= 7 and date_object.hour <= 10: 
        morning_trips.append(i)

print(morning_trips[:10])
```

    [190, 191, 192, 193, 194, 195, 196, 197, 198, 199]


Målet vårt var å henta alle turar som starta på ein kvardag mellom 7 og 10. Då må me henta turane som er i både-og `weekday_trips`  i `morning_trips`! Dette kan gjerast effektivt viss me først konverterer listene til *mengder* (*sets* på engelsk):


```python
weekday_trips = set(weekday_trips)
morning_trips = set(morning_trips)
```

*Ei mengd er det same som ei liste, bortsett frå at ho er usortert.*

No kan me bruka operasjonen `&`, som hentar alle element som finst i **begge** mengdene:


```python
weekday_morning_trips = weekday_trips & morning_trips
```

Resultatet er ei ny mengd, og me kan konvertera denne tilbake til ei liste:


```python
weekday_morning_trips = list(weekday_morning_trips)
print(weekday_morning_trips[:10])
```

    [114883, 127533, 127388, 127909, 114884, 127389, 127910, 114885, 128117, 127390]


Så kor mange turar vart gjorde mellom 7 og 10 på kvardagar?


```python
k = len(weekday_morning_trips)
n = len(trips)

print(k)
print(n)
print(k/n)
```

    18763
    131381
    0.14281364885333495


Her ser me at 18.763 turar vart gjorde på kvardagar mellom 7 og 10, og at dette utgjer omtrent 14.3 % av alle turar.

**Fordeling av turar på vekedagar.** Korleis kan me telja talet på turar som skjedde på måndag, tysdag, onsdag, og resten av vekedagane? Me kan ta utgangspunkt i følgjande dictionary:


```python
counts = {
    0: 0,
    1: 0,
    2: 0,
    3: 0,
    4: 0,
    5: 0,
    6: 0
}
```

Me har eitt attributt for kvar dag; 0 for måndag, 1 for tysdag, og så vidare. Me ønskjer at verdien til attributtet skal vera talet på turar som skjedde på den aktuelle dagen. Då må me gå gjennom alle turar, og for kvar tur må me auka verdien til den rette nøkkelen:


```python
for t in trips:
    date_string = t["started_at"]
    date_object = datetime.fromisoformat(date_string)
    weekday = date_object.weekday()
    counts[weekday] += 1

print(counts)
```

    {0: 21259, 1: 18696, 2: 19305, 3: 18998, 4: 19367, 5: 19005, 6: 14751}


Den mest populære dagen er altså måndag, med 21259 turar. Me kan konvertera desse tala til prosentdelar ved å dela på det samla talet turar:


```python
percentages = {}
n = len(trips)

for k in counts.keys():
    percentages[k]= counts[k]/n

print(percentages)
```

    {0: 0.1618118297166257, 1: 0.14230368165868734, 2: 0.14693905511451427, 3: 0.14460233975993483, 4: 0.14741096505582998, 5: 0.14465561991459952, 6: 0.11227650877980834}


Her ser me at omtrent 16.2 % av turane skjer på måndagar, medan 11.2 % av turane skjer på søndagar.

**Oppsummering.** I denne seksjonen har me lært følgjande:
- *Parsing* er å henta ut informasjon frå strenger som er skrive i eit strukturert format.
- Det finst Python-pakkar for parsing av kjende strengformat.
- Python-pakken *datetime* kan brukast til å henta informasjon frå ein standard datostreng, som til dømes *2023-07-03 03:06:45.130000+00:00*.

I vårt døme brukte me *datetime* til å henta sykkelturar som starta mellom 7 og 10 på ein kvardag, og dessutan å telja talet på sykkelturar for kvar vekedag.

**Aktivitetsforslag 1.**

1. Opprett variabelen `evening_weekend_trips`, som skal vera ei liste over alle turar som vart gjorde på kveldstid i helgar, det vil seia mellom 20 og 24 på anten fredag, laurdag eller søndag. Lista treng berre å innehalda indeksen til dei aktuelle turane.
2. Kor mange slike turar finst og kor stor prosentdel utgjer dei?
3. Kva er gjennomsnittleg varigheit for slike turar?

**Aktivitetsforslag 2.** Kva er gjennomsnittleg varigheit for kvardagsturar? Og for helgesturer? Kva trur du forskjellen kjem av?

**Aktivitetsforslag 3.**
1. Tell talet på sykkelturar som starta på kvar av klokketimane, det vil seia 0, 1, 2, 3 og opp til 23. Kva klokketime har flest og færrast sykkelturar? Vis fordelinga i prosent.
2. Korleis fordeler turane seg på følgjande periodar av dagen?
* Natt: kl. 0-5
* Morgon: kl. 6-11
* Ettermiddag: kl. 12-17
* Kveld: kl. 18-23

