---
title: "Beskriva algoritmar med flytdiagram"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
	- "algoritmer_flytdiagram1.svg"
	- "algoritmer_flytdiagram2.svg"
	- "algoritmer_flytdiagram3.svg"
	- "algoritmer_flytdiagram.svg"
---

Me har allereie sett på flytdiagram i kapittelet *Konsepter i objektorientert programmering*. No skal me sjå på korleis me kan presentera algoritmar med flytdiagram.

Når me skal teikna eit flytdiagram, plasserer me stega i boksar, og bruker piler til å visa *flyten* mellom stega, altså korleis ein går frå eit steg til det neste. Me kan godt velja om me vil bruka ord, pseudokode eller programkode i boksane.

Korleis kan me omsetja algoritmen *Finn største tal* til eit flytdiagram? Det er ofte lurt å ta utgangspunkt i pseudokoden, fordi me då kan omsetja kvar linje til ein boks. La oss byrja med dei to første linjene:

>**set** $s$ **to** $L[0]$
**set** $i$ **to** $1$

Kvar av desse linjene er ein *operasjon* eller ein *prosess*, og desse skal plasserast i **prosessboksar**. Me teiknar desse som rektangulære boksar:

<img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram1.svg">

I dette tilfellet har me valt å plassera begge operasjonane i éin felles boks, men dei kunne også vore i kvar sin boks.

Den neste linja i pseudokoden er:

>**while** $i$ **smaller than**  $n $

Her må me ha ei forgreining i flytdiagrammet! Dersom $i$ er mindre enn $n$ skal me gå inn i ei løkke, og når $i$ ikkje er mindre enn $n$, skal me gå ut av løkka:

<img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram2.svg">

For å testa om noko er sant har me brukt ein **valboks**, som blir teikna med diamantform. Sidan testen vart gjort av ein **while**-setning, skal det vera to piler som går ut av boksen; den eine pila skal leia til ei løkke og den andre pila skal leia vidare i diagrammet.

Det neste me må gjera er å laga boksane som skal vera inni løkka. Pseudokoden er:

>&emsp;**if** $L[i]$ **greater than** $s$
&emsp;&emsp;**set** $s$ **to** $L[i]$
&emsp;**endif**
&emsp;**set** $i$ **to** $i + 1$

I løkka skal me altså gjera ein ny test, nemleg å sjekka om $L[i]$ er større enn $s$. Igjen teiknar me testen med ein valboks, og ei pil for kvart av utfalla:

<img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram3.svg">

Dersom testen har positivt svar, skal me altså oppdatera variabelen $s$, og deretter gå til det neste steget. Dersom testen har negativt svar, skal me gå rett til det neste steget.

Den siste operasjonen i løkka er å auka iterasjonsvariabelen $i$. Me må alltid hugsa denne operasjonen når me teiknar løkker; som me skal sjå i neste seksjon, gjeld dette også **for**-løkker.

Dei to siste linjene i pseudokoden er:

>**endwhile**
**return** $s$

Dette fortel kva me skal gjera når me kjem ut av **while**-løkka. Den siste linja fortel eigentleg kva som er utdata for algoritmen. Inndata og utdata for ein algoritme blir sett i **databoksar**, som blir teikna med parallellogram. Databoksane er det som står att for å fullføra flytdiagrammet:

>**Algoritme** *Finn største tal*
>
><img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram.svg">

For å utføra algoritmen startar me på boksen *Inndata* og følgjer pilene heilt til me kjem til boksen *Utdata*. I oppgåva nedanfor kan du sjølv gå gjennom flytdiagrammet med nokre tilfeldig genererte lister.

**Aktivitetsforslag 1:** Utfør algoritmen *Finn største tal* på listene som er genererte nedanfor. Du skal utføra algoritmen ved å gå gjennom flytdiagrammet. I kvar valboks må du avgjera grein du skal følgja vidare i diagrammet. Du bør skriva ned kva verdi variablane $i$ og $s$ har til kvar tid.


```python
from random import randint

for i in range(3):
    random_list = [randint(0,10) for i in range(10)]
    print(random_list)
```

    [6, 9, 3, 1, 5, 8, 9, 3, 4, 6]
    [4, 4, 1, 2, 5, 5, 10, 3, 8, 5]
    [8, 7, 1, 9, 3, 5, 7, 4, 7, 3]


**Aktivitetsforslag 2:** Ta utgangspunkt i *Aktivitetsforslag 2* frå seksjonen *Beskrive algoritmar med ord*. Presenter algoritmen med flytdiagram.

