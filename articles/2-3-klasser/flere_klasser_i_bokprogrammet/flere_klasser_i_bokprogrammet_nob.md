---
title: "Flere klasser i bokprogrammet"
belongs_to_chain: "Hva er en klasse?"
figures_to_include:
	- "modell_boksamling.svg"
	- "klasse_bokhylle.svg"
	- "klasse_alle.svg"
---

I planleggingen av bokprogrammet kom vi fram til følgende modell av objektene: 

<img src="/media/markdowncontent/assosiated_files/modell_boksamling.svg" width="500">

Hvilke klasser kommer disse objektene fra? For eksempel har vi to bokhylleobjekter, og i forrige kapittel kom vi fram til relevante datafelter og handlinger for bokhyller. Dette kan vi bruke til å lage en klasse: 

<img src="/media/markdowncontent/assosiated_files/klasse_bokhylle.svg" width="120">

Legg merke til at disse handlingene må ha en parameter, fordi vi må vite hvilken bok som skal legges til eller fjernes. 

Vi fortsetter å definere klassene for de andre objektene, og tegner dem i et felles diagram: 

<img src="/media/markdowncontent/assosiated_files/klasse_alle.svg" width="800">

Nå kan vi opprette objekter fra fem forskjellige klasser. Den øverste figuren viser at vi bare trenger å opprette ett `Boksamling`-objekt, mens fra de andre klassene kommer vi til å opprette flere objekter. Et bokobjekt kalles også en *instans* av `Bok`-klassen. Altså kommer vi til å opprette mange instanser av klassen `Bok`. 

