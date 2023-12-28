---
title: "Håndtering av dato og tid"
belongs_to_chain: "Databehandling"
figures_to_include:
---

Tenk deg at vi ønsker å finne ut hvor mange som sykler mellom 7 og 10 på hverdager. Da må vi gå gjennom alle sykkelturer, og trekke ut turene som tilfredsstiller kravene. 

La oss først sjekke om en spesifikk tur tilfredsstiller kravene:


```python
print(json.dumps(trips[800], indent=4))
```

    {
        "started_at": "2023-07-01 09:32:13.801000+00:00",
        "ended_at": "2023-07-01 09:33:45.726000+00:00",
        "duration": 91,
        "start_station_id": "449",
        "start_station_name": "Rusel\u00f8kkg\u00e5rden",
        "start_station_description": "langs L\u00f8kkeveien",
        "start_station_latitude": 59.91357497092093,
        "start_station_longitude": 10.726229742333288,
        "end_station_id": "449",
        "end_station_name": "Rusel\u00f8kkg\u00e5rden",
        "end_station_description": "langs L\u00f8kkeveien",
        "end_station_latitude": 59.91357497092093,
        "end_station_longitude": 10.726229742333288
    }


Hva må vi få programmet vårt til å gjøre? Vi må sjekke om datostrengen *2023-07-01 09:32:13.801000+00:00* tilfredsstiller kravene, nemlig at det er en hverdag og mellom klokken 7 og 10!

Hvordan trekker vi informasjon ut av datostrengen? For eksempel kan vi enkelt hente årstallet:


```python
my_date_string = "2023-07-01 09:32:13.801000+00:00"
year = int(my_date_string[:4])
print(year)
```

    2023


Her har vi hentet ut de fire første tegnene i datostrengen, og konvertert det til et heltall. Denne metoden vil alltid fungere, fordi alle datostrengne er skrevet i samme format. Å hente ut informasjon fra strenger kalles *parsing*. 

Det finnes mange Python-pakker som kan brukes til parsing av bestemte formater. Ved å søke etter *python parse date and time*, vil du antagelig komme over pakken [*datetime*](https://docs.python.org/3/library/datetime.html). 

En vanlig virkemåte for slike pakker er å  konvertere en streng til et objekt. I vårt tilfelle kan vi bruke *datetime* til å konvertere en datostreng til et Python-objekt: 


```python
from datetime import datetime
my_date_object = datetime.fromisoformat("2023-07-01 09:32:13.801000+00:00")
```

Et Python-objekt er kort sagt en enhet som består av variabler og funksjoner. Objektet `my_date_object` består for eksempel av følgende variabler: 


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


Objektet har også funksjoner som utfører operasjoner på disse variablene. Det finnes en funksjon som regner ut ukedagen til datostrengen:


```python
print(my_date_object.weekday())
```

    5


Her må vi lese [dokumentasjonen](https://docs.python.org/3/library/datetime.html#datetime.datetime.weekday) for å forstå at ukedagene er nummerert fra 0 til 6. Tallet 5 betyr altså lørdag, så vi kan konkludere med at denne spesifikke turen ikke skjedde på en hverdag!

Nå kan vi gå gjennom alle sykkelturer og dele dem inn i to lister, avhengig av om turen skjedde på hverdag eller helg:


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


Her har vi laget to lister, `weekday_trips` og `weekend_trips`, og vi har printet ut de ti første turene i hver liste. I disse listene har vi kun lagret indeksen til turene. Hvorfor det? Vel, dersom vi ønsker mer informasjon om en bestemt tur i listen, for eksempel tur nummer 6989, kan vi alltid hente dette i variabelen `trips`:


```python
print(trips[6989])
```

    {'started_at': '2023-07-03 03:06:45.130000+00:00', 'ended_at': '2023-07-03 03:13:54.871000+00:00', 'duration': 429, 'start_station_id': '403', 'start_station_name': 'Parkveien', 'start_station_description': 'ved trikkestoppet', 'start_station_latitude': 59.921768, 'start_station_longitude': 10.730476, 'end_station_id': '609', 'end_station_name': 'Fred Olsens gate', 'end_station_description': 'ved Karl Johans gate', 'end_station_latitude': 59.9110506, 'end_station_longitude': 10.7493737}


Nå bruker vi samme metode til å hente alle turer som startet mellom 7 og 10:


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


Målet vårt var å hente alle turer som startet på en hverdag mellom 7 og 10. Da må vi hente turene som er i både `weekday_trips` og i `morning_trips`! Dette kan gjøres effektivt hvis vi først konverterer listene til *mengder* (*sets* på engelsk): 


```python
weekday_trips = set(weekday_trips)
morning_trips = set(morning_trips)
```

*En mengde er det samme som en liste, bortsett fra at den er usortert.*

Nå kan vi bruke operasjonen `&`, som henter alle elementer som finnes i **begge** mengdene:


```python
weekday_morning_trips = weekday_trips & morning_trips
```

Resultatet er en ny mengde, og vi kan konvertere denne tilbake til en liste:


```python
weekday_morning_trips = list(weekday_morning_trips)
print(weekday_morning_trips[:10])
```

    [114883, 127533, 127388, 127909, 114884, 127389, 127910, 114885, 128117, 127390]


Så hvor mange turer ble gjort mellom 7 og 10 på hverdager? 


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


Her ser vi at 18.763 turer ble gjort på hverdager mellom 7 og 10, og at dette utgjør omtrent 14.3 % av alle turer. 

**Fordeling av turer på ukedager.** Hvordan kan vi telle antall turer som skjedde på mandag, tirsdag, onsdag, og resten av ukedagene? Vi kan ta utgangspunkt i følgende dictionary: 


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

Vi har én attributt for hver dag; 0 for mandag, 1 for tirsdag, og så videre. Vi ønsker at verdien til attributtet skal være antall turer som skjedde på den aktuelle dagen. Da må vi gå gjennom alle turer, og for hver tur må vi øke verdien til den riktige nøkkelen: 


```python
for t in trips:
    date_string = t["started_at"]
    date_object = datetime.fromisoformat(date_string)
    weekday = date_object.weekday()
    counts[weekday] += 1

print(counts)
```

    {0: 21259, 1: 18696, 2: 19305, 3: 18998, 4: 19367, 5: 19005, 6: 14751}


Den mest populære dagen er altså mandag, med 21259 turer. Vi kan konvertere disse tallene til prosentandeler ved å dele på totalt antall turer: 


```python
percentages = {}
n = len(trips)

for k in counts.keys():
    percentages[k]= counts[k]/n

print(percentages)
```

    {0: 0.1618118297166257, 1: 0.14230368165868734, 2: 0.14693905511451427, 3: 0.14460233975993483, 4: 0.14741096505582998, 5: 0.14465561991459952, 6: 0.11227650877980834}


Her ser vi at omtrent 16.2 % av turene skjer på mandager, mens 11.2 % av turene skjer på søndager.  

**Oppsummering.** I denne seksjonen har vi lært følgende: 
- *Parsing* er å hente ut informasjon fra strenger som er skrevet i et strukturert format.
- Det finnes Python-pakker for parsing av kjente strengformater.
- Python-pakken *datetime* kan brukes til å hente informasjon fra en standard datostreng, som for eksempel *2023-07-03 03:06:45.130000+00:00*.

I vårt eksempel brukte vi *datetime* til å hente sykkelturer som startet mellom 7 og 10 på en hverdag, samt å telle antall sykkelturer for hver ukedag.

**Aktivitetsforslag 1.**

1. Opprett variabelen `evening_weekend_trips`, som skal være en liste over alle turer som ble gjort på kveldstid i helger, det vil si mellom 20 og 24 på enten fredag, lørdag eller søndag. Listen trenger kun å inneholde indeksen til de aktuelle turene. 
2. Hvor mange slike turer finnes og hvor stor prosentandel utgjør de?
3. Hva er gjennomsnittlig varighet for slike turer? 

**Aktivitetsforslag 2.** Hva er gjennomsnittlig varighet for hverdagsturer? Og for helgesturer? Hva tror du forskjellen skyldes? 

**Aktivitetsforslag 3.** 
1. Tell antall sykkelturer som startet på hver av klokketimene, det vil si 0, 1, 2, 3 og opp til 23. Hvilken klokketime har flest og færrest sykkelturer? Vis fordelingen i prosent. 
2. Hvordan fordeler turene seg på følgende perioder av dagen?
    * Natt: kl. 0-5
    * Morgen: kl. 6-11
    * Ettermiddag: kl. 12-17
    * Kveld: kl. 18-23

