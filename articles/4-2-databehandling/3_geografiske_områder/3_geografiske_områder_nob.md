---
title: "Geografiske områder"
belongs_to_chain: "Databehandling"
figures_to_include:
	- "oslo_region.png"
---

Hva om vi ønsker å selv definere et område og hente alle turer som endte i dette området? Under kan du se et eksempel på et område:

<img src="/media/markdowncontent/assosiated_files/oslo_region.png" width="300">

Hvordan kan vi definere dette området i Python? Alt vi trenger å gjøre er å angi *hjørnepunktene* som en liste av koordinater. Disse hjørnepunktene danner nemlig en mangekant (*polygon*):


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

Forklaring: for å definere området brukte vi funksjonen  `Polygon(corners)`, som vi hentet fra Python-pakken [*shapely*](https://shapely.readthedocs.io/en/stable/manual.html). Denne pakken brukes til å gjøre operasjoner på geometriske objekter, slik som punkter, linjer og mangekanter.

Når vi har definert det geometriske objektet, gir `shapely` oss en rekke funksjoner, blant annet å sjekke om et punkt ligger innenfor objektet. Med andre ord, vi kan sjekke om et geografisk punkt ligger innenfor mangekanten: 


```python
oslo_s = Point(59.91085305987858, 10.750512158605307)
vigelandsparken = Point(59.9286828181158, 10.697803494202565)

print(oslo_s.within(my_area))
print(vigelandsparken.within(my_area))
```

    True
    False


Resultatet forteller oss at *Oslo S* ligger innenfor området vårt, mens *Vigelandsparken* ligger utenfor. 

Metoden for å sjekke om et punkt ligger innenfor et område er: 
1. Definer området med kommandoen `my_area = Polygon(corners)`, der `corners` er en liste av koordinater. 
2. Definer punktet med kommandoen `my_point = Point(longitude, latitude)`. Her må vi bruke `Point`-funksjonen, som vi importerer fra `shapely`. 
3. Bruk kommandoen `my_point.within(my_area)`. Dersom resultatet er `True` betyr det at punktet er innenfor området.

Vi kan nå bruke en `if`-setning for å bestemme hva vi skal gjøre ved positivt resultat:


```python
if oslo_s.within(my_area):
    print("Oslo S er innenfor mitt område!")
```

    Oslo S er innenfor mitt område!


Det er også mulig å definere et område som består av flere mangekanter, som i figuren under: 

<img src="../fig3/oslo_regions.png" width="300">

For å få til dette må vi definere de to mangekantene hver for seg, for eksempel med variabelnavnene `my_area1` og `my_area2`. Deretter kan vi kombinere disse med kommandoen `my_combined_area = MultiPolygon(my_area1, my_area2)`. 

**Hente sykkelturer innenfor et område.** Hva om vi nå ønsker å hente sykkelturer som både startet og endte innenfor mangekanten? Vi går gjennom hver tur, definerer start -og endepunktet, og sjekker om begge er innenfor området: 


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


Her ser vi at 77629 turer startet og slutter innnenfor området, som svarer til omtrent 59% av alle turer!

**Oppsummering.** I denne seksjonen har vi lært hvordan vi definerer et geografisk område i Python, og hvordan vi kan sjekke om et geografisk punkt er innenfor et område. Vi har brukt dette til å hente alle sykkelturer som startet og endte innenfor et bestemt område. 

**Aktivitetsforslag 1.** 

I nettleseren: 

1. Gå inn på [*geojson.io*](https://geojson.io/#map=10.68/59.9195/10.7298) og bruk funksjonen *Draw polygon* til å markere ett eller flere områder. Hjørnepunktene vil vises til høyre.

I Python:

3. Oprett en liste med hjørnekoordinatene, og opprett deretter mangekanten (*polygon*). 
4. Opprett en liste som inneholder alle turene som endte i ditt valgte område. Hvor stor prosentandel utgjør dette av alle turer? 

**Aktivitetsforslag 2.** Bruk [*geojson.io*](https://geojson.io/#map=10.68/59.9195/10.7298) til å lage to områder; et startområde og et sluttområde. Opprett en liste over alle turer som starter i det første området og slutter i det andre området. Hvor stor prosentandel utgjør dette av alle turer? 
