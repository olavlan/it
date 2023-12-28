---
title: "Visualisere fordelinger"
figures_to_include:
	- "4-3-3-visualisering_27_0.png"
	- "4-3-3-visualisering_30_0.png"
	- "4-3-3-visualisering_36_0.png"
	- "4-3-3-visualisering_38_0.png"
	- "4-3-3-visualisering_55_0.png"
---

**Kakediagram.** Vi har tidligere sett hvor enkelt det er å finne ut hvordan sykkelturene fordeler seg på ukedagene: 


```python
counts = trips["day_of_week"].value_counts()
counts = counts[weekdays]

print(counts)
```

    day_of_week
    monday       21259
    tuesday      18696
    wednesday    19305
    thursday     18998
    friday       19367
    saturday     19005
    sunday       14751
    Name: count, dtype: int64


Hva om vi nå ønsker å visualisere dette med et kakediagram? Med `plt` kan vi enkelt få til dette med funksjonen `pie`:


```python
plt.pie(counts, labels = counts.index, autopct = '%1.1f%%')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_27_0.png' width=600>
    


Forklaring: 

* Som første parameter gir vi kolonnen som inneholder antall sykkelturer på de ulike dagene.
* I parameteren `labels` gir vi navnet på hver gruppe. I vårt tilfelle henter vi indeksene til kolonnen, som allerede gir oss passende navn.
* Parameteren `autopct = '%1.1f%%'` forteller at andelene skal angis i prosent med én desimal.

På samme måte kan vi visualisere hvilke perioder på dagen som er mest populære: 


```python
counts  = trips["part_of_day"].value_counts()

parts_of_day = ["morning", "afternoon", "evening", "night"]
counts = counts[parts_of_day]

plt.pie(counts, labels = counts.index, autopct = '%1.1f%%')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_30_0.png' width=600>
    


Her ser vi at ettermiddag og morgen er de mest populære periodene på dagen. Men hva om vi ønsker et kakediagram for hverdagsturer, og et kakediagram for helgesturer, slik at vi kan sammenligne gruppene? 

Vi ønsker altså at turtabellen skal deles inn i to grupper; helg og hverdag. Da må vi gruppere etter `part_of_week`:


```python
grouped = trips.groupby("part_of_week")

counts  = grouped["part_of_day"].value_counts()
counts = counts.unstack()

parts_of_day = ["morning", "afternoon", "evening", "night"]
counts = counts[parts_of_day]

print(counts)
```

    part_of_day   morning  afternoon  evening  night
    part_of_week                                    
    weekday         31450      44674    14369   7132
    weekend         10330      15606     7140    680


Merk at vi har brukt funksjonen `unstack` for å gjøre kolonnen `counts` om til en tabell, samt at vi har sortert kolonnene. 

Vi ønsker nå å visualisere fordelingene til hverdag og helg hver for seg. Da må vi hente ut radene i tabellen - husk at funksjonen `loc` brukes for å hente ut en rad:


```python
weekday_counts = counts.loc["weekday"]
weekend_counts = counts.loc["weekend"]

print(weekday_counts)
print()
print(weekend_counts)
```

    part_of_day
    morning      31450
    afternoon    44674
    evening      14369
    night         7132
    Name: weekday, dtype: int64
    
    part_of_day
    morning      10330
    afternoon    15606
    evening       7140
    night          680
    Name: weekend, dtype: int64


Nå er vi klare til å visualisere fordelingene hver for seg. Vi begynner med hverdager:


```python
plt.pie(weekday_counts, labels = weekday_counts.index, autopct = '%1.1f%%')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_36_0.png' width=600>
    


Deretter viser vi fordelingen for helger:


```python
plt.pie(weekend_counts, labels = weekend_counts.index, autopct = '%1.1f%%')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_38_0.png' width=600>
    


Hvilke forskjeller kan du se mellom turer som startet på hverdag og helg? 

**Flere diagrammer med løkke.** I slutten av forrige seksjon la du kanskje merke til at vi gjorde nesten akkurat det samme to ganger? For å opprette flere diagrammer i ett og samme program, kan vi bruke følgende løkke:


```python
for i in range(2):
    plt.plot(0,0, "o")
    filename = f"{i}.pdf"
    plt.savefig(filename)
    plt.close()
```

Med koden over oppretter vi to diagrammer, og lagrer dem som filer med navnene *0.pdf* og *1.pdf*. Merk at når vi er ferdige med én figur og har lagret den, må vi bruke `plt.close()` før vi kan starte på neste figur.

Vi ønsker altså å opprette et diagram for hver av radene i følgende tabell:


```python
print(counts)
```

    part_of_day   morning  afternoon  evening  night
    part_of_week                                    
    weekday         31450      44674    14369   7132
    weekend         10330      15606     7140    680


Husk at vi brukte kommandoen `counts.loc["weekday"]` for å hente den første raden. I stedet for å skrive indeksene *weekday* og *weekend* manuelt, kan de hentes fra variabelen `counts`: 


```python
indices = counts.index
for i in indices:
    print(i)
```

    weekday
    weekend


Nå kan vi opprette et kakediagram for hver av radene:


```python
for i in indices:
    c = counts.loc[i]
    plt.pie(c, labels = c.index, autopct = '%1.1f%%')
    filename = f"piechart-{i}.pdf"
    plt.savefig(filename)
    plt.close()
```

Ved kjøring av denne koden opprettes to filer (*piechart-weekday.pdf* og *piechart-weekend.pdf*) med de ønskede kakediagrammene.

**Søylediagram.** Hva om vi ønsker mer detaljer om når på dagen turene skjer? Vi har sett at omtrent 32% av turer skjer på morgenen, altså mellom 6 og 11, men hvilke klokketimer er mest populære?

Dersom vi ønsker å vite fordelingen av turer på klokketimer, så trenger vi 24 kategorier. Det blir for mye å vise så mange segmenter i et kakediagram, så i dette tilfellet er det fornuftig med et søylediagram i stedet!

Men først må vi opprette en kolonne i turtabellen som inneholder nøyaktig den informasjonen vi ønsker å bruke. I første omgang trenger vi en funksjon som konverterer en datostreng til klokketime: 


```python
def get_hour(date_string):
    date_object = datetime.fromisoformat(date_string)
    return date_object.hour

test = get_hour("2023-07-01 10:27:10")
print(test)
```

    10


Nå kan vi konvertere hele kolonnen *started_at*, og plassere resultatet i en ny kolonne:


```python
trips["hour"] = trips["started_at"].apply(get_hour)
print(trips["hour"])
```

    0          1
    1          3
    2          3
    3          3
    4          3
              ..
    131376    22
    131377    22
    131378    22
    131379    23
    131380    23
    Name: hour, Length: 131381, dtype: int64


Det neste steget er å telle antall forekomster for hver klokketime: 


```python
counts = trips["hour"].value_counts()
counts = counts.sort_index()
print(counts)
```

    hour
    0         3
    1         2
    2         1
    3       584
    4      1917
    5      5305
    6      7680
    7      5575
    8      5763
    9      6989
    10     7767
    11     8006
    12     8643
    13    10734
    14    11649
    15    11219
    16    10066
    17     7969
    18     6353
    19     5385
    20     4353
    21     3391
    22     2022
    23        5
    Name: count, dtype: int64


Merk at vi her har brukt kolonnefunksjonen `sort_index` for å sortere klokketimene i stigende rekkefølge. 

Nå kan vi opprette et søylediagram som viser antall forekomster for hver klokketime:


```python
counts.plot(kind='bar')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_55_0.png' width=600>
    


Her ser vi for eksempel at klokketimen 6 (altså mellom 6:00 og 6:59) er spesielt populær. Vi har altså fått med flere detaljer i fordelingen enn vi kunne med et kakediagram.

**Oppsummering.** I denne seksjonen har vi visualisert hvordan sykkelturene fordeler seg på ulike kategorier. Dersom vi har få kategorier kan vi bruke et kakediagram, mens ved mange kategorier kan vi bruke et søylediagram.

Vi har også sett hvordan vi kan gruppere sykkelturene, og visualisere fordelingen til hver av grupppene. Dette kan gjøres effektivt dersom vi bruker en løkke til å opprette flere diagrammer.

**Aktivitetsforslag 1.** Grupper sykkelturene i hverdag og helg. Opprett et søylediagram for hver av gruppene, som viser hvordan sykkelturene fordeler seg på klokketimer. Hvilke forskjeller kan du finne mellom de to diagrammene? Hva tror du er årsaken til forskjellene? 

**Aktivitetsforslag 2.** Opprett to tabeller; den ene tabellen skal inneholde alle turer som varte kortere enn én time (3600), og den andre tabellen skal inneholde alle turer som varte én time eller lengre. 

1. Bruk kakediagrammer til å vise hvordan korte og lange turer fordeler seg på ukedagene. Hvilke forskjeller finner du? Hva tror du årsaken er?
2. Bruk søylediagrammer til å vise hvordan korte og lange turer fordeler seg på kloketimer. Kommenter resultatet.

