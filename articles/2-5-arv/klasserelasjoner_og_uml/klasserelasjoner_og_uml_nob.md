---
title: "Klasserelasjoner og UML"
belongs_to_chain: "Arv"
figures_to_include:
	- "komposisjon_prosess.svg"
	- "superklasse_prosess2.svg"
	- "komposisjon2.svg"
	- "klasserelasjoner.svg"
---

Vi har sett at det kan være aktuelt å trekke ut noen av datafeltene og metodene fra en klasse, og plassere dem i en ny klasse. Vi har sett to måter å gjøre dette på:

**1.**

<img src="/media/markdowncontent/assosiated_files/komposisjon_prosess.svg" width="800">

**2.**

<img src="/media/markdowncontent/assosiated_files/superklasse_prosess2.svg" width="1000">

1. I forrige kapittel trakk vi ut datafelter og metoder som har et mer spesifikt ansvar enn for en bok, nemlig for anmeldelser av en bok. Vi fikk en "har"-relasjon mellom den opprinnelige klassen og den nye klassen - en bok har bokanmeldelser. 
2. I dette kapittelet trakk vi ut datafelter og metoder som to klasser har til felles. Vi fikk en "arver fra"-relasjon mellom de opprinnelige klassene og den nye klassen - bøker og filmer arver fra utlånsobjekter. Det betyr at bøker og filmer *er* utlånsobjekter, med noen ekstra datafelter og metoder.


Figurene ovenfor viser at når vi deler opp klasser, så ender vi opp med relaterte klasser. Hva med klassene vi hadde fra starten av? Kan vi finne relasjoner mellom dem? Er for eksempel `Bokhylle` og`Bok` relaterte? Hvis ja, er det en "har"-relasjon eller en "arver fra"-relasjon? Vi kan ikke si at en bok er en bokhylle (eller motsatt), så det er ikke en "arver fra"-relasjon!  Men vi kan si at en bokhylle har bøker! Vi kan altså legge til en "har"-relasjon mellom disse klassene: 

<img src="/media/markdowncontent/assosiated_files/komposisjon2.svg" width="400">

Måten vi leser dette diagrammet på er:

- Ett `Bokhylle`-objekt har null eller flere `Bok`-objekter.

Vi kan nå tegne et klassediagram der vi tar med alle relasjonene vi har funnet: 

<img src="/media/markdowncontent/assosiated_files/klasserelasjoner.svg" width="700">

Her har vi ikke skrevet "har" og "arver fra", siden denne informasjonen allerede finnes i diagrammet:

1. Diamantform betyr "har"-relasjon. 
	- Diamantform uten fyll er en svak "har"-relasjon.  En bok kan eksistere uten å være i en bokhylle, så denne "har"-relasjonen er svak. 
	- Diamantform med fyll er en sterk "har"-relasjon.  Bokanmeldelser eksisterer kun som en del av en bok, så denne "har"-relasjonen er sterk.  
2. Pil uten fyll betyr "arver fra"-relasjon.

Det kan være en god øvelse å komme tilbake til klassediagrammet over, og gjenta følgende konsepter:  

* Relasjoner mellom klasser
	* "Har"-relasjon
	* "Arver fra"-relasjon
* Tegne UML-klassediagram
	- Legge til konstruktører
	- Angi datatyper på datafelter, parametre og returverdier
	- Angi om metoder skal være private eller offentlige
	- Angi relasjoner mellom klasser

I klassediagrammet ovenfor vises eksempler på alle disse punktene.

