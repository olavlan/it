---
title: "Tabellfunksjoner"
figures_to_include:
---

Forrige seksjon ga oss en nyttig måte å konvertere en enkelt kolonne. Men hva om vi legge til en kolonne som inneholder avstanden mellom start -og endestasjonen for hver tur? 

La oss først prøve å regne ut avstanden for en enkelt rad i tabellen. For å hente ut en spesifikk rad bruker vi tabellfunksjonen `loc`, på følgende måte:


```python
my_row = trips.loc[1000]
print(my_row)
```

    started_at                   2023-07-01 10:07:16.682000+00:00
    ended_at                     2023-07-01 10:27:10.715000+00:00
    duration                                                 1194
    start_station_id                                          464
    start_station_name                                Sukkerbiten
    start_station_description                       ved gangbroen
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


Vi kan nå hente en spesifikk verdi i denne raden: 


```python
start_lat = my_row["start_station_latitude"]
print(start_lat)
```

    59.905124380703484


Dette er én av fire verdier vi trenger for å regne ut avstanden. Vi definerer nå en funksjon som tar en rad som parameter, og returnerer avstanden: 


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


*Denne koden er basert på det vi lærte i seksjonen* Håndtering av geografisk data.

For å bruke denne funksjonen på alle radene i tabellen, bruker vi igjen `apply`:


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


Merk at vi må inkludere parameteren `axis=1`, for å spesifisere at funksjonen vår skal brukes på alle rader (ikke alle kolonner). 

Resultatet av `apply` er en ny kolonne, som kan settes inn i tabellen: 


```python
trips["distance"] = trips.apply(get_distance, axis=1)
```

Nå har vi opprettet kolonnen *distance*, og vi kan enkelt hente diverse statistiske verdier: 


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


Her ser vi at sykkelturer i gjennomsnitt skjedde mellom stasjoner som var 1.56 km fra hverandre, og at den største avstanden var 8.17 km. (Hvorfor tror du den minste er avstanden 0 km? Og hva betyr det at medianverdien er 1.38 km?)

Hva om vi ønsker å finne ut om helgesturer i gjennomsnitt er lengre enn hverdagsturer? I forrige seksjon opprettet vi kolonnen *part_of_week*, som nettopp forteller om en tur skjedde på hverdag eller helg. Vi kan nå *gruppere* tabellen etter denne kolonnen: 


```python
grouped = trips.groupby("part_of_week")
```

Vi kan nå tenke oss at tabellen er delt i to; alle rader med verdien *weekday* er i den første gruppen, og alle rader med verdien *weekend* er i den andre gruppen. Hva er poenget med dette? Det ser vi dersom vi prøver å regne ut gjennomsnittet: 


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

* Når tabellen er ugruppert, vil gjennomsnittet av en kolonne bare være et tall.
* Når tabellen er gruppert, får vi ett gjennomsnitt for hver av gruppene.

Resultatet forteller oss at helgeturer i gjennomsnitt er litt lengre enn hverdagsturer.

Vi kan bruke samme metode for å sammenligne ulike grupper i tabellen. Kanskje vi ønsker å sammenligne hver ukedag, med tanke på hvor lenge sykkelturene varer i gjennomsnitt? 


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


Her ser vi at varigheten til sykkelturene i gjennomsnitt er kortest på mandag, tirsdag og onsdag, og lengst på lørdag og søndag. 

**Oppsummering.** I denne seksjonen har vi sett hvordan tabellfunksjonen `apply` kan brukes for å gjøre en operasjon på alle radene i en tabell. Resultatet er en ny kolonne som kan settes inn i tabellen. 

Videre har vi sett at tabellfunksjonen `groupby` kan brukes for å dele tabellen inn i grupper. Når vi regner ut statistiske verdier, får vi én verdi for hver gruppe. Det gjør at vi kan sammenligne gruppene og finne tendenser. 

**Aktivitetsforslag.** Dette forutsetter at du har gjort oppgavene i forrige seksjon.

1. Legg til en ny kolonne i `trips`, som inneholder avstanden mellom *Oslo S* og endestasjonen for turene. *Hint: lag først en funksjon som konverterer en enkelt rad i tabellen til den riktige avstanden.*
2. Hvor nærme ender turene *Oslo S* i gjennomsnitt? 
3. Sammenlign gruppene morgen, ettermiddag, kveld og natt. I hvilken gruppe ender turene i snitt nærmest *Oslo S*, og i hvilken gruppe ender de lengst unna?
4. Sammenlign gruppene helg og hverdag. I hvilken gruppe ender turene nærmest *Oslo S*?

Utfordringsoppgave: Vi har i denne seksjonen sett hvordan man kan gruppere etter én kolonne. Det er også mulig å gruppere etter to kolonner, ved å bruke følgende kommando:
```py
grouped = table.groupby(["column1", "column2"])
``` 
Grupper sykkelturene etter følgende kolonner:

* *part_of_week*: forteller om en tur startet på hverdag eller helg
* *part_of_day*: forteller om tur startet på morgen, ettermiddag, kveld eller natt.

Du må opprette disse kolonnene dersom du ikke har dem. Hent gjennomsnittlige avstander i den grupperte tabellen. Hva forteller svarene deg?

Utfordringsspørsmål: I de siste to seksjonene har du sett at det finnes to versjoner av `apply`; en kolonnefunksjon og en tabellfunksjon. Hva er forskjellen på disse? Hvorfor må du bruke tabellfunksjonen i punkt 1? Kan du gi en regel for når du må bruke tabellfunksjonen?

# Trekke ut ustrukturert data

Vi skal nå se på hvordan vi kan opprette en tabell som kun inneholder informasjon om sykkelstasjonene. Da må vi trekke ut relevant data fra sykkelturtabellen. 

Først lager vi en tabell som kun inneholder de relevante kolonnene i turtabellen (men fortsatt alle radene): 


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
      <td>utenfor Bjørvika visningssenter</td>
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



Nå har vi bare tatt med startstasjonene, men vi må ta høyde for at det kanskje finnes noen stasjoner som bare er brukt som endestasjon:


```python
columns = ["end_station_id", "end_station_name", "end_station_description", "end_station_latitude", "end_station_longitude"]
end_stations = trips[columns]
```

Nå ønsker vi at tabellene `start_stations` og `end_stations` skal ha samme kolonnenavn. Vi endrer kolonnenavnene på følgende måte: 


```python
new_column_names = ["id", "name", "description", "latitude", "longitude"]
start_stations.columns = new_column_names
end_stations.columns = new_column_names
```

Nå har vi to tabeller med akkurat de samme kolonnenavnene. Da kan vi slå dem sammen til en ny tabell:


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
      <td>utenfor Bjørvika visningssenter</td>
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



Nå har vi en tabell som garantert inneholder alle stasjonene. Men siden hver rad i tabellen fortsatt representerer en sykkeltur, vil det være mange duplikasjoner. Vi kan enkelt fjerne duplikasjonene:


```python
stations = stations.drop_duplicates()
```

I tabellen ovenfor ser vi at hver rad har en indeks som kommer fra sykkelturtabellen! Vi ønsker heller å bruke kolonnen *id* som indeks: 


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
      <td>utenfor Bjørvika visningssenter</td>
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



Nå kan vi hente en spesifikk stasjon ved å bruke stasjons-id: 


```python
s = stations.loc["387"]
print(s)
```

    name            Studenterlunden
    description    langs Karl Johan
    latitude              59.914586
    longitude             10.735453
    Name: 387, dtype: object


Videre kan vi hente spesifikke verdier:


```python
print(s["latitude"])
```

    59.914586


Dette er svært nyttig når vi i neste seksjon skal visualisere sykkeldata på kart!

**Oppsummering.** I denne seksjonen har trukket ut ustrukturert data fra en tabell, og opprettet en ny tabell der dataene er strukturert. Vi har gjort det ved å 
- hente bestemte kolonner,
- endre kolonnenavn,
- slå sammen tabeller,
- fjerne duplikasjoner og
- endre indeksering. 


```python
%store trips
%store stations
```

    Stored 'trips' (DataFrame)
    Stored 'stations' (DataFrame)

