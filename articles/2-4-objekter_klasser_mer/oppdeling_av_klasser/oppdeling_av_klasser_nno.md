---
title: "Oppdeling av klassar"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok_oppdeling1.svg"
	- "objektdiagram_bok_oppdeling1.svg"
	- "objektdiagram_bok_oppdeling2.svg"
	- "klasse_bok_oppdeling2.svg"
	- "uml_komposisjon.svg"
	- "bokanmeldelser.svg"
---

Me har tidlegare sett at ein metode berre bør ha éi oppgåve, og at me kan oppnå dette ved å dela opp metodar. Det finst ein tilsvarande regel for klassar. Ein klasse kan sjølvsagt ikkje berre ha éi oppgåve, men ho bør berre ha **eitt ansvar**. Det betyr at `Bok`-klassen berre skal ha ansvar for datafelt og metodar som har å gjera med ei bok. La oss sjå på følgjande klassediagram:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_oppdeling1.svg" width="250">

Her har me markert nokre av  datafelta og metodane i grøn skrift. Kva har desse til felles? Det er ikkje feil å seia at dei har å gjera med ei bok, men kan me vera endå meir spesifikke? Ja, me kan seia at dei har å gjera med *meldingar av ei bok*. `Bok`-klassen har altså to ansvar - både for sjølve boka, og for meldingar av boka.

Me kan også sjå dette i eit spesifikt `Bok`-objekt:

<img src="/media/markdowncontent/assosiated_files/objektdiagram_bok_oppdeling1.svg" width="300">

Me har igjen markert datafelta som har med meldingar å gjera. Me kan trekkja desse ut av `Bok`-objektet og leggja dei i eitt nytt objekt:

<img src="/media/markdowncontent/assosiated_files/objektdiagram_bok_oppdeling2.svg" width="800">

Det nye objektet har ansvar for meldingar av boka *Sofies verd*, medan det opphavlege objektet har ansvar for meir generelle aspekt ved boka. Alt i bokobjektet som var relatert til meldingar har no har vorte redusert til ein peikar til det nye objektet!

Du har kanskje merka at det nye objektet har fått datatypen `Bokanmeldelser`? Objektet kjem altså frå ein klasse me ikkje har definert endå. Me definerer den nye klassen ved å ta utgangspunkt i `Bok`-klassen, og trekkja ut alt som har med meldingar å gjera:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_oppdeling2.svg" width="800">

No ser me at `Bok`-klassen berre har ansvar for ting som handlar om sjølve boka (grunnleggjande informasjon om boka og handtering av utlån). Me har ikkje mista noko funksjonalitet knytt til meldingar av boka, men delegert ansvaret til ein ny klasse!

Me kan visa relasjonen mellom dei to klassane på følgjande måte:

<img src="/media/markdowncontent/assosiated_files/uml_komposisjon.svg" width="500">

Me les dette klassediagrammet på følgjande måte:

* Eitt `Bok`-objekt har null eller eitt  `Bokanmeldelser`-objekt.

Det er viktig å presisera at `Bok`-objekt ikkje treng å ha eitt `Bokanmeldelser`-objekt. `Bok`-klassen fungerer heilt fint på eiga hand, men har moglegheit for utvida funksjonalitet med `Bokanmeldelser`. Og når me ønskjer å registrera bokmeldingar for to utgåver av den same boka, treng me no berre å gjera det éin gong:
<img src="/media/markdowncontent/assosiated_files/bokanmeldelser.svg" width="500">

For å samanfatta, så har me delt opp `Bok`-klassen fordi me ønskjer at han berre skal ha ansvar for sjølve boka. Ansvaret for meldingar av boka har me delegert til ein ny klasse. Å følgja prinsippet om eitt ansvar per klasse har dei same fordelane som prinsippet om éi oppgåve per metode, nemleg at det blir lettare å modifisera og utvida programmet.

- Eigenskapar og metodar blir sorterte over fleire klassar på ein naturleg måte. Koden blir dermed betre strukturert og lettare å lesa.
- Når me seinare vil endra noko som har med innhenting og prosessering av meldingar, kan me jobba med ein klasse som berre har dette ansvaret, utan å bli forstyrra av alt anna som har å gjera med bøker.
- Me kan gjenbruka den nye klassen `Bokanmeldelser` i andre program. Viss me til dømes skal laga ei nettside som rangerer bøker, så ønskjer me kanskje ikkje å bruka `Bok`-klassen (me treng ikkje eit system for utlån av bøker), men det er veldig aktuelt å gjenbruka måten me handterer bokmeldingar.

Som ein ekstra fordel såg me at oppdeling av klassar kan redusera duplikasjoner av data. To utgåver av ei bok vil ha dei same meldingane, og oppdeling sørgjer for at me berre treng å registrera meldingane éin gong.

