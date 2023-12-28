---
title: "Beskrive algoritmer med flytdiagram"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
	- "algoritmer_flytdiagram1.svg"
	- "algoritmer_flytdiagram2.svg"
	- "algoritmer_flytdiagram3.svg"
	- "algoritmer_flytdiagram.svg"
---

Vi har allerede sett på flytdiagrammer i kapittelet *Konsepter i objektorientert programmering*. Nå skal vi se på hvordan vi kan presentere algoritmer med flytdiagram. 

Når vi skal tegne et flytdiagram, plasserer vi stegene i bokser, og bruker piler til å vise *flyten* mellom stegene, altså hvordan man går fra et steg til det neste. Vi kan godt velge om vi vil bruke ord, pseudokode eller programkode i boksene. 

Hvordan kan vi oversette algoritmen *Finn største tall* til et flytdiagram? Det er ofte lurt å ta utgangspunkt i pseudokoden, fordi vi da kan oversette hver linje til en boks. La oss begynne med de to første linjene: 

>**set** $s$ **to** $L[0]$   
**set** $i$ **to** $1$

Hver av disse linjene er en *operasjon* eller en *prosess*, og disse skal plasseres i **prosessbokser**. Vi tegner disse som rektangulære bokser:

<img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram1.svg">

I dette tilfellet har vi valgt å plassere begge operasjonene i én felles boks, men de kunne også vært i hver sin boks. 

Den neste linjen i pseudokoden er:

>**while** $i$ **smaller than**  $n $

Her må vi ha en forgrening i flytdiagrammet! Dersom $i$ er mindre enn $n$ skal vi gå inn i en løkke, og når $i$ ikke er mindre enn $n$, skal vi gå ut av løkken:

<img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram2.svg">

For å teste om noe er sant har vi brukt en **valgboks**, som tegnes med diamantform. Siden testen ble gjort av en **while**-setning, skal det være to piler som går ut av boksen; den ene pilen skal lede til en løkke og den andre pilen skal lede videre i diagrammet. 

Det neste vi må gjøre er å lage boksene som skal være inni løkka. Pseudokoden er:

>&emsp;**if** $L[i]$ **greater than** $s$   
&emsp;&emsp;**set** $s$ **to** $L[i]$    
&emsp;**endif**   
&emsp;**set** $i$ **to** $i + 1$

I løkka skal vi altså gjøre en ny test, nemlig å sjekke om $L[i]$ er større enn $s$. Igjen tegner vi testen med en valgboks, og en pil for hvert av utfallene:

<img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram3.svg">

Dersom testen har positivt svar, skal vi altså oppdatere variabelen $s$, og deretter gå til det neste steget. Dersom testen har negativt svar, skal vi gå rett til det neste steget. 

Den siste operasjonen i løkka er å øke iterasjonsvariabelen $i$. Vi må alltid huske denne operasjonen når vi tegner løkker; som vi skal se i neste seksjon, gjelder dette også **for**-løkker.

De to siste linjene i pseudokoden er:

>**endwhile**     
**return** $s$ 

Dette forteller hva vi skal gjøre når vi kommer ut av **while**-løkka. Den siste linja forteller egentlig hva som er utdata for algoritmen. Inndata og utdata for en algoritme settes i **databokser**, som tegnes med parallellogrammer. Databoksene er det som gjenstår for å fullføre flytdiagrammet:  

>**Algoritme** *Finn største tall*
>
><img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram.svg">

For å utføre algoritmen starter vi på boksen *Inndata* og følger pilene helt til vi kommer til boksen *Utdata*. I oppgaven nedenfor kan du selv gå gjennom flytdiagrammet med noen tilfeldig genererte lister.

**Aktivitetsforslag 1:** Utfør algoritmen *Finn største tall* på listene som er generert nedenfor. Du skal utføre algoritmen ved å gå gjennom flytdiagrammet. I hver valgboks må du avgjøre gren du skal følge videre i diagrammet. Du bør skrive ned hvilken verdi variablene $i$ og $s$ har til enhver tid. 


```python
from random import randint

for i in range(3):
    random_list = [randint(0,10) for i in range(10)]
    print(random_list)
```

    [6, 9, 3, 1, 5, 8, 9, 3, 4, 6]
    [4, 4, 1, 2, 5, 5, 10, 3, 8, 5]
    [8, 7, 1, 9, 3, 5, 7, 4, 7, 3]


**Aktivitetsforslag 2:** Ta utgangspunkt i *Aktivitetsforslag 2* fra seksjonen *Beskrive algoritmer med ord*. Presenter algoritmen med flytdiagram.  

