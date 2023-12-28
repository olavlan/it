---
title: "Datatypar"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok.svg"
	- "klasse_bok_utlaan.svg"
	- "klasse_bok_utlaanshistorikk.svg"
	- "klasse_bok_utlaanshistorikk2.svg"
	- "klasse_bok_datatyper.svg"
---

Når me skriv tekststrengen `"Sofies verden"` i Python, så blir eit objekt oppretta frå klassen `str`, som er ein innebygd klasse i Python. Denne klassen har derfor datafelt og metodar, akkurat som klassane me lagar sjølv.

*Me kan til dømes be objektet `"Sofies verden"` om å utføra metoden `capitalize()` for å endra tekststrengen til `"SOFIES VERDEN"`. Viss du er interessert i kva for nokre andre metodar `str`-klassen har, kan du sjå [her](https://docs.python.org/3/library/stdtypes.html#string-methods)*.

Tilsvarande, når me skriv talet `512` i Python, så blir eit objekt oppretta frå klassen `int`.

I Python seier me at *datatypen* til eit objekt er det same som klassen det er laga frå. Me seier derfor at:

* `"Sofies verden"`er eit objekt av datatypen `str`.
* `512`er eit objekt av datatypen `int`.
* `Bok("Sofies verden")` er eit objekt av datatypen `Bok`.

I klassediagrammet kan me skriva kva datatypar dei ulike datafelta skal ha:

<img src="/media/markdowncontent/assosiated_files/klasse_bok.svg" width="120"> 

Datafelta  må sjølvsagt ikkje ha datatypen `str` eller `int` - me kan bruka våre eigne datatypar! Til dømes bør eit `Bok`-objekt ha informasjon om lånestatus. Me kan gjera dette ved å leggja til datafeltet `aktivt_utlån`:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_utlaan.svg" width="120">

Her bruker me datatypen `Utlån`.  Det betyr at datafeltet `aktivt_utlån` skal halda på eit `Utlån`-objekt, der me finn informasjon om utlånet, slik som lånetakar, startdato og leveringsfrist.

I tillegg ønskjer me kanskje å lagra lånehistorikken til ei bok. Då kan me leggja til eit datafelt som heiter `lånehistorikk`:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_utlaanshistorikk.svg" width="120">

Kva datatype skal dette datafeltet ha? Det me ønskjer er å ta vare på alle `Utlån`-objekt som har vorte oppretta for boka. Desse kan lagrast i ei liste! I Python har du kanskje laget listar av tal eller tekststrenger, som til dømes:

`["Per Hansen", "Hilde Bakken", "Siv Larsen" ]`
`[70, 63, 47]`

Kva er datatypen til desse listene? Når me opprettar ei liste i `Python`, bruker me den innebygde klassen `list`. Derfor kan me seia at `[70, 63, 47]` er eit objekt av datatypen `list`! Viss me vil presisera at lista inneheld `int`-objekt, kan me seia at datatypen er `list[int]`. Her er eit døme på eit objekt av typen `list[Bok]`:

`[Bok("Beatles"), Bok("Når villdyret våkner")]`

Vi ønsket at datafeltet `lånehistorikk` skulle lagra tidlegare utlån. No veit me kva datatype me treng, nemleg `list[Utlån]`! Me kan leggja til dette i klassediagrammet:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_utlaanshistorikk2.svg" width="120">

Me kan også visa datatypen til parametrar og returverdiar:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_datatyper.svg" width="150">

Her definerer me at parameteren `person` skal ha datatypen `Person`, og at returverdien skal ha datatypen  `bool`. Altså er returverdien anten-eller `True`  `False` (dette kan fortelja om utlånet/innleveringa vart godkjend eller ikkje).

