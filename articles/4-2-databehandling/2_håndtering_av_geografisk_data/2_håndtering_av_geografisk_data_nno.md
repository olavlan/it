---
title: "Handtering av geografisk data"
belongs_to_chain: "Databehandling"
figures_to_include:
---

Korleis kan me behandla geografiske koordinatar i Python? Til dømes, korleis kan me finna ut kor mange som pendlar til Oslo sentrum? Er det mogleg å henta alle turar som er lengre enn tre kilometer og endar på ein sykkelstasjon i sentrum?

La oss igjen sjå på ein tilfeldig tur:


```python
print(json.dumps(trips[1000], indent=4))
```

    {
"started_at": "2023-07-01 10:07:16.682000+00:00",
"ended_at": "2023-07-01 10:27:10.715000+00:00",
"duration": 1194
"start_station_id": "464",
"start_station_name": "Sukkerbiten",
"start_station_description": "ved gangbrua",
"start_station_latitude": 59.905124380703484
"start_station_longitude": 10.753763553726515
"end_station_id": "440",
"end_station_name": "Lakkegata",
"end_station_description": "ved Sundtkvartalet",
"end_station_latitude": 59.9172088
"end_station_longitude": 10.7622135
    }


Me har følgjande posisjonar:

Start: *59.91944043984847, 10.7437646218726*
Slutt: *59.922425, 10.758182*

Me har ikkje noko informasjon om kva rute syklisten tok mellom dei to stasjonane, men som ei forenkling kan me rekna ut avstanden mellom start -og sluttposisjonen. I Python kan me bruka pakken [*GeoPy*](https://geopy.readthedocs.io/ein/stabla/) for å rekna ut avstanden mellom to koordinatar:


```python
from geopy import distance

start = (59.91944043984847, 10.7437646218726)
end = (59.922425, 10.758182)

d = distance.distance(start, end)

print(d.km)
```

    0.8722726079461717


Forklaring:

* Me definerer dei geografiske punkta som variablar. Eit punkt blir definert som eit tuppel med skrivemåten `start = (latitude, longitude)`.
* Me reknar ut avstanden mellom to punkt ved å bruka kommandoen `d= distance.distance(start, end)`.
* Variabelen `d` er no eit Python-objekt som inneheld ulike verdiar, til dømes avstanden i kilometer (`d.km`) og engelske mil (`d.miles`).
* Resultatet er avstanden i **luftlinje**, også kjent som den *[geodetiske korga](https://no.wikipedia.org/wiki/geodetisk_kurve)* mellom punkta. Syklisten må ha sykla **minst** denne avstanden for å reisa mellom stasjonane.

Me ser at avstanden mellom dei to stasjonane er omtrent 0.87 km. Resultatet fortel oss at sykkelturen var **minst** 0.87 km.

Me kan bruka denne metoden til å henta alle turar som var minst 3 km:


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


Igjen lagrar me berre indeksen til dei aktuelle turane, sidan all annan informasjon kan hentast i variabelen *trips*. Frå utskrifta ser me at 11791 turar var minst tre kilometer lange, og at dette utgjer omtrent 9% av alle turar.

Vi ønsket lange turar som endar i sentrum av Oslo. Dersom me går inn på [*Google Maps*](https://www.google.no/maps/place//@59.9105115,10.7484254,17z) og høgreklikkar på *Oslo S*, kan me kopiera koordinatane og leggja dei i ein Python-variabel:


```python
oslo_s = (59.91085305987858, 10.750512158605307)
```

Som ei forenkling kan me no henta alle turar som enda i ein viss nærleik til *Oslo S*. Til dømes kan me krevja at endestasjonen er innan 1 km av *Oslo S*:


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


Me ser at omtrent 34.2% av turane enda i nærleiken av *Oslo S*. Denne koden tok ein del tid å køyra, fordi me gjekk gjennom over 130.000 turar og gjorde ei avstandsutrekning kvar gong. Finst det ein meir effektiv måte å gjera det på?

Frå tidlegare veit me at det berre finst 266 sykkelstasjonar:


```python
print(len(stations))
```

    266


Alt me treng er å rekna ut avstanden til *Oslo S* éin gong for kvar stasjon! Hugs at variabelen `stations` inneheld ein dictionary på følgjande form:

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

Det me ønskjer er å leggja til eit ekstra attributt for kvar stasjon, slik at me endar opp med følgjande dictionary:

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

Me må altså gå gjennom kvar stasjon, rekna ut avstanden til *Oslo S*, og leggja til dette som eit ekstra attributt:


```python
for id in stations.keys(): 
    s = stations[id]
    station_coordinates = (s["latitude"], s["longitude"])
    d = distance.distance(station_coordinates, oslo_s)
    stations[id]["distance_to_oslo_s"] = d.km
```

No kan me enkelt henta avstanden frå ein bestemd stasjon til *Oslo S*:


```python
print(stations["384"]["distance_to_oslo_s"])
```

    1.028501530622403


No som me har lagra alle relevante avstandar, kan me meir effektivt henta alle turar som enda i nærleiken av *Oslo S*:


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


Målet vårt var å henta turar som både var lengre enn 3 km og enda i nærleiken av *Oslo S*, altså turar som er i både lista `long_trips` og `trips_to_city_centre`. Då kan me bruka same metode som i førre seksjon:


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


Her ser me at 3056 turar, som utgjer omtrent 2.3% av alle turar, tilfredstiller begge krava.

**Oppsummering.** I denne seksjonen har me lært følgjande:
* Korleis me kan lagra eit geografiske punkt som eit tuppel av typen `(59.922425, 10.758182)`, og bruka `geopy` til å rekna ut avstanden mellom punkt.
* Korleis avstandar kan lagrast på ein systematisk måte, slik at me unngår å gjera dei same utrekningane mange gonger.

Me har brukt dette til å henta alle sykkelturar som var minst 3 km lange og enda i Oslo sentrum.

**Aktivitetsforslag 1.**

1. Kva er gjennomsnittleg avstand mellom start -og sluttstasjon blant alle sykkelturar? Finn også den største og minste avstanden.
2. Samanlikn gjennomsnittleg avstand for kvardagsturar og helgesturer. Viss det er ein forskjell, kva trur du det kjem av?

**Aktivitetsforslag 2.**

Vel deg eit geografisk punkt i Oslo og hent koordinatane tl punktet (til dømes ved å høyreklikke på punktet i *Google Maps*). Gjer følgjande oppgåver:

1. Endre variabelen `stations` slik at han også inneheld avstanden frå stasjonane til ditt valde punkt, på følgjande måte:

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
Du kan sjølv velja namnet til det nye attributtet.

Bruk avstandane du har lagra til å gjera følgjande oppgåver:

2. Opprett ei liste med alle turar som **starta** i nærleiken av ditt valde punkt.
3. Opprett ei liste med alle turar som **enda** i nærleiken av ditt valde punkt.
4. Opprett ei liste med alle turar som **både** starta og enda i nærleiken av ditt valde punkt.
5. Kor mange turar finst i kvar av listene og kor stor prosentdel utgjer dei?
6. Kor nærme endar sykkelturane ditt punkt i gjennomsnitt? Finn også gjennomsnittet for kvardagsturar, og for helgesturer. Samanlikn resultata - viss det er ein stor forskjell, kva trur du det kjem av?

**Aktivitetsforslag 3 (utfordring).** Gå gjennom alle turar med ei løkke. For kvar stasjon, rekn ut avstand delt på varigheit. Dette fortel kor raskt syklisten har lagt bak seg avstanden mellom dei to stasjonane, altså ein slags "gjennomsnittleg fart". Skriv ut informasjon om følgjande turar:

* Turen med høgast "fart" og
* avstand over 1 km
* avstand over 3 km
* avstand over 5 km
      
Finn start -og endestasjon for desse turane på kartet. Finn ut kor lang tid *Google* bereknar at det tek å sykla mellom stasjonane. Samanlikn med kor kort tid syklisten faktisk brukte.

**Aktivitetsforslag 4 (utfordring).**

Me ønskjer no å leggja til følgjande informasjon i variabelen `stations`:

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
For kvar stasjon skal du altså oppretta attributtet *distance_to_other_stations*, der du skal lagra avstanden til alle andre stasjonar. Hugs at for å gå gjennom alle stasjonar kan du bruka løkka:


```python
for id in stations.keys(): 
    s = stations[id]       
```

Bruk avstandane du har lagra til å henta alle turar som var minst 3 km.

