---
title: "Superklasser"
belongs_to_chain: "Arv"
figures_to_include:
	- "klasse_utlaansobjekt.svg"
	- "utlaansobjekter.svg"
	- "klasser_arv.svg"
	- "superklasse_prosess.svg"
---

Hvordan kan vi si med én setning hva `Film`-objektet og `Bok`-objektet har til felles? Vi kan si at de begge er utlånsobjekter! Det kan være navnet på basisklassen: 

<img src="/media/markdowncontent/assosiated_files/klasse_utlaansobjekt.svg" width="120">

Nå kan vi opprette `Utlån`-objekter! Hva slags objekter er dette? Enhver ting som vi ønsker å låne ut og som har en tittel! Det kan for eksempel et spill eller en tegneserie:

<img src="/media/markdowncontent/assosiated_files/utlaansobjekter.svg" width="350">

Det er lett å tenke at vi her bør opprette nye klasser, for eksempel med navn "Spill" og "Tegneserie". Men foreløpig ønsker vi ikke å gjøre spesifikke handlinger med spill eller tegneserier. Alt vi ønsker å gjøre er å låne dem ut, og da bør vi betrakte dem som utlånsobjekter! Å være veldig spesifikke er altså noe vi prøver å unngå når vi planlegger et objektorientert program. 

På bøker og filmer ønsker vi derimot å gjøre spesifikke handlinger, som å hente informasjon og anmeldelser på nett. Derfor gir det mening å definere spesifikke klasser for bøker og filmer. Men siden bøker og filmer også er utlånsobjekter, så må vi sørge for at `Bok` og `Film` arver alle datafeltene og metodene til `Utlånsobjekt`. Dette viser vi med følgende piler: 

<img src="/media/markdowncontent/assosiated_files/klasser_arv.svg" width="400">
 
Måten vi leser diagrammet på er følgende: 

- Den første pilen forteller at `Bok` arver datafeltene og metodene i `Utlånsobjekt`. Tilsvarende sier den andre pilen at `Film` også arver datafeltene og metodene i `Utlånsobjekt`.
- Vi sier at`Utlånsobjekt` er *superklassen* til `Bok` og `Film`. 
- Vi sier  at `Bok` og `Film` er *subklassene* til `Utlånsobjekt`.

For å oppsummere, så har vi identifisert felles datafelter og metoder i klassene `Bok` og `Film`, og laget en superklasse som inneholder disse. Følgende figur viser hele prosessen:

<img src="/media/markdowncontent/assosiated_files/superklasse_prosess.svg" width="1000">

Det er flere fordeler med å definere superklasser: 

- Vi unngår å repetere de samme metodene i flere klasser. I stedet definerer vi disse ett sted, nemlig i superklassen. Det betyr at vi også unngår duplisering av kode, og det blir lettere å gjøre endringer. Hvis vi for eksempel vil endre måten utlån registreres på, trenger vi kun å endre koden ett sted, nemlig i klassen `Utlånsobjekt`. 
- Vi kan gjenbruke superklassen til andre formål. For eksempel, dersom vi senere ønsker et utlånssystem for helt andre ting enn bøker og filmer, så kan vi gjenbruke klassen `Utlånsobjekt`. 

