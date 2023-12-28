---
title: "Tabellfunksjonar"
figures_to_include:
---

Førre seksjon gav oss ein nyttig måte å konvertera ein enkelt kolonne. Men kva om me leggja til ein kolonne som inneheld avstanden mellom start -og endestasjonen for kvar tur?

La oss først prøva å rekna ut avstanden for ei enkelt rad i tabellen. For å henta ut ei spesifikk rad bruker me tabellfunksjonen `loc`, på følgjande måte:


```python
my_row = trips.loc[1000]
print(my_row)
```

started_at                   2023-07-01 10:07:16.682000+00:00
ended_at                     2023-07-01 10:27:10.715000+00:00
duration                                                 1194
start_station_id                                          464
start_station_name                                Sukkerbiten
start_station_description                       ved gangbrua
start_station_latitude                              59.905124
start_station_longitude                             10.753764
end_station_id                                            440
end_station_name                                    Lakkegata
end_station_description                    ved Sundtkvartalet
end_station_latitude                                59.917209
end_station_longitude                               10.762213
day_of_week                                          saturday
part_of_week                                          weekend
part_of_day                                           morning
Name: 1000, dtype: object


Me kan no henta ein spesifikk verdi i denne rada:


```python
start_lat = my_row["start_station_latitude"]
print(start_lat)
```

    59.905124380703484


Dette er éin av fire verdiar me treng for å rekna ut avstanden. Me definerer no ein funksjon som tek ei rad som parameter, og returnerer avstanden:


```python
from geopy import distance

def get_distance(row):
    start_lat = row["start_station_latitude"]
    start_lon = row["start_station_longitude"]
    end_lat = row["end_station_latitude"]
    end_lon = row["end_station_longitude"]
    start = (start_lat, start_lon)
    end = (end_lat, end_lon)
    d = distance.distance(start, end)
    return d.km

test = get_distance(my_row)
print(test)
```

    1.426929791603095


*Denne koden er basert på det me lærte i seksjonen* Håndtering av geografisk data.

For å bruka denne funksjonen på alle radene i tabellen, bruker me igjen `apply`:


```python
distances = trips.apply(get_distance, axis=1)
print(distances)
```

    0         1.351713
    1         2.531455
    2         0.872273
    3         3.941900
    4         0.824377
                ...   
    131376    0.653792
    131377    2.107308
    131378    0.000000
    131379    0.000000
    131380    0.000000
Length: 131381, dtype: float64


Merk at me må inkludera parameteren `axis=1`, for å spesifisera at funksjonen vår skal brukast på alle rader (ikkje alle kolonnar).

Resultatet av `apply` er ein ny kolonne, som kan setjast inn i tabellen:


```python
trips["distance"] = trips.apply(get_distance, axis=1)
```

No har me oppretta kolonnen *distance*, og me kan enkelt henta diverse statistiske verdiar:


```python
print(trips["distance"].mean())
print(trips["distance"].median())
print(trips["distance"].max())
print(trips["distance"].min())
```

    1.5637046147163225
    1.3778103572129936
    8.17033235134136
    0.0


Her ser me at sykkelturar i gjennomsnitt skjedde mellom stasjonar som var 1.56 km frå kvarandre, og at den største avstanden var 8.17 km. (Kvifor trur du den minste er avstanden 0 km? Og kva betyr det at medianverdien er 1.38 km?)

Kva om me ønskjer å finna ut om helgesturer i gjennomsnitt er lengre enn kvardagsturar? I førre seksjon oppretta me kolonnen *part_of_week*, som nettopp fortel om ein tur skjedde på kvardag eller helg. Me kan no *gruppera* tabellen etter denne kolonnen:


```python
grouped = trips.groupby("part_of_week")
```

Me kan no tenkja oss at tabellen er delt i to; alle rader med verdien *weekday* er i den første gruppa, og alle rader med verdien *weekend* er i den andre gruppa. Kva er poenget med dette? Det ser me dersom me prøver å rekna ut gjennomsnittet:


```python
print(trips["distance"].mean())
print()
print(grouped["distance"].mean())
```

    1.5637046147163225
    
part_of_week
weekday    1.559390
weekend    1.576183
Name: distance, dtype: float64


Forklaring:

* Når tabellen er ugruppert, vil gjennomsnittet av ein kolonne berre vera eit tal.
* Når tabellen er gruppert, får me eitt gjennomsnitt for kvar av gruppene.

Resultatet fortel oss at helgeturar i gjennomsnitt er litt lengre enn kvardagsturar.

Me kan bruka same metode for å samanlikna ulike grupper i tabellen. Kanskje me ønskjer å samanlikna kvar vekedag, med tanke på kor lenge sykkelturane varer i gjennomsnitt?


```python
grouped = trips.groupby("day_of_week")
print(grouped["duration"].mean())
```

day_of_week
friday        878.331543
monday        797.965191
saturday      999.538279
sunday       1030.042845
thursday      842.061164
tuesday       794.381312
wednesday     815.300803
Name: duration, dtype: float64


Her ser me at varigheita til sykkelturane i gjennomsnitt er kortast på måndag, tysdag og onsdag, og lengst på laurdag og søndag.

**Oppsummering.** I denne seksjonen har me sett korleis tabellfunksjonen `apply` kan brukast for å gjera ein operasjon på alle radene i ein tabell. Resultatet er ein ny kolonne som kan setjast inn i tabellen.

Vidare har me sett at tabellfunksjonen `groupby` kan brukast for å dela tabellen inn i grupper. Når me reknar ut statistiske verdiar, får me éin verdi for kvar gruppe. Det gjer at me kan samanlikna gruppene og finna tendensar.

**Aktivitetsforslag.** Dette føreset at du har gjort oppgåvene i førre seksjon.

1. Legg til ein ny kolonne i `trips`, som inneheld avstanden mellom *Oslo S* og endestasjonen for turane. *Hint: lag først ein funksjon som konverterer ei enkelt rad i tabellen til den rette avstanden.*
2. Kor nærme endar turane *Oslo S* i gjennomsnitt?
3. Samanlikn gruppene morgon, ettermiddag, kveld og natt. I kva gruppe endar turane i snitt nærast *Oslo S*, og i kva gruppe endar dei lengst unna?
4. Samanlikn gruppene helg og kvardag. I kva gruppe endar turane nærast *Oslo S*?

Utfordringsoppgåve: Me har i denne seksjonen sett korleis ein kan gruppera etter éin kolonne. Det er også mogleg å gruppera etter to kolonnar, ved å bruka følgjande kommando:
```py
grouped = table.groupby(["column1", "column2"])
``` 
Grupper sykkelturane etter følgjande kolonnar:

* *part_of_week*: fortel om ein tur starta på kvardag eller helg
* *part_of_day*: fortel om tur starta på morgon, ettermiddag, kveld eller natt.

Du må oppretta desse kolonnane dersom du ikkje har dei. Hent gjennomsnittlege avstandar i den grupperte tabellen. Kva fortel svara deg?

Utfordringsspørsmål: I dei siste to seksjonane har du sett at det finst to versjonar av `apply`; ein kolonnefunksjon og ein tabellfunksjon. Kva er forskjellen på desse? Kvifor må du bruka tabellfunksjonen i punkt 1? Kan du gi ein regel for når du må bruka tabellfunksjonen?

# Trekkja ut ustrukturert data

Me skal no sjå på korleis me kan oppretta ein tabell som berre inneheld informasjon om sykkelstasjonane. Då må me trekkja ut relevant data frå sykkelturtabellen.

Først lagar me ein tabell som berre inneheld dei relevante kolonnane i turtabellen (men framleis alle radene):


```python
columns = ["start_station_id", "start_station_name", "start_station_description", "start_station_latitude", "start_station_longitude"]
start_stations = trips[columns]
start_stations.head()
```




<div>
<style scoped>
.dataframe tbody tr th:only-of-type {
vertical-align: middle;
    }

.dataframe tbody tr th {
vertical-align: top;
    }

.dataframe thead th {
text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>start_station_id</th>
<th>start_station_name</th>
<th>start_station_description</th>
<th>start_station_latitude</th>
<th>start_station_longitude</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>387</td>
<td>Studenterlunden</td>
<td>langs Karl Johan</td>
<td>59.914586</td>
<td>10.735453</td>
</tr>
<tr>
<th>1</th>
<td>2315</td>
<td>Rostockgata</td>
<td>utanfor Bjørvika visningssenter</td>
<td>59.906920</td>
<td>10.760312</td>
</tr>
<tr>
<th>2</th>
<td>384</td>
<td>Vår Frelsers gravlund</td>
<td>langs Ullevålsveien</td>
<td>59.919440</td>
<td>10.743765</td>
</tr>
<tr>
<th>3</th>
<td>584</td>
<td>Henrik Wergelands allé</td>
<td>ved Bogstadveien</td>
<td>59.926894</td>
<td>10.720789</td>
</tr>
<tr>
<th>4</th>
<td>600</td>
<td>Dyvekes bru</td>
<td>ved skatepark</td>
<td>59.905323</td>
<td>10.768958</td>
</tr>
</tbody>
</table>
</div>



No har me berre teke med startstasjonane, men me må ta høgd for at det kanskje finst nokre stasjonar som berre er brukte som endestasjon:


```python
columns = ["end_station_id", "end_station_name", "end_station_description", "end_station_latitude", "end_station_longitude"]
end_stations = trips[columns]
```

No ønskjer me at tabellane `start_stations` og `end_stations` skal ha same kolonnenamn. Me endrar kolonnenamna på følgjande måte:


```python
new_column_names = ["id", "name", "description", "latitude", "longitude"]
start_stations.columns = new_column_names
end_stations.columns = new_column_names
```

No har me to tabellar med akkurat dei same kolonnenamna. Då kan me slå dei saman til ein ny tabell:


```python
tables = [start_stations, end_stations]
stations = pd.concat(tables)
stations.head()
```




<div>
<style scoped>
.dataframe tbody tr th:only-of-type {
vertical-align: middle;
    }

.dataframe tbody tr th {
vertical-align: top;
    }

.dataframe thead th {
text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>id</th>
<th>name</th>
<th>description</th>
<th>latitude</th>
<th>longitude</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>387</td>
<td>Studenterlunden</td>
<td>langs Karl Johan</td>
<td>59.914586</td>
<td>10.735453</td>
</tr>
<tr>
<th>1</th>
<td>2315</td>
<td>Rostockgata</td>
<td>utanfor Bjørvika visningssenter</td>
<td>59.906920</td>
<td>10.760312</td>
</tr>
<tr>
<th>2</th>
<td>384</td>
<td>Vår Frelsers gravlund</td>
<td>langs Ullevålsveien</td>
<td>59.919440</td>
<td>10.743765</td>
</tr>
<tr>
<th>3</th>
<td>584</td>
<td>Henrik Wergelands allé</td>
<td>ved Bogstadveien</td>
<td>59.926894</td>
<td>10.720789</td>
</tr>
<tr>
<th>4</th>
<td>600</td>
<td>Dyvekes bru</td>
<td>ved skatepark</td>
<td>59.905323</td>
<td>10.768958</td>
</tr>
</tbody>
</table>
</div>



No har me ein tabell som garantert inneheld alle stasjonane. Men sidan kvar rad i tabellen framleis representerer ein sykkeltur, vil det vera mange duplikasjoner. Me kan enkelt fjerne duplikasjonene:


```python
stations = stations.drop_duplicates()
```

I tabellen ovanfor ser me at kvar rad har ein indeks som kjem frå sykkelturtabellen! Me ønskjer heller å bruka kolonnen *id* som indeks:


```python
stations = stations.set_index("id")
stations.head()
```




<div>
<style scoped>
.dataframe tbody tr th:only-of-type {
vertical-align: middle;
    }

.dataframe tbody tr th {
vertical-align: top;
    }

.dataframe thead th {
text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>name</th>
<th>description</th>
<th>latitude</th>
<th>longitude</th>
</tr>
<tr>
<th>id</th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>387</th>
<td>Studenterlunden</td>
<td>langs Karl Johan</td>
<td>59.914586</td>
<td>10.735453</td>
</tr>
<tr>
<th>2315</th>
<td>Rostockgata</td>
<td>utanfor Bjørvika visningssenter</td>
<td>59.906920</td>
<td>10.760312</td>
</tr>
<tr>
<th>384</th>
<td>Vår Frelsers gravlund</td>
<td>langs Ullevålsveien</td>
<td>59.919440</td>
<td>10.743765</td>
</tr>
<tr>
<th>584</th>
<td>Henrik Wergelands allé</td>
<td>ved Bogstadveien</td>
<td>59.926894</td>
<td>10.720789</td>
</tr>
<tr>
<th>600</th>
<td>Dyvekes bru</td>
<td>ved skatepark</td>
<td>59.905323</td>
<td>10.768958</td>
</tr>
</tbody>
</table>
</div>



No kan me henta ein spesifikk stasjon ved å bruka stasjons-id:


```python
s = stations.loc["387"]
print(s)
```

name            Studenterlunden
description    langs Karl Johan
latitude              59.914586
longitude             10.735453
Name: 387, dtype: object


Vidare kan me henta spesifikke verdiar:


```python
print(s["latitude"])
```

    59.914586


Dette er svært nyttig når me i neste seksjon skal visualisera sykkeldata på kart!

**Oppsummering.** I denne seksjonen har trekt ut ustrukturert data frå ein tabell, og oppretta ein ny tabell der dataa er strukturerte. Me har gjort det ved å
- henta bestemde kolonnar,
- endre kolonnenamn,
- slå saman tabellar,
- fjerne duplikasjoner og
- endre indeksering.


```python
%store trips
%store stations
```

Stored 'trips' (DataFrame)
Stored 'stations' (DataFrame)

