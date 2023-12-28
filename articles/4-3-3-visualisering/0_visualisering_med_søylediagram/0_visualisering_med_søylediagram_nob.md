---
title: "Visualisering med søylediagram"
figures_to_include:
	- "4-3-3-visualisering_9_0.png"
	- "4-3-3-visualisering_11_0.png"
	- "4-3-3-visualisering_19_0.png"
---

I seksjonen *Tabellfunksjoner* så vi at vi kunne gruppere en tabell etter en bestemt kolonne, og deretter finne gjennomsnittlige verdier. På denne måten kan vi for eksempel finne gjennomsnittlig varighet for sykkelturer, gruppert etter ukedag:


```python
grouped = trips.groupby("day_of_week")
means_sec = grouped["duration"].mean()
means = means_sec/60
print(means)
```

    day_of_week
    friday       14.638859
    monday       13.299420
    saturday     16.658971
    sunday       17.167381
    thursday     14.034353
    tuesday      13.239689
    wednesday    13.588347
    Name: duration, dtype: float64


Merk at vi har delt resultatet på 60 for å få svaret i antall minutter. En gjennomsnittlig fredagstur varte omtrent 14.64 minutter, som tilsvarer 14 minutter og 38 sekunder (fordi 64% av ett minutt er 38 sekunder). 

Nå ønsker vi å visualisere disse tallene som et søylediagram. I første omgang er det lurt å sortere verdiene i ønsket rekkefølge. 

Indeksene er *friday*, *monday*, *saturday* og så videre. Vi oppretter en liste med alle indeksene i den rekkefølgen vi ønsker:


```python
weekdays = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"]
```

Nå kan vi bruke skrivemåten `means[weekdays]` for å endre rekkefølgen:


```python
means = means[weekdays]
print(means)
```

    day_of_week
    monday       13.299420
    tuesday      13.239689
    wednesday    13.588347
    thursday     14.034353
    friday       14.638859
    saturday     16.658971
    sunday       17.167381
    Name: duration, dtype: float64


Variabelen `means` inneholder en kolonne med tallverdier, og på denne kan vi bruke funksjonen `plot`:


```python
means.plot(kind='bar')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_9_0.png' width=600>
    


Merk at vi tegner søylene i et *plott*, det vil si et koordinatsystem med en $x$ -og $y$-akse. Det er Python-pakken [*matplotlib.pyplot*](https://matplotlib.org/3.5.3/index.html) som brukes, og vi har importert pakken under navnet `plt`. 

Vi kan bruke `plt` til å markere gjennomsnittlig varighet av alle turer som en striplet linje i koordinatsystemet:


```python
means.plot(kind='bar')

m = trips["duration"].mean()/60
plt.axhline(y=m, linestyle='--', color='black')

plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_11_0.png' width=600>
    


I dette diagrammet er det lett å se at den gjennomsnittlige varigheten til sykkelturer øker når vi kommer nærmere helgen.

Vi kan også lage mer komplekse grupper som vi kan sammenligne. For eksempel lagde vi tidligere en kolonne som forteller hvilken periode på dagen turene skjedde (se løsningsforslag i seksjonen *Kolonnefunksjoner*): 


```python
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


Vi kan nå gruppere tabellen etter kolonnene *day_of_week* og *part_of_day*: 


```python
grouped = trips.groupby(["day_of_week", "part_of_day"])
means = grouped["duration"].mean()
means = means.unstack()
means = means/60
print(means)
```

    part_of_day  afternoon    evening    morning      night
    day_of_week                                            
    friday       15.189377  14.132662  14.957210   9.524581
    monday       13.319349  13.749092  14.062873   9.621954
    saturday     17.156382  15.041252  17.300547  11.460043
    sunday       17.874148  15.005889  18.243728   9.340621
    thursday     14.288915  13.600807  14.872700   9.318157
    tuesday      13.564925  13.161409  13.801724   9.206462
    wednesday    13.732902  13.437937  14.403294   9.688066


Forklaring:

- Operasjonen `means.unstack()` gjør kolonnen om til en tabell, der det er lettere å lese verdiene til de ulike gruppene.
- Vi har igjen delt på 60 for å få verdiene i minutter i stedet for sekunder.

I tabellen ser vi for eksempel at sykkelturer som skjer på en søndag morgen har gjennomsnittlig varighet 15 minutter, mens på tirsdag natt er det i overkant av 9 minutter. 

Nå gjenstår det å sortere verdiene i ønsket rekkefølge. Da må vi skille mellom sortering av rader og kolonner:


```python
parts_of_day = ["morning", "afternoon", "evening", "night"]
weekdays = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"]

means = means[parts_of_day]
means = means.loc[weekdays]

print(means)
```

    part_of_day    morning  afternoon    evening      night
    day_of_week                                            
    monday       14.062873  13.319349  13.749092   9.621954
    tuesday      13.801724  13.564925  13.161409   9.206462
    wednesday    14.403294  13.732902  13.437937   9.688066
    thursday     14.872700  14.288915  13.600807   9.318157
    friday       14.957210  15.189377  14.132662   9.524581
    saturday     17.300547  17.156382  15.041252  11.460043
    sunday       18.243728  17.874148  15.005889   9.340621


For å sortere radene, må vi altså bruke kommandoen `loc`.

Nå kan vi opprette søylediagrammet på akkurat samme måte som tidligere. Merk at denne gangen inneholder `means` en tabell, men vi kan fortsatt bruke funksjonen `plot`: 


```python
means.plot(kind='bar')

m = trips["duration"].mean()/60
plt.axhline(y=m, linestyle='--', color='black')

plt.legend(loc='upper left', fontsize=10, ncol=2)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_19_0.png' width=600>
    


Fra dette søylediagrammet kan vi hente mer spesifikk informasjon. For eksempel ser vi at økningen som skjer i helgen hovedsakelig skyldes sykkelturer som starter på morgen og ettermiddag.

**Oppsummering.** I denne seksjonen har vi sett hvordan vi kan bruke søylediagram til å sammenligne ulike grupper i dataene. Vi gjør følgende tre steg for å oppnå dette:

1. Vi bruker funksjonen `groupby` på tabellen for å opprette en gruppering.
2. Vi bruker funksjonen `mean` på en av kolonnene i den grupperte tabellen. Resultatet er en kolonne som inneholder gjennomsnittet til hver gruppe. 
3. Vi bruker `plot(kind='bar')` på kolonnen vi fikk i forrige steg. Da opprettes et søylediagram, der hver gruppe får en søyle.

Etter steg 2 kan det være aktuelt å gjøre noen mellomsteg:
* Dersom vi har gruppert etter to kolonner, bør vi konvertere resultatet til en tabell med funksjonen `unstack`.
* Vi kan endre rekkefølgen på gruppene slik at søylediagrammet blir mer oversiktlig.

**Aktivitetsforslag 1.** Grupper turtabellen etter ukedag og periode på dagen, og lag et søylediagram som viser gjennomsnittlig avstand mellom start -og sluttstasjon. 

**Aktivitetsforslag 2.** 

Forberedelse: 

1. Velg deg et punkt i Oslo, og opprett en kolonne i turtabellen som forteller hvor nærme turene endte dette punktet (se seksjonen *Tabellfunksjoner* for hjelp).
2. Del inn turtabellen i grupper etter eget ønske (for eksempel ukedag eller periode på dagen). 

Oppgaver: 

1. Hvor nærme ender sykkelturene i gjennomsnitt ditt valgte punkt?
2. Hvilken gruppe av sykkelturer ender i gjennomsnitt nærmest og lengst unna ditt valgte punkt?
3. Sammenlign de ulike gruppene ved å lage et søylediagram.
4. Hva tror du forskjellen mellom gruppene skyldes?

