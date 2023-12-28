---
title: "Fleire klassar i bokprogrammet"
belongs_to_chain: "Hva er en klasse?"
figures_to_include:
	- "modell_boksamling.svg"
	- "klasse_bokhylle.svg"
	- "klasse_alle.svg"
---

I planlegginga av bokprogrammet kom me fram til følgjande modell av objekta:

<img src="/media/markdowncontent/assosiated_files/modell_boksamling.svg" width="500">

Kva klassar kjem desse objekta frå? Til dømes har me to bokhylleobjekt, og i førre kapittel kom me fram til relevante datafelt og handlingar for bokhyller. Dette kan me bruka til å laga ein klasse:

<img src="/media/markdowncontent/assosiated_files/klasse_bokhylle.svg" width="120">

Legg merke til at desse handlingane må ha ein parameter, fordi me må vita kva bok som skal leggjast til eller blir fjerna.

Me held fram med å definera klassane for dei andre objekta, og teiknar dei i eit felles diagram:

<img src="/media/markdowncontent/assosiated_files/klasse_alle.svg" width="800">

No kan me oppretta objekt frå fem ulike klassar. Den øvste figuren viser at me berre treng å oppretta eitt `Boksamling`-objekt, medan frå dei andre klassane kjem me til å oppretta fleire objekt. Eit bokobjekt blir også kalla ein *instans* av `Bok`-klassen. Altså kjem me til å oppretta mange instansar av klassen `Bok`.

