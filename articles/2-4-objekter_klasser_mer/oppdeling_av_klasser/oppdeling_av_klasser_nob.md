---
title: "Oppdeling av klasser"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok_oppdeling1.svg"
	- "objektdiagram_bok_oppdeling1.svg"
	- "objektdiagram_bok_oppdeling2.svg"
	- "klasse_bok_oppdeling2.svg"
	- "uml_komposisjon.svg"
	- "bokanmeldelser.svg"
---

Vi har tidligere sett at en metode kun bør ha én oppgave, og at vi kan oppnå dette ved å dele opp metoder. Det finnes en tilsvarende regel for klasser. En klasse kan selvfølgelig ikke bare ha én oppgave, men den bør kun ha **ett ansvar**. Det betyr at `Bok`-klassen bare skal ha ansvar for datafelter og metoder som har å gjøre med en bok. La oss se på følgende klassediagram: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_oppdeling1.svg" width="250">

Her har vi markert noen av  datafeltene og metodene i grønn skrift. Hva har disse til felles? Det er ikke feil å si at de har å gjøre med en bok, men kan vi være enda mer spesifikke? Ja, vi kan si at de har å gjøre med *anmeldelser av en bok*. `Bok`-klassen har altså to ansvar - både for selve boka, og for anmeldelser av boka. 

Vi kan også se dette i et spesifikt `Bok`-objekt:

<img src="/media/markdowncontent/assosiated_files/objektdiagram_bok_oppdeling1.svg" width="300">

Vi har igjen markert datafeltene som har med anmeldelser å gjøre. Vi kan trekke disse ut av `Bok`-objektet og legge dem i ett nytt objekt:

<img src="/media/markdowncontent/assosiated_files/objektdiagram_bok_oppdeling2.svg" width="800">

Det nye objektet har ansvar for anmeldelser av boka *Sofies verden*, mens det opprinnelige objektet har ansvar for mer generelle aspekter ved boka. Alt i bokobjektet som var relatert til anmeldelser har nå har blitt redusert til en peker til det nye objektet!

Du har kanskje merket at det nye objektet har fått datatypen `Bokanmeldelser`? Objektet kommer altså fra en klasse vi ikke har definert enda. Vi definerer den nye klassen ved å ta utgangspunkt i `Bok`-klassen, og trekke ut alt som har med anmeldelser å gjøre: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_oppdeling2.svg" width="800">

Nå ser vi at `Bok`-klassen kun har ansvar for ting som handler om selve boka (grunnleggende informasjon om boka og håndtering av utlån). Vi har ikke mistet noe funksjonalitet knyttet til anmeldelser av boka, men delegert ansvaret til en ny klasse!

Vi kan vise relasjonen mellom de to klassene på følgende måte:

<img src="/media/markdowncontent/assosiated_files/uml_komposisjon.svg" width="500">

Vi leser dette klassediagrammet på følgende måte:

* Ett `Bok`-objekt har null eller ett  `Bokanmeldelser`-objekt.

Det er viktig å presisere at `Bok`-objekter ikke trenger å ha ett `Bokanmeldelser`-objekt. `Bok`-klassen fungerer helt fint på egen hånd, men har mulighet for utvidet funksjonalitet med `Bokanmeldelser`. Og når vi ønsker å registrere bokanmeldelser for to utgaver av den samme boken, trenger vi nå bare å gjøre det én gang:
<img src="/media/markdowncontent/assosiated_files/bokanmeldelser.svg" width="500">

For å oppsummere, så har vi delt opp `Bok`-klassen fordi vi ønsker at den kun skal ha ansvar for selve boka. Ansvaret for anmeldelser av boka har vi delegert til en ny klasse. Å følge prinsippet om ett ansvar per klasse har de samme fordelene som prinsippet om én oppgave per metode, nemlig at det blir lettere å modifisere og utvide programmet. 

- Egenskaper og metoder sorteres over flere klasser på en naturlig måte. Koden blir dermed bedre strukturert og lettere å lese. 
- Når vi senere vil endre noe som har med innhenting og prosessering av anmeldelser, kan vi jobbe med en klasse som kun har dette ansvaret, uten å bli forstyrret av alt annet som har å gjøre med bøker.
- Vi kan gjenbruke den nye klassen `Bokanmeldelser` i andre programmer. Hvis vi for eksempel skal lage en nettside som rangerer bøker, så ønsker vi kanskje ikke å bruke `Bok`-klassen (vi trenger ikke et system for utlån av bøker), men det er veldig aktuelt å gjenbruke måten vi håndterer bokanmeldelser. 

Som en ekstra fordel så vi at oppdeling av klasser kan redusere duplikasjoner av data. To utgaver av en bok vil ha de samme anmeldelsene, og oppdeling sørger for at vi bare trenger å registrere anmeldelsene én gang. 

