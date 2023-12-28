---
title: "Kolonnefunksjonar"
figures_to_include:
---

Ein viktig fordel med pandas er at me ikkje treng løkker for å gjera operasjonar på alle verdiane i ein kolonne, eller alle radene i ein tabell. Det skal me sjå nærare på i dei to neste seksjonane.

Kva om me til dømes ønskjer å henta alle sykkelturar som starta på ein måndag? I staden for å bruka ei løkke, ønskjer me å skriva noko sånt som:

```py
monday_trips = trips[trips["day_of_week"]=="monday"]
```

Problemet er at tabellen vår ikkje har ein kolonne som fortel vekedagen. Det einaste me har er kolonnen *started_at*, som inneheld datostrenger:


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


For å oppnå det me ønskjer, må me oppretta ein ny kolonne i tabellen, der datostrengene er konverterte til vekedag.

Det første steget er å oppretta ein funksjon som konverterer **éin** datostreng til rett vekedag:


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


*Denne koden er basert på det me lærte i seksjonen* Håndtering av dato og tid.

Med pandas kan me no køyra denne funksjonen på alle verdiane i kolonnen *started_at*:


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


Som forventa får me ein ny kolonne tilbake, der alle datostrengene har vorte konverterte til rett vekedag.

Kolonnefunksjonen `apply` blir brukt for å konvertera alle verdiane i ein kolonne. Som parameter må me gi namnet på ein funksjon som konverterer **éin** verdi.

Det er viktig å hugsa at `apply` ikkje gjer endringar på den originale kolonnen, men gir oss ein ny kolonne. For å ta vare på den nye kolonnen, kan me leggja han til i tabellen:


```python
trips["day_of_week"] = trips["started_at"].apply(get_day_of_week)
```

For å oppretta ein ny kolonne bruker me altså skrivemåten `table["new_column_name"] = new_column`. Her er det viktig at variabelen `new_column` er kompatibel med tabellen. I dømet ovanfor har me ingen problem, fordi den nye kolonnen er laga ved å konvertera ein kolonne som allereie eksisterer i tabellen. Som regel er det slik me opprettar nye kolonnar.

Med den nye kolonnen kan me enkelt henta alle turar som starta på ein måndag:


```python
monday_trips = trips[trips["day_of_week"]=="monday"]
```

No har me fått ein tabell som inneheld alle måndagsturar. Men dersom me ønskjer å telja turar på dei ulike vekedagane, kan me i staden bruka ein svært nyttig kolonnefunksjon:


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


Her har me henta kolonnen *day_of_week*, og talt førekomstar av kvar verdi. Resultatet fortel oss at måndag er den mest populære dagen, med 21259 sykkelturar. Dersom me ønskjer fordelinga i prosent, kan me leggja til følgjande parameter:


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


Me ser at omtrent 16.2% av sykkelturane skjedde på måndagar.

Kva om me berre er interesserte i fordelinga mellom kvardag og helg? Då legg me til ein kolonne i tabellen som inneheld nøyaktig den informasjonen me ønskjer, nemleg om ein tur skjedde på ein kvardag eller helg. Først må me definera ein funksjon som kan konvertera **éin** datostreng til rett verdi:


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


No kan me oppretta ein ny kolonne ved å konvertera alle verdiane i *started_at*:


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


Til slutt kan me finna den prosentvise fordelinga mellom kvardag og helg:


```python
counts = trips["part_of_week"].value_counts(normalize=True)
print(counts)
```

part_of_week
weekday    0.743068
weekend    0.256932
Name: proportion, dtype: float64


Me ser at omtrent 74.3 % av turane skjedde på kvardagar.

**Oppsummering.** I denne seksjonen har me sett korleis kolonnefunksjonen `apply` kan brukast for å konvertera alle verdiane i ein kolonne. Då får me ein ny kolonne som me kan setja inn i tabellen. For å bruka `apply` må me ha definert ein funksjon som konverterer **éin** verdi.

Vidare har me sett korleis kolonnefunksjonen `value_counts`kan brukast til å finna fordelinga av verdiar i ein kolonne.

**Aktivitetsforslag.**

1. Legg til ein ny kolonne i `trips` som inneheld klokketimen turane starta på. Denne kolonnen skal altså innehalda verdiar mellom 0 og 23. *Hint: Lag først ein funksjon som konverterer ein datostreng til rett klokketime.*
2. Finn prosentfordelinga av turar på klokketimar. Kva klokketime er mest og minst populær?
3. Lag ein funksjon som tek klokketime som inndata, og som gir ein av følgjande strenger som utdata: *morning*, *afternoon*, *evening*, *night*. Du kan sjølv velja kva klokketimar som svarer til dei ulike strengene.
4. Legg til ein kolonne i `trips` som fortel kva periode av dagen ein tur starta på. Verdiane i kolonnen skal altså vera strengene frå førre punkt. *Hint: kva kolonne må du konvertera, og kva funksjon kan du bruka til å konvertera han?*

**Løysingsforslag.**

Me lagar ein funksjon som konverterer ein datostreng til ønskt verdi:


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


Me kan no bruka denne funksjonen på alle datostrengene i kolonnen *started_at*. Resultatet kan leggjast til som ein ny kolonne i turtabellen:


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


