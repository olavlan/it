---
title: "Visualisera fordelingar"
figures_to_include:
	- "4-3-3-visualisering_27_0.png"
	- "4-3-3-visualisering_30_0.png"
	- "4-3-3-visualisering_36_0.png"
	- "4-3-3-visualisering_38_0.png"
	- "4-3-3-visualisering_55_0.png"
---

**Kakediagram.** Me har tidlegare sett kor enkelt det er å finna ut korleis sykkelturane fordeler seg på vekedagane:


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


Kva om me no ønskjer å visualisera dette med eit kakediagram? Med `plt` kan me enkelt få til dette med funksjonen `pie`:


```python
plt.pie(counts, labels = counts.index, autopct = '%1.1f%%')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_27_0.png' width=600>
    


Forklaring:

* Som første parameter gir me kolonnen som inneheld talet på sykkelturar på dei ulike dagane.
* I parameteren `labels` gir me namnet på kvar gruppe. I vårt tilfelle hentar me indeksane til kolonnen, som allereie gir oss passande namn.
* Parameteren `autopct = '%1.1f%%'` fortel at andelane skal angivast i prosent med éin desimal.

På same måte kan me visualisera kva periodar på dagen som er mest populære:


```python
counts  = trips["part_of_day"].value_counts()

parts_of_day = ["morning", "afternoon", "evening", "night"]
counts = counts[parts_of_day]

plt.pie(counts, labels = counts.index, autopct = '%1.1f%%')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_30_0.png' width=600>
    


Her ser me at ettermiddag og morgon er dei mest populære periodane på dagen. Men kva om me ønskjer eit kakediagram for kvardagsturar, og eit kakediagram for helgesturer, slik at me kan samanlikna gruppene?

Me ønskjer altså at turtabellen skal delast inn i to grupper; helg og kvardag. Då må me gruppera etter `part_of_week`:


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


Merk at me har brukt funksjonen `unstack` for å gjera kolonnen `counts` om til ein tabell, og dessutan at me har sortert kolonnane.

Me ønskjer no å visualisera fordelingane til kvardag og helg kvar for seg. Då må me henta ut radene i tabellen - hugs at funksjonen `loc` blir brukt for å henta ut ei rad:


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


No er me klare til å visualisera fordelingane kvar for seg. Me byrjar med kvardagar:


```python
plt.pie(weekday_counts, labels = weekday_counts.index, autopct = '%1.1f%%')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_36_0.png' width=600>
    


Deretter viser me fordelinga for helgar:


```python
plt.pie(weekend_counts, labels = weekend_counts.index, autopct = '%1.1f%%')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_38_0.png' width=600>
    


Kva forskjellar kan du sjå mellom turar som starta på kvardag og helg?

**Fleire diagram med løkke.** I slutten av førre seksjon la du kanskje merka til at me gjorde nesten akkurat det same to gonger? For å oppretta fleire diagram i eitt og same program, kan me bruka følgjande løkke:


```python
for i in range(2):
    plt.plot(0,0, "o")
    filename = f"{i}.pdf"
    plt.savefig(filename)
    plt.close()
```

Med koden over opprettar me to diagram, og lagrar dei som filer med namna *0.PDF* og *1.PDF*. Merk at når me er ferdige med éin figur og har lagra han, må me bruka `plt.close()` før me kan starta på neste figur.

Me ønskjer altså å oppretta eit diagram for kvar av radene i følgjande tabell:


```python
print(counts)
```

part_of_day   morning  afternoon  evening  night
part_of_week
weekday         31450      44674    14369   7132
weekend         10330      15606     7140    680


Hugs at me brukte kommandoen `counts.loc["weekday"]` for å henta den første rada. I staden for å skriva indeksane *weekday* og *weekend* manuelt, kan dei hentast frå variabelen `counts`:


```python
indices = counts.index
for i in indices:
    print(i)
```

weekday
weekend


No kan me oppretta eit kakediagram for kvar av radene:


```python
for i in indices:
    c = counts.loc[i]
    plt.pie(c, labels = c.index, autopct = '%1.1f%%')
    filename = f"piechart-{i}.pdf"
    plt.savefig(filename)
    plt.close()
```

Ved køyring av denne koden blir to filer oppretta (*piechart-weekday.PDF* og *piechart-weekend.PDF*) med dei ønskte kakediagramma.

**Søylediagram.** Kva om me ønskjer meir detaljar om når på dagen turane skjer? Me har sett at omtrent 32% av turar skjer på morgonen, altså mellom 6 og 11, men kva klokketimar er mest populære?

Dersom me ønskjer å vita fordelinga av turar på klokketimar, så treng me 24 kategoriar. Det blir for mykje å visa så mange segment i eit kakediagram, så i dette tilfellet er det fornuftig med eit søylediagram i staden!

Men først må me oppretta ein kolonne i turtabellen som inneheld nøyaktig den informasjonen me ønskjer å bruka. I første omgang treng me ein funksjon som konverterer ein datostreng til klokketime:


```python
def get_hour(date_string):
    date_object = datetime.fromisoformat(date_string)
    return date_object.hour

test = get_hour("2023-07-01 10:27:10")
print(test)
```

    10


No kan me konvertera heile kolonnen *started_at*, og plassera resultatet i ein ny kolonne:


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


Det neste steget er å telja førekomstar for kvar klokketime:


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


Merk at me her har brukt kolonnefunksjonen `sort_index` for å sortera klokketimane i stigande rekkjefølgje.

No kan me oppretta eit søylediagram som viser talet på førekomstar for kvar klokketime:


```python
counts.plot(kind='bar')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_55_0.png' width=600>
    


Her ser me til dømes at klokketimen 6 (altså mellom 6:00 og 6:59) er spesielt populær. Me har altså fått med fleire detaljar i fordelinga enn me kunne med eit kakediagram.

**Oppsummering.** I denne seksjonen har me visualisert korleis sykkelturane fordeler seg på ulike kategoriar. Dersom me har få kategoriar kan me bruka eit kakediagram, medan ved mange kategoriar kan me bruka eit søylediagram.

Me har også sett korleis me kan gruppera sykkelturane, og visualisera fordelinga til kvar av gruppene. Dette kan gjerast effektivt dersom me bruker ei løkke til å oppretta fleire diagram.

**Aktivitetsforslag 1.** Grupper sykkelturane i kvardag og helg. Opprett eit søylediagram for kvar av gruppene, som viser korleis sykkelturane fordeler seg på klokketimar. Kva forskjellar kan du finna mellom dei to diagramma? Kva trur du er årsaka til forskjellane?

**Aktivitetsforslag 2.** Opprett to tabellar; den eine tabellen skal innehalda alle turar som varte kortare enn éin time (3600), og den andre tabellen skal innehalda alle turar som varte éin time eller lengre.

1. Bruk kakediagram til å visa korleis korte og lange turar fordeler seg på vekedagane. Kva forskjellar finn du? Kva trur du årsaka er?
2. Bruk søylediagram til å visa korleis korte og lange turar fordeler seg på kloketimer. Kommenter resultatet.

