---
title: "Håndtering av geografisk data"
belongs_to_chain: "Databehandling"
figures_to_include:
---

Hvordan kan vi behandle geografiske koordinater i Python? For eksempel, hvordan kan vi finne ut hvor mange som pendler til Oslo sentrum? Er det mulig å hente alle turer som er lengre enn tre kilometer og ender på en sykkelstasjon i sentrum? 

La oss igjen se på en tilfeldig tur:


```python
print(json.dumps(trips[1000], indent=4))
```

    {
        "started_at": "2023-07-01 10:07:16.682000+00:00",
        "ended_at": "2023-07-01 10:27:10.715000+00:00",
        "duration": 1194,
        "start_station_id": "464",
        "start_station_name": "Sukkerbiten",
        "start_station_description": "ved gangbroen",
        "start_station_latitude": 59.905124380703484,
        "start_station_longitude": 10.753763553726515,
        "end_station_id": "440",
        "end_station_name": "Lakkegata",
        "end_station_description": "ved Sundtkvartalet",
        "end_station_latitude": 59.9172088,
        "end_station_longitude": 10.7622135
    }


Vi har følgende posisjoner: 

Start: *59.91944043984847, 10.7437646218726*   
Slutt: *59.922425, 10.758182*

Vi har ikke noe informasjon om hvilken rute syklisten tok mellom de to stasjonene, men som en forenkling kan vi regne ut avstanden mellom start -og sluttposisjonen. I Python kan vi bruke pakken [*GeoPy*](https://geopy.readthedocs.io/en/stable/) for å regne ut avstanden mellom to koordinater: 


```python
from geopy import distance

start = (59.91944043984847, 10.7437646218726)
end = (59.922425, 10.758182)

d = distance.distance(start, end)

print(d.km)
```

    0.8722726079461717


Forklaring:

* Vi definerer de geografiske punktene som variabler. Et punkt defineres som et tuppel med skrivemåten `start = (latitude, longitude)`.
* Vi regner ut avstanden mellom to punkter ved å bruke kommandoen `d= distance.distance(start, end)`.
* Variabelen `d` er nå et Python-objekt som inneholder ulike verdier, for eksempel avstanden i kilometer (`d.km`) og engelske mil (`d.miles`).
* Resultatet er avstanden i **luftlinje**, også kjent som den *[geodetiske kurven](https://no.wikipedia.org/wiki/Geodetisk_kurve)* mellom punktene. Syklisten må ha syklet **minst** denne avstanden for å reise mellom stasjonene. 

Vi ser at avstanden mellom de to stasjonene er omtrent 0.87 km. Resultatet forteller oss at sykkelturen var **minst** 0.87 km. 

Vi kan bruke denne metoden til å hente alle turer som var minst 3 km: 


```python
long_trips = []

n = len(trips)
for i in range(n):
    t = trips[i]
    start = (t["start_station_latitude"], t["start_station_longitude"])
    end = (t["end_station_latitude"], t["end_station_longitude"])
    d = distance.distance(start, end)
    if d.km > 3:
        long_trips.append(i)

print(long_trips[:10])

k = len(long_trips)
print(k)
print(k/n)
```

    [3, 6, 37, 40, 60, 74, 78, 143, 163, 166]
    11791
    0.08974661480731613


Igjen lagrer vi kun indeksen til de aktuelle turene, siden all annen informasjon kan hentes i variabelen *trips*. Fra utskriften ser vi at 11791 turer var minst tre kilometer lange, og at dette utgjør omtrent 9% av alle turer.

Vi ønsket lange turer som ender i sentrum av Oslo. Dersom vi går inn på [*Google Maps*](https://www.google.no/maps/place//@59.9105115,10.7484254,17z) og høyreklikker på *Oslo S*, kan vi kopiere koordinatene og legge dem i en Python-variabel:


```python
oslo_s = (59.91085305987858, 10.750512158605307)
```

Som en forenkling kan vi nå hente alle turer som endte i en viss nærhet til *Oslo S*. For eksempel kan vi kreve at endestasjonen er innen 1 km av *Oslo S*:


```python
trips_to_city_centre = []

n = len(trips)
for i in range(n):
    t = trips[i]
    end = (t["end_station_latitude"], t["end_station_longitude"])
    d = distance.distance(oslo_s, end)
    if d.km < 1:
        trips_to_city_centre.append(i)

print(trips_to_city_centre[:10])

k = len(trips_to_city_centre)
print(k)
print(k/n)
```

    [4, 5, 6, 8, 11, 12, 14, 15, 16, 19]
    44896
    0.34172368911790896


Vi ser at omtrent 34.2% av turene endte i nærheten av *Oslo S*. Denne koden tok en del tid å kjøre, fordi vi gikk gjennom over 130.000 turer og gjorde en avstandsutregning hver gang. Finnes det en mer effektiv måte å gjøre det på? 

Fra tidligere vet vi at det bare finnes 266 sykkelstasjoner:


```python
print(len(stations))
```

    266


Alt vi trenger er å regne ut avstanden til *Oslo S* én gang for hver stasjon! Husk at variabelen `stations` inneholder en dictionary på følgende form: 

```json
{
    "551": {
        "name": "Olaf Ryes plass",
        "description": "langs Sofienberggata",
        "latitude": 59.922425,
        "longitude": 10.758182  
    },
    "384": {
        "name": "V\u00e5r Frelsers gravlund",
        "description": "langs Ullev\u00e5lsveien",
        "latitude": 59.91944043984847,
        "longitude": 10.7437646218726   
    },
    ...
}
```

Det vi ønsker er å legge til en ekstra attributt for hver stasjon, slik at vi ender opp med følgende dictionary:

```json
{
    "551": {
        "name": "Olaf Ryes plass",
        "description": "langs Sofienberggata",
        "latitude": 59.922425,
        "longitude": 10.758182,
        "distance_to_oslo_s": 1.3587591231552714
    },
    "384": {
        "name": "V\u00e5r Frelsers gravlund",
        "description": "langs Ullev\u00e5lsveien",
        "latitude": 59.91944043984847,
        "longitude": 10.7437646218726,
        "distance_to_oslo_s": 1.028501530622403
    },
    ...
}
```

Vi må altså gå gjennom hver stasjon, regne ut avstanden til *Oslo S*, og legge til dette som et ekstra attributt:


```python
for id in stations.keys(): 
    s = stations[id]
    station_coordinates = (s["latitude"], s["longitude"])
    d = distance.distance(station_coordinates, oslo_s)
    stations[id]["distance_to_oslo_s"] = d.km
```

Nå kan vi enkelt hente avstanden fra en bestemt stasjon til *Oslo S*:


```python
print(stations["384"]["distance_to_oslo_s"])
```

    1.028501530622403


Nå som vi har lagret alle relevante avstander, kan vi mer effektivt hente alle turer som endte i nærheten av *Oslo S*:


```python
trips_to_city_centre = []

n = len(trips)
for i in range(n):
    end_station_id = trips[i]["end_station_id"]
    d = stations[end_station_id]["distance_to_oslo_s"]
    if d < 1:
        trips_to_city_centre.append(i)

print(trips_to_city_centre[:10])

k = len(trips_to_city_centre)
print(k)
print(k/n)
```

    [4, 5, 6, 8, 11, 12, 14, 15, 16, 19]
    44896
    0.34172368911790896


Målet vårt var å hente turer som både var lengre enn 3 km og endte i nærheten av *Oslo S*, altså turer som er i både listen `long_trips` og `trips_to_city_centre`. Da kan vi bruke samme metode som i forrige seksjon:


```python
long_trips_to_city_centre =  set(long_trips) & set(trips_to_city_centre)
long_trips_to_city_centre = list(long_trips_to_city_centre)

print(long_trips_to_city_centre[:10])

k = len(long_trips_to_city_centre)
print(k)
print(k/n)
```

    [6, 49158, 65545, 81933, 65553, 16406, 32793, 114714, 49186, 49188]
    3056
    0.023260593236464937


Her ser vi at 3056 turer, som utgjør omtrent 2.3% av alle turer, tilfredstiller begge kravene. 

**Oppsummering.** I denne seksjonen har vi lært følgende: 
* Hvordan vi kan lagre et geografiske punkt som et tuppel av typen `(59.922425, 10.758182)`, og bruke `geopy` til å regne ut avstanden mellom punkter.
* Hvordan avstander kan lagres på en systematisk måte, slik at vi unngår å gjøre de samme utregningene mange ganger.

Vi har brukt dette til å hente alle sykkelturer som var minst 3 km lange og endte i Oslo sentrum. 

**Aktivitetsforslag 1.** 

1. Hva er gjennomsnittlig avstand mellom start -og sluttstasjon blant alle sykkelturer? Finn også den største og minste avstanden.
2. Sammenlign gjennomsnittlig avstand for hverdagsturer og helgesturer. Hvis det er en forskjell, hva tror du det skyldes?

**Aktivitetsforslag 2.** 

Velg deg et geografisk punkt i Oslo og hent koordinatene tl punktet (for eksempel ved å høyreklikke på punktet i *Google Maps*). Gjør følgende oppgaver: 

1. Endre variabelen `stations` slik at den også inneholder avstanden fra stasjonene til ditt valgte punkt, på følgende måte:

```
{
    "551": {
        "name": "Olaf Ryes plass",
        "description": "langs Sofienberggata",
        "latitude": 59.922425,
        "longitude": 10.758182,
        "distance_to_my_point": 
    },
    "384": {
        "name": "V\u00e5r Frelsers gravlund",
        "description": "langs Ullev\u00e5lsveien",
        "latitude": 59.91944043984847,
        "longitude": 10.7437646218726,
        "distance_to_my_point": 
    },
    ...
}
```
Du kan selv velge navnet til det nye attributtet. 

Bruk avstandene du har lagret til å gjøre følgende oppgaver:

2. Opprett en liste med alle turer som **startet** i nærheten av ditt valgte punkt.
3. Opprett en liste med alle turer som **endte** i nærheten av ditt valgte punkt.
4. Opprett en liste med alle turer som **både** startet og endte i nærheten av ditt valgte punkt.
5. Hvor mange turer finnes i hver av listene og hvor stor prosentandel utgjør de?
6. Hvor nærme ender sykkelturene ditt punkt i gjennomsnitt? Finn også gjennomsnittet for hverdagsturer, og for helgesturer. Sammenlign resultatene - hvis det er en stor forskjell, hva tror du det skyldes?

**Aktivitetsforslag 3 (utfordring).** Gå gjennom alle turer med en løkke. For hver stasjon, regn ut avstand delt på varighet. Dette forteller hvor raskt syklisten har tilbakelagt avstanden mellom de to stasjonene, altså en slags "gjennomsnittlig hastighet". Skriv ut informasjon om følgende turer:

* Turen med høyest "hastighet" og
    * avstand over 1 km
    * avstand over 3 km
    * avstand over 5 km
      
Finn start -og endestasjon for disse turene på kartet. Finn ut hvor lang tid *Google* beregner at det tar å sykle mellom stasjonene. Sammenlign med hvor kort tid syklisten faktisk brukte.

**Aktivitetsforslag 4 (utfordring).** 

Vi ønsker nå å legge til følgende informasjon i variabelen `stations`: 

```json
{
    "551": {
        "name": "Olaf Ryes plass",
        "description": "langs Sofienberggata",
        "latitude": 59.922425,
        "longitude": 10.758182,
        "distance_to_other_stations": {
            "387": 1.5424618400028995,
            "499": 0.7591003631405512,
            "2315": 1.731562337348591,
            "410": 0.8739156584845489,
            ...
        }
    },
    ...
}
```
For hver stasjon skal du altså opprette attributtet *distance_to_other_stations*, der du skal lagre avstanden til alle andre stasjoner. Husk at for å gå gjennom alle stasjoner kan du bruke løkken:


```python
for id in stations.keys(): 
    s = stations[id]       
```

Bruk avstandene du har lagret til å hente alle turer som var minst 3 km.

