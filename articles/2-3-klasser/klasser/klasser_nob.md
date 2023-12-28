---
title: "Klasser"
belongs_to_chain: "Hva er en klasse?"
figures_to_include:
	- "oppskrift.svg"
	- "klasse.svg"
	- "objekter_fra_klasse.svg"
	- "objekter_metodekall.svg"
	- "klasser_med_navn.svg"
---

Vi fokuserer nå på malene for bøker og personer: 

<img src="/media/markdowncontent/assosiated_files/oppskrift.svg" width="300">

Når vi bruker malene får vi altså objekter med visse datafelter. Men som nevnt i forrige kapittel skal objektene ikke bare ha datafelter, men også handlinger. For eksempel skal bøker kunne lånes ut og leveres inn. Derfor legger vi til handlinger i malene: 

<img src="/media/markdowncontent/assosiated_files/klasse.svg" width="300">

Her skriver vi handlingene som funksjoner, for å vise at det nettopp er funksjoner vi skal programmere. Mer om det senere - nå skal vi se hva som skjer når vi oppretter objekter fra malene: 

<img src="/media/markdowncontent/assosiated_files/objekter_fra_klasse.svg" width="700">

Hvert objekt får altså handlingene fra malen. Dette er for å vise at når vi skal utføre en handling, må vi først "gå inn" på et spesifikt objekt, og deretter utføre handlingen på det objektet. Å gjøre handlingen `lån_ut()` på det første bokobjektet (*Sofies verden*) kan gi et annet resultat enn på det andre bokobjektet (*Beatles*). Her kan du se hvordan handlinger kan ha ulikt resultat på ulike objekter: 

<img src="/media/markdowncontent/assosiated_files/objekter_metodekall.svg" width="700">

Nå som malene både inneholder datafelter og handlinger, kan vi si at de er klasser! En *klasse* er nemlig akkurat det - en mal på objekter av samme type, der vi tar med både datafelter og handlinger. Vi skal senere se hvordan man programmerer en klasse, men vi bør alltid skissere klassene i et diagram først. I et slikt diagram må hver klasse også ha et navn med stor forbokstav: 

<img src="/media/markdowncontent/assosiated_files/klasser_med_navn.svg" width="300">

Vi har altså en `Bok`-klasse og en `Person`-klasse, og fra disse kan vi opprette `Bok`-objekter og `Person`-objekter. 

Diagrammet ovenfor kalles et *klassediagram*. Mer spesifikt har vi laget en enkel versjon av et *UML-klassediagram*. UML betyr *Unified Modeling Language* og gir regler for hvordan vi skal tegne, slik at alle kan forstå hverandres diagrammer. Man trenger ikke å pugge disse reglene, men lære gjennom eksempler. Ved å følge eksempelet over kan du allerede tegne enkle UML-klassediagrammer, og senere skal vi vise hvordan man legger til mer informasjon.

