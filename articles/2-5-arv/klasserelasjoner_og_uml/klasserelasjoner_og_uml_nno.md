---
title: "Klasserelasjonar og UML"
belongs_to_chain: "Arv"
figures_to_include:
	- "komposisjon_prosess.svg"
	- "superklasse_prosess2.svg"
	- "komposisjon2.svg"
	- "klasserelasjoner.svg"
---

Me har sett at det kan vera aktuelt å trekkja ut nokre av datafelta og metodane frå ein klasse, og plassera dei i ein ny klasse. Me har sett to måtar å gjera dette på:

**1.**

<img src="/media/markdowncontent/assosiated_files/komposisjon_prosess.svg" width="800">

**2.**

<img src="/media/markdowncontent/assosiated_files/superklasse_prosess2.svg" width="1000">

1. I førre kapittel trekte me ut datafelt og metodar som har eit meir spesifikt ansvar enn for ei bok, nemleg for meldingar av ei bok. Me fekk ein "har"-relasjon mellom den opphavlege klassen og den nye klassen - ei bok har bokmeldingar.
2. I dette kapittelet trekte me ut datafelt og metodar som to klassar har til felles. Me fekk ein "arvar frå"-relasjon mellom dei opphavlege klassane og den nye klassen - bøker og filmar arvar frå utlånsobjekt. Det betyr at bøker og filmar *er* utlånsobjekt, med nokre ekstra datafelt og metodar.


Figurane ovanfor viser at når me deler opp klassar, så endar me opp med relaterte klassar. Kva med klassane me hadde frå starten av? Kan me finna relasjonar mellom dei? Er til dømes `Bokhylle` og`Bok` relaterte? Viss ja, er det ein "har"-relasjon eller ein "arvar frå"-relasjon? Me kan ikkje seia at ei bok er ei bokhylle (eller motsett), så det er ikkje ein "arvar frå"-relasjon!  Men me kan seia at ei bokhylle har bøker! Me kan altså leggja til ein "har"-relasjon mellom desse klassane:

<img src="/media/markdowncontent/assosiated_files/komposisjon2.svg" width="400">

Måten me les dette diagrammet på er:

- Eitt `Bokhylle`-objekt har null eller fleire `Bok`-objekt.

Me kan no teikna eit klassediagram der me tek med alle relasjonane me har funne:

<img src="/media/markdowncontent/assosiated_files/klasserelasjoner.svg" width="700">

Her har me ikkje skrive "har" og "arvar frå", sidan denne informasjonen allereie finst i diagrammet:

1. Diamantform betyr "har"-relasjon.
	- Diamantform utan fyll er ein svak "har"-relasjon.  Ei bok kan eksistera utan å vera i ei bokhylle, så denne "har"-relasjonen er svak.
	- Diamantform med fyll er ein sterk "har"-relasjon.  Bokmeldingar eksisterer berre som ein del av ei bok, så denne "har"-relasjonen er sterk.
2. Pil utan fyll betyr "arvar frå"-relasjon.

Det kan vera ei god øving å komma tilbake til klassediagrammet over, og gjenta følgjande konsept:

* Relasjonar mellom klassar
	* "Har"-relasjon
	* "Arvar frå"-relasjon
* Tegne UML-klassediagram
	- Leggja til konstruktørar
	- Angi datatypar på datafelt, parametrar og returverdiar
	- Angi om metodar skal vera private eller offentlege
	- Angi relasjonar mellom klassar

I klassediagrammet ovanfor døma til vise på alle desse punkta.

