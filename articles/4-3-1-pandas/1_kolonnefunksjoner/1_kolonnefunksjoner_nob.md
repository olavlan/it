---
title: "Kolonnefunksjoner"
figures_to_include:
---

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


