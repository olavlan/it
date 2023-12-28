---
title: "Geografiske område"
belongs_to_chain: "Databehandling"
figures_to_include:
	- "oslo_region.png"
---

Kva om me ønskjer å sjølv definera eit område og henta alle turar som enda i dette området? Under kan du sjå eit døme på eit område:

<img src="/media/markdowncontent/assosiated_files/oslo_region.png" width="300">

Korleis kan me definera dette området i Python? Alt me treng å gjera er å angi *hjørnepunkta* som ei liste av koordinatar. Desse hjørnepunkta dannar nemleg ein mangekant (*polygon*):


```python
from shapely.geometry import Point, Polygon, MultiPolygon

corners = [(59.92065829373027, 10.705038426191948),
           (59.904743048315424, 10.707183476660077),
           (59.902591754210164, 10.73549814283615),
           (59.89979486351757, 10.782689253130059),
           (59.91162625297167, 10.78826638434711),
           (59.92818311704261, 10.76896093013562),
           (59.93140751894279, 10.725201900590633)]

my_area = Polygon(corners)
```

Forklaring: for å definera området brukte me funksjonen  `Polygon(corners)`, som me henta frå Python-pakken [*shapely*](https://shapely.readthedocs.io/ein/stabla/manual.html). Denne pakken blir brukt til å gjera operasjonar på geometriske objekt, slik som punkt, linjer og mangekantar.

Når me har definert det geometriske objektet, gir `shapely` oss ei rekkje funksjonar, mellom anna å sjekka om eit punkt ligg innanfor objektet. Med andre ord, me kan sjekka om eit geografisk punkt ligg innanfor mangekanten:


```python
oslo_s = Point(59.91085305987858, 10.750512158605307)
vigelandsparken = Point(59.9286828181158, 10.697803494202565)

print(oslo_s.within(my_area))
print(vigelandsparken.within(my_area))
```

Tru
Falsa


Resultatet fortel oss at *Oslo S* ligg innanfor området vårt, medan *Vigelandsparken* ligg utanfor.

Metoden for å sjekka om eit punkt ligg innanfor eit område er:
1. Definer området med kommandoen `my_area = Polygon(corners)`, der `corners` er ei liste av koordinatar.
2. Definer punktet med kommandoen `my_point = Point(longitude, latitude)`. Her må me bruka `Point`-funksjonen, som me importerer frå `shapely`.
3. Bruk kommandoen `my_point.within(my_area)`. Dersom resultatet er `True` betyr det at punktet er innanfor området.

Me kan no bruka ein `if`-setning for å bestemma kva me skal gjera ved positivt resultat:


```python
if oslo_s.within(my_area):
    print("Oslo S er innenfor mitt område!")
```

Oslo S er innanfor mitt område!


Det er også mogleg å definera eit område som består av fleire mangekantar, som i figuren under:

<img src="../fig3/oslo_regions.png" width="300">

For å få til dette må me definera dei to mangekantane kvar for seg, til dømes med variabelnamna `my_area1` og `my_area2`. Deretter kan me kombinera desse med kommandoen `my_combined_area = MultiPolygon(my_area1, my_area2)`.

**Henta sykkelturar innanfor eit område.** Kva om me no ønskjer å henta sykkelturar som både starta og enda innanfor mangekanten? Me går gjennom kvar tur, definerer start -og endepunktet, og sjekkar om begge er innanfor området:


```python
trips_in_my_area = []

n = len(trips)
for i in range(n):
    t = trips[i]
    
    lat1, lon1 = t["start_station_latitude"], t["start_station_longitude"]
    start = Point(lat1, lon1)
    
    lat2, lon2 = t["end_station_latitude"], t["end_station_longitude"]
    end = Point(lat2, lon2)
    
    if start.within(my_area) and end.within(my_area):
        trips_in_my_area.append(i)

k = len(trips_in_my_area)

print(k)
print(k/n)
```

    77629
    0.5908693037806075


Her ser me at 77629 turar starta og sluttar innenfor området, som svarer til omtrent 59% av alle turar!

**Oppsummering.** I denne seksjonen har me lært korleis me definerer eit geografisk område i Python, og korleis me kan sjekka om eit geografisk punkt er innanfor eit område. Me har brukt dette til å henta alle sykkelturar som starta og enda innanfor eit bestemt område.

**Aktivitetsforslag 1.**

I nettlesaren:

1. Gå inn på [*geojson.io*](https://geojson.io/#map=10.68/59.9195/10.7298) og bruk funksjonen *Draw polygon* til å markera eitt eller fleire område. Hjørnepunkta vil visast til høgre.

I Python:

3. Oprett ei liste med hjørnekoordinatane, og opprett deretter mangekanten (*polygon*).
4. Opprett ei liste som inneheld alle turane som enda i ditt valde område. Kor stor prosentdel utgjer dette av alle turar?

**Aktivitetsforslag 2.** Bruk [*geojson.io*](https://geojson.io/#map=10.68/59.9195/10.7298) til å laga to område; eit startområde og eit sluttområde. Opprett ei liste over alle turar som startar i det første området og sluttar i det andre området. Kor stor prosentdel utgjer dette av alle turar?
