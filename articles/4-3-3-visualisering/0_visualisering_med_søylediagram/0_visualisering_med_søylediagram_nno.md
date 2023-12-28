---
title: "Visualisering med søylediagram"
figures_to_include:
	- "4-3-3-visualisering_9_0.png"
	- "4-3-3-visualisering_11_0.png"
	- "4-3-3-visualisering_19_0.png"
---

I seksjonen *Tabellfunksjoner* såg me at me kunne gruppera ein tabell etter ein bestemd kolonne, og deretter finna gjennomsnittlege verdiar. På denne måten kan me til dømes finna gjennomsnittleg varigheit for sykkelturar, gruppert etter vekedag:


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


Merk at me har delt resultatet på 60 for å få svaret i talet på minutt. Ein gjennomsnittleg fredagstur varte omtrent 14.64 minutt, som svarer til 14 minutt og 38 sekund (fordi 64% av eitt minutt er 38 sekund).

No ønskjer me å visualisera desse tala som eit søylediagram. I første omgang er det lurt å sortera verdiane i ønskt rekkjefølgje.

Indeksane er *friday*, *monday*, *saturday* og så vidare. Me opprettar ei liste med alle indeksane i den rekkjefølgja me ønskjer:


```python
weekdays = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"]
```

No kan me bruka skrivemåten `means[weekdays]` for å endra rekkjefølgja:


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


Variabelen `means` inneheld ein kolonne med talverdiar, og på denne kan me bruka funksjonen `plot`:


```python
means.plot(kind='bar')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_9_0.png' width=600>
    


Merk at me teiknar søylene i eit *plott*, det vil seia eit koordinatsystem med ein $x$ -og $y$-akse. Det er Python-pakken [*matplotlib.pyplot*](https://matplotlib.org/3.5.3/index.html) som blir brukt, og me har importert pakken under namnet `plt`.

Me kan bruka `plt` til å markera gjennomsnittleg varigheit av alle turar som ein striplet linje i koordinatsystemet:


```python
means.plot(kind='bar')

m = trips["duration"].mean()/60
plt.axhline(y=m, linestyle='--', color='black')

plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_11_0.png' width=600>
    


I dette diagrammet er det lett å sjå at den gjennomsnittlege varigheita til sykkelturar aukar når me kjem nærare helga.

Me kan også laga meir komplekse grupper som me kan samanlikna. Til dømes laga me tidlegare ein kolonne som fortel kva periode på dagen turane skjedde (sjå løysingsforslag i seksjonen *Kolonnefunksjoner*):


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


Me kan no gruppera tabellen etter kolonnane *day_of_week* og *part_of_day*:


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

- Operasjonen `means.unstack()` gjer kolonnen om til ein tabell, der det er lettare å lesa verdiane til dei ulike gruppene.
- Me har igjen delt på 60 for å få verdiane i minutt i staden for sekund.

I tabellen ser me til dømes at sykkelturar som skjer på ein søndag morgon har gjennomsnittleg varigheit 15 minutt, medan på tysdag natt er det i overkant av 9 minutt.

No står det att å sortera verdiane i ønskt rekkjefølgje. Då må me skilja mellom sortering av rader og kolonnar:


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


For å sortera radene, må me altså bruka kommandoen `loc`.

No kan me oppretta søylediagrammet på akkurat same måte som før. Merk at denne gongen inneheld `means` ein tabell, men me kan framleis bruka funksjonen `plot`:


```python
means.plot(kind='bar')

m = trips["duration"].mean()/60
plt.axhline(y=m, linestyle='--', color='black')

plt.legend(loc='upper left', fontsize=10, ncol=2)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_19_0.png' width=600>
    


Frå dette søylediagrammet kan me henta meir spesifikk informasjon. Til dømes ser me at auken som skjer i helga hovudsakleg kjem av sykkelturar som startar på morgon og ettermiddag.

**Oppsummering.** I denne seksjonen har me sett korleis me kan bruka søylediagram til å samanlikna ulike grupper i dataa. Me gjer følgjande tre steg for å oppnå dette:

1. Me bruker funksjonen `groupby` på tabellen for å oppretta ei gruppering.
2. Me bruker funksjonen `mean` på ein av kolonnane i den grupperte tabellen. Resultatet er ein kolonne som inneheld gjennomsnittet til kvar gruppe.
3. Me bruker `plot(kind='bar')` på kolonnen me fekk i førre steg. Då blir eit søylediagram oppretta, der kvar gruppe får ei søyle.

Etter steig 2 kan det vera aktuelt å gjera nokre mellomsteg:
* Dersom me har gruppert etter to kolonnar, bør me konvertera resultatet til ein tabell med funksjonen `unstack`.
* Me kan endra rekkjefølgja på gruppene slik at søylediagrammet blir meir oversiktleg.

**Aktivitetsforslag 1.** Grupper turtabellen etter vekedag og periode på dagen, og lag eit søylediagram som viser gjennomsnittleg avstand mellom start -og sluttstasjon.

**Aktivitetsforslag 2.**

Førebuing:

1. Vel deg eit punkt i Oslo, og opprett ein kolonne i turtabellen som fortel kvar nær turane enda dette punktet (sjå seksjonen *Tabellfunksjoner* for hjelp).
2. Del inn turtabellen i grupper etter eige ønske (til dømes vekedag eller periode på dagen).

Oppgåver:

1. Kor nærme endar sykkelturane i gjennomsnitt ditt valde punkt?
2. Kva gruppe av sykkelturar endar i gjennomsnitt nærast og lengst unna ditt valde punkt?
3. Samanlikn dei ulike gruppene ved å laga eit søylediagram.
4. Kva trur du forskjellen mellom gruppene kjem av?

