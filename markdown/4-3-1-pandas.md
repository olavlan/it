```python
import requests
import json
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime
from geopy import distance
from scipy.stats import gaussian_kde
```

## Introduksjon til pandas

Kort sagt er [*pandas*](https://pandas.pydata.org/) en Python-pakke som gjør det mer effektivt å drive databehandling. I de forrige seksjonene jobbet vi med dictionary og lister, mens i *pandas* brukes *tabeller*. Vi kan opprette tabeller og utføre operasjoner på dem.

Først viser vi hvordan man kan konvertere en dictionary til en tabell: 


```python
data = [
    {"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo", "number_of_children": 0},
    {"fornavn": "Kari", "etternavn": "Svendsen", "alder": 42, "bosted": "Trondheim", "number_of_children": 1},
    {"fornavn": "Per", "etternavn": "Hansen", "alder": 64, "bosted": "Tromsø", "number_of_children": 3}
]

people = pd.DataFrame(data)

print(people)
```

      fornavn etternavn  alder     bosted  number_of_children
    0     Ola  Nordmann     17       Oslo                   0
    1    Kari  Svendsen     42  Trondheim                   1
    2     Per    Hansen     64     Tromsø                   3


Legg merke til at vi har importert *pandas* under navnet *pd*, som er en vanlig praksis. Deretter har vi opprettet et såkalt *DataFrame*-objekt.  

I pandas finnes to typer objekter; *DataFrame* og *Series*. En *DataFrame* er en tabell, mens en *Series* er en kolonne i tabellen - fra nå av skal vi holde oss til begrepene *tabell* og *kolonne*. 

La oss hente en kolonne:


```python
ages = people["alder"]
print(ages)
```

    0    17
    1    42
    2    64
    Name: alder, dtype: int64


I pandas bruker vi altså skrivemåten `table["column_name"]` for å hente en bestemt kolonne. 

Pandas gir oss mange nyttige funksjoner for tabeller og kolonner. Et eksempel på en *kolonnefunksjon* er `mean`, som regner ut gjennomsnittet av alle verdiene:


```python
average_age = ages.mean()
print(average_age)
```

    41.0


**Importere data.** All data som er på tabellform kan settes inn i en pandas-tabell. For å laste inn data fra en *Excel*-fil, brukes følgende kommando: 

```py
table = pd.read_excel("path_to_file.xls", sheet_name="Sheet1")
```
For å laste inn data fra en *CSV*-fil, brukes funksjonen `read_csv` i stedet. 

Men hva med sykkeldataene, som er lagret med *JSON*? Vi har sett at en slik fil består av attributter, objekter og lister, som ikke nødvendigvis kan konverteres til en tabell. 

Sykkeldataene er imidlertid strukturert på en enkel måte:

```json
[
    {
        "started_at": "2023-07-01 01:22:38.878000+00:00",
        "ended_at": "2023-07-01 01:40:04.748000+00:00",
        "duration": 1045,
        "start_station_id": "387",
        "start_station_name": "Studenterlunden",
        "start_station_description": "langs Karl Johan",
        "start_station_latitude": 59.914586,
        "start_station_longitude": 10.735453,
        "end_station_id": "499",
        "end_station_name": "Bjerregaards gate",
        "end_station_description": "ovenfor Fredrikke Qvams gate",
        "end_station_latitude": 59.925488,
        "end_station_longitude": 10.746058
    },
    {
        "started_at": "2023-07-01 03:02:43.726000+00:00",
        "ended_at": "2023-07-01 03:13:45.064000+00:00",
        "duration": 661,
        "start_station_id": "2315",
        "start_station_name": "Rostockgata",
        "start_station_description": "utenfor Bj\u00f8rvika visningssenter",
        "start_station_latitude": 59.90691970255054,
        "start_station_longitude": 10.760311802881915,
        "end_station_id": "410",
        "end_station_name": "Landstads gate",
        "end_station_description": "langs Uelands gate",
        "end_station_latitude": 59.929005,
        "end_station_longitude": 10.7496755
    }
]
```

Vi merker oss at alle turene har de samme datafeltene, nemlig *duration*, *end_station_description*, og så videre. Ved å skrive disse som kolonner, og hver sykkeltur som en rad, får vi følgende tabell:

| started_at                       | ended_at                         | duration | start_station_id | start_station_name | start_station_description       | start_station_latitude | start_station_longitude | end_station_id | end_station_name  | end_station_description      | end_station_latitude | end_station_longitude |
|----------------------------------|----------------------------------|----------|------------------|--------------------|---------------------------------|------------------------|-------------------------|----------------|-------------------|------------------------------|----------------------|-----------------------|
| 2023-07-01 01:22:38.878000+00:00 | 2023-07-01 01:40:04.748000+00:00 | 1045     | 387              | Studenterlunden    | langs Karl Johan                | 59.914586              | 10.735453               | 499            | Bjerregaards gate | ovenfor Fredrikke Qvams gate | 59.925488            | 10.746058             |
| 2023-07-01 03:02:43.726000+00:00 | 2023-07-01 03:13:45.064000+00:00 | 661      | 2315             | Rostockgata        | utenfor Bjørvika visningssenter | 59.90691970255054      | 10.760311802881915      | 410            | Landstads gate    | langs Uelands gate           | 59.929005            | 10.7496755            |

Vi kan konkludere med at sykkeldataene kan settes inn i en tabell. Hvordan gjør vi dette?

Som vist i seksjonen *Innhenting og inspeksjon av data*, kan vi begynne med å laste dataene inn i en dictionary:


```python
url = "https://data.urbansharing.com/oslobysykkel.no/trips/v1/2023/07.json"
page = requests.get(url).text
data = json.loads(page)
```

 Når dette er gjort, kan vi legge dadtaene inn i en tabell, som vist i starten av seksjonen: 


```python
trips = pd.DataFrame(data)
trips.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>started_at</th>
      <th>ended_at</th>
      <th>duration</th>
      <th>start_station_id</th>
      <th>start_station_name</th>
      <th>start_station_description</th>
      <th>start_station_latitude</th>
      <th>start_station_longitude</th>
      <th>end_station_id</th>
      <th>end_station_name</th>
      <th>end_station_description</th>
      <th>end_station_latitude</th>
      <th>end_station_longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-01 01:22:38.878000+00:00</td>
      <td>2023-07-01 01:40:04.748000+00:00</td>
      <td>1045</td>
      <td>387</td>
      <td>Studenterlunden</td>
      <td>langs Karl Johan</td>
      <td>59.914586</td>
      <td>10.735453</td>
      <td>499</td>
      <td>Bjerregaards gate</td>
      <td>ovenfor Fredrikke Qvams gate</td>
      <td>59.925488</td>
      <td>10.746058</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2023-07-01 03:02:43.726000+00:00</td>
      <td>2023-07-01 03:13:45.064000+00:00</td>
      <td>661</td>
      <td>2315</td>
      <td>Rostockgata</td>
      <td>utenfor Bjørvika visningssenter</td>
      <td>59.906920</td>
      <td>10.760312</td>
      <td>410</td>
      <td>Landstads gate</td>
      <td>langs Uelands gate</td>
      <td>59.929005</td>
      <td>10.749676</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-07-01 03:13:28.322000+00:00</td>
      <td>2023-07-01 03:25:26.944000+00:00</td>
      <td>718</td>
      <td>384</td>
      <td>Vår Frelsers gravlund</td>
      <td>langs Ullevålsveien</td>
      <td>59.919440</td>
      <td>10.743765</td>
      <td>551</td>
      <td>Olaf Ryes plass</td>
      <td>langs Sofienberggata</td>
      <td>59.922425</td>
      <td>10.758182</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-07-01 03:15:18.482000+00:00</td>
      <td>2023-07-01 03:32:54.956000+00:00</td>
      <td>1056</td>
      <td>584</td>
      <td>Henrik Wergelands allé</td>
      <td>ved Bogstadveien</td>
      <td>59.926894</td>
      <td>10.720789</td>
      <td>583</td>
      <td>Galgeberg</td>
      <td>langs St. Halvards gate</td>
      <td>59.907076</td>
      <td>10.779164</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-07-01 03:22:07.761000+00:00</td>
      <td>2023-07-01 03:25:41.579000+00:00</td>
      <td>213</td>
      <td>600</td>
      <td>Dyvekes bru</td>
      <td>ved skatepark</td>
      <td>59.905323</td>
      <td>10.768958</td>
      <td>465</td>
      <td>Bjørvika</td>
      <td>under broen Nylandsveien</td>
      <td>59.909006</td>
      <td>10.756180</td>
    </tr>
  </tbody>
</table>
</div>



Her ser vi et eksempel på en nyttig tabellfunksjon, nemlig `head`, som skriver ut de første radene i tabellen. Vi bør alltid gjøre dette for å sjekke at tabellen har blitt opprettet riktig. 

Vi kan nå hente ut en kolonne og regne ut gjennomsnittet av verdiene: 


```python
durations = trips["duration"]
print(durations.mean())
```

    873.4412814638342


Så enkelt var det å finne den gjennomsnittlige variheten til sykkelturene!

Videre kan vi trekke ut sykkelturer som tilfredsstiller et bestemt krav, for eksempel at varigheten er mindre enn 180 sekunder (tre minutter):


```python
short_trips = trips[trips["duration"] < 180] 
short_trips.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>started_at</th>
      <th>ended_at</th>
      <th>duration</th>
      <th>start_station_id</th>
      <th>start_station_name</th>
      <th>start_station_description</th>
      <th>start_station_latitude</th>
      <th>start_station_longitude</th>
      <th>end_station_id</th>
      <th>end_station_name</th>
      <th>end_station_description</th>
      <th>end_station_latitude</th>
      <th>end_station_longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>2023-07-01 04:55:13.425000+00:00</td>
      <td>2023-07-01 04:56:45.208000+00:00</td>
      <td>91</td>
      <td>2350</td>
      <td>Blindern T-Bane</td>
      <td>ved Blindernveien</td>
      <td>59.940252</td>
      <td>10.716724</td>
      <td>2350</td>
      <td>Blindern T-Bane</td>
      <td>ved Blindernveien</td>
      <td>59.940252</td>
      <td>10.716724</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2023-07-01 04:57:18.873000+00:00</td>
      <td>2023-07-01 04:59:56.660000+00:00</td>
      <td>157</td>
      <td>442</td>
      <td>Vulkan</td>
      <td>ved Maridalsveien</td>
      <td>59.922510</td>
      <td>10.751010</td>
      <td>463</td>
      <td>Schous plass trikkestopp</td>
      <td>ved biblioteket</td>
      <td>59.920728</td>
      <td>10.759486</td>
    </tr>
    <tr>
      <th>56</th>
      <td>2023-07-01 05:30:20.792000+00:00</td>
      <td>2023-07-01 05:32:35.367000+00:00</td>
      <td>134</td>
      <td>584</td>
      <td>Henrik Wergelands allé</td>
      <td>ved Bogstadveien</td>
      <td>59.926894</td>
      <td>10.720789</td>
      <td>579</td>
      <td>Bogstadveien</td>
      <td>ved Sporveisgata</td>
      <td>59.924732</td>
      <td>10.724628</td>
    </tr>
    <tr>
      <th>65</th>
      <td>2023-07-01 05:41:52.369000+00:00</td>
      <td>2023-07-01 05:43:44.970000+00:00</td>
      <td>112</td>
      <td>600</td>
      <td>Dyvekes bru</td>
      <td>ved skatepark</td>
      <td>59.905323</td>
      <td>10.768958</td>
      <td>737</td>
      <td>Munkegata</td>
      <td>langs Oslo gate</td>
      <td>59.908255</td>
      <td>10.767800</td>
    </tr>
    <tr>
      <th>71</th>
      <td>2023-07-01 05:47:06.312000+00:00</td>
      <td>2023-07-01 05:50:00.209000+00:00</td>
      <td>173</td>
      <td>737</td>
      <td>Munkegata</td>
      <td>langs Oslo gate</td>
      <td>59.908255</td>
      <td>10.767800</td>
      <td>600</td>
      <td>Dyvekes bru</td>
      <td>ved skatepark</td>
      <td>59.905323</td>
      <td>10.768958</td>
    </tr>
  </tbody>
</table>
</div>



Som forventet får vi en ny tabell med radene som tilfredsstiller kravet. Men hvordan gjorde vi egentlig dette? Hva betyr det å skrive `trips[trips["duration"] < 180]`? 

Vi er jo vant til å bruke indekser, som for eksempel `trips[:10]` for å hente de ti første turene. Men siden vi nå jobber med en pandas-tabell, har vi flere muligheter - i stedet for indekser kan vi skrive en betingelse! I dette tilfellet er betingelsen at kolonnen *duration* har en tallverdi som er mindre enn 180. Da vil *pandas* sørge for å hente ut alle radene der betingelsen stemmer!

**Oppsummering.** I denne seksjonen har vi sett at pandas gir oss muligheten til å jobbe med to typer objekter; tabeller og kolonner. Vi har sett hvordan tabeller i noen tilfeller kan opprettes fra *JSON*-filer. Videre har vi sett hvordan vi henter spesifikke kolonner fra en tabell, samt hente rrader som tilfredsstiller en betingelse.

## Kolonnefunksjoner

En viktig fordel med pandas er at vi ikke trenger løkker for å gjøre operasjoner på alle verdiene i en kolonne, eller alle radene i en tabell. Det skal vi se nærmere på i de to neste seksjonene.

Hva om vi for eksempel ønsker å hente alle sykkelturer som startet på en mandag? I stedet for å bruke en løkke, ønsker vi å skrive noe sånt som:

```py
monday_trips = trips[trips["day_of_week"]=="monday"]
```

Problemet er at tabellen vår ikke har en kolonne som forteller ukedagen. Det eneste vi har er kolonnen *started_at*, som inneholder datostrenger: 


```python
print(trips["started_at"])
```

    0         2023-07-01 01:22:38.878000+00:00
    1         2023-07-01 03:02:43.726000+00:00
    2         2023-07-01 03:13:28.322000+00:00
    3         2023-07-01 03:15:18.482000+00:00
    4         2023-07-01 03:22:07.761000+00:00
                            ...               
    131376    2023-07-31 22:56:28.774000+00:00
    131377    2023-07-31 22:57:48.437000+00:00
    131378    2023-07-31 22:59:07.894000+00:00
    131379    2023-07-31 23:21:56.183000+00:00
    131380    2023-07-31 23:21:56.775000+00:00
    Name: started_at, Length: 131381, dtype: object


For å oppnå det vi ønsker, må vi opprette en ny kolonne i tabellen, der datostrengene er konvertert til ukedag. 

Det første steget er å opprette en funksjon som konverterer **én** datostreng til riktig ukedag:


```python
days_of_week = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"]

def get_day_of_week(date_string):
    date_object = datetime.fromisoformat(date_string)
    i = date_object.weekday()
    return days_of_week[i]

test = get_day_of_week("2023-07-01 10:27:10")
print(test)
```

    saturday


*Denne koden er basert på det vi lærte i seksjonen* Håndtering av dato og tid. 

Med pandas kan vi nå kjøre denne funksjonen på alle verdiene i kolonnen *started_at*: 


```python
test = trips["started_at"].apply(get_day_of_week)
print(test)
```

    0         saturday
    1         saturday
    2         saturday
    3         saturday
    4         saturday
                ...   
    131376      monday
    131377      monday
    131378      monday
    131379      monday
    131380      monday
    Name: started_at, Length: 131381, dtype: object


Som forventet får vi en ny kolonne tilbake, der alle datostrengene har blitt konvertert til riktig ukedag. 

Kolonnefunksjonen `apply` brukes for å konvertere alle verdiene i en kolonne. Som parameter må vi gi navnet på en funksjon som konverterer **én** verdi. 

Det er viktig å huske at `apply` ikke gjør endringer på den originale kolonnen, men gir oss en ny kolonne. For å ta vare på den nye kolonnen, kan vi legge den til i tabellen:


```python
trips["day_of_week"] = trips["started_at"].apply(get_day_of_week)
```

For å opprette en ny kolonne bruker vi altså skrivemåten `table["new_column_name"] = new_column`. Her er det viktig at variabelen `new_column` er kompatibel med tabellen. I eksempelet ovenfor har vi ingen problemer, fordi den nye kolonnen er laget ved å konvertere en kolonne som allerede eksisterer i tabellen. Som regel er det slik vi oppretter nye kolonner. 

Med den nye kolonnen kan vi enkelt hente alle turer som startet på en mandag: 


```python
monday_trips = trips[trips["day_of_week"]=="monday"]
```

Nå har vi fått en tabell som inneholder alle mandagsturer. Men dersom vi ønsker å telle antall turer på de forskjellige ukedagene, kan vi i stedet bruke en svært nyttig kolonnefunksjon:


```python
counts = trips["day_of_week"].value_counts()
print(counts)
```

    day_of_week
    monday       21259
    friday       19367
    wednesday    19305
    saturday     19005
    thursday     18998
    tuesday      18696
    sunday       14751
    Name: count, dtype: int64


Her har vi hentet kolonnen *day_of_week*, og telt antall forekomster av hver verdi. Resultatet forteller oss at mandag er den mest populære dagen, med 21259 sykkelturer. Dersom vi ønsker fordelingen i prosent, kan vi legge til følgende parameter: 


```python
counts = trips["day_of_week"].value_counts(normalize=True)
print(counts)
```

    day_of_week
    monday       0.161812
    friday       0.147411
    wednesday    0.146939
    saturday     0.144656
    thursday     0.144602
    tuesday      0.142304
    sunday       0.112277
    Name: proportion, dtype: float64


Vi ser at omtrent 16.2% av sykkelturene skjedde på mandager. 

Hva om vi kun er interessert i fordelingen mellom hverdag og helg? Da legger vi til en kolonne i tabellen som inneholder nøyaktig den informasjonen vi ønsker, nemlig om en tur skjedde på en hverdag eller helg. Først må vi definere en funksjon som kan konvertere **én** datostreng til riktig verdi:


```python
def get_part_of_week(date_string):
    date_object = datetime.fromisoformat(date_string)
    i = date_object.weekday()
    if i < 5:
        return "weekday"
    else:
        return "weekend"

test = get_part_of_week("2023-07-01 10:27:10")
print(test)
```

    weekend


Nå kan vi opprette en ny kolonne ved å konvertere alle verdiene i *started_at*:


```python
trips["part_of_week"] = trips["started_at"].apply(get_part_of_week)
print(trips["part_of_week"])
```

    0         weekend
    1         weekend
    2         weekend
    3         weekend
    4         weekend
               ...   
    131376    weekday
    131377    weekday
    131378    weekday
    131379    weekday
    131380    weekday
    Name: part_of_week, Length: 131381, dtype: object


Til slutt kan vi finne den prosentvise fordelingen mellom hverdag og helg:


```python
counts = trips["part_of_week"].value_counts(normalize=True)
print(counts)
```

    part_of_week
    weekday    0.743068
    weekend    0.256932
    Name: proportion, dtype: float64


Vi ser at omtrent 74.3 % av turene skjedde på hverdager. 

**Oppsummering.** I denne seksjonen har vi sett hvordan kolonnefunksjonen `apply` kan brukes for å konvertere alle verdiene i en kolonne. Da får vi en ny kolonne som vi kan sette inn i tabellen. For å bruke `apply` må vi ha definert en funksjon som konverterer **én** verdi. 

Videre har vi sett hvordan kolonnefunksjonen `value_counts`kan brukes til å finne fordelingen av verdier i en kolonne. 

**Aktivitetsforslag.**

1. Legg til en ny kolonne i `trips` som inneholder klokketimen turene startet på. Denne kolonnen skal altså inneholde verdier mellom 0 og 23. *Hint: Lag først en funksjon som konverterer en datostreng til riktig klokketime.*
2. Finn prosentfordelingen av turer på klokketimer. Hvilken klokketime er mest og minst populær? 
3. Lag en funksjon som tar klokketime som inndata, og som gir en av følgende strenger som utdata: *morning*, *afternoon*, *evening*, *night*. Du kan selv velge hvilke klokketimer som svarer til de ulike strengene.
4. Legg til en kolonne i `trips` som forteller hvilken periode av dagen en tur startet på. Verdiene i kolonnen skal altså være strengene fra forrige punkt. *Hint: hvilken kolonne må du konvertere, og hvilken funksjon kan du bruke til å konvertere den?*

**Løsningsforslag.**

Vi lager en funksjon som konverterer en datostreng til ønsket verdi: 


```python
def get_part_of_day(date_string):
    date_object = datetime.fromisoformat(date_string)
    hour = date_object.hour
    if hour < 6:
        return "night"
    elif hour < 12:
        return "morning"
    elif hour < 18:
        return "afternoon"
    else:
        return "evening"

test = get_part_of_day("2023-07-01 10:27:10")
print(test)
```

    morning


Vi kan nå bruke denne funksjonen på alle datostrengene i kolonnen *started_at*. Resultatet kan legges til som en ny kolonne i turtabellen:


```python
trips["part_of_day"] = trips["started_at"].apply(get_part_of_day)
print(trips["part_of_day"])
```

    0           night
    1           night
    2           night
    3           night
    4           night
               ...   
    131376    evening
    131377    evening
    131378    evening
    131379    evening
    131380    evening
    Name: part_of_day, Length: 131381, dtype: object


## Tabellfunksjoner

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

## Trekke ut ustrukturert data

Vi skal nå se på hvordan vi kan opprette en tabell som kun inneholder informasjon om sykkelstasjonene. Da må vi trekke ut relevant data fra sykkelturtabellen. 

Først lager vi en tabell som kun inneholder de relevante kolonnene i turtabellen (men fortsatt alle radene): 


```python
columns = ["start_station_id", "start_station_name", "start_station_description", "start_station_latitude", "start_station_longitude"]
start_stations = trips[columns]
start_stations.head()
```




<div>
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

