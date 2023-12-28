---
title: "Datatyper"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok.svg"
	- "klasse_bok_utlaan.svg"
	- "klasse_bok_utlaanshistorikk.svg"
	- "klasse_bok_utlaanshistorikk2.svg"
	- "klasse_bok_datatyper.svg"
---

Når vi skriver tekststrengen `"Sofies verden"` i Python, så opprettes et objekt fra klassen `str`, som er en innebygd klasse i Python. Denne klassen har derfor datafelter og metoder, akkurat som klassene vi lager selv. 

*Vi kan for eksempel be objektet `"Sofies verden"` om å utføre metoden `capitalize()` for å endre tekststrengen til `"SOFIES VERDEN"`. Hvis du er interessert i hvilke andre metoder `str`-klassen har, kan du se [her](https://docs.python.org/3/library/stdtypes.html#string-methods)*. 

Tilsvarende, når vi skriver tallet `512` i Python, så opprettes et objekt fra klassen `int`. 

I Python sier vi at *datatypen* til et objekt er det samme som klassen det er laget fra. Vi sier derfor at: 

* `"Sofies verden"`er et objekt av datatypen `str`.
* `512`er et objekt av datatypen `int`.
* `Bok("Sofies verden")` er et objekt av datatypen `Bok`. 

I klassediagrammet kan vi skrive hvilke datatyper de ulike datafeltene skal ha:

<img src="/media/markdowncontent/assosiated_files/klasse_bok.svg" width="120"> 

Datafeltene  må selvfølgelig ikke ha datatypen `str` eller `int` - vi kan bruke våre egne datatyper! For eksempel bør et `Bok`-objekt ha informasjon om lånestatus. Vi kan gjøre dette ved å legge til datafeltet `aktivt_utlån`: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_utlaan.svg" width="120">

Her bruker vi datatypen `Utlån`.  Det betyr at datafeltet `aktivt_utlån` skal holde på et `Utlån`-objekt, der vi finner informasjon om utlånet, slik som lånetaker, startdato og leveringsfrist. 

I tillegg ønsker vi kanskje å lagre lånehistorikken til en bok. Da kan vi legge til et datafelt som heter `lånehistorikk`: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_utlaanshistorikk.svg" width="120">

Hvilken datatype skal dette datafeltet ha? Det vi ønsker er å ta vare på alle `Utlån`-objekter som har blitt opprettet for boka. Disse kan lagres i en liste! I Python har du kanskje laget lister av tall eller tekststrenger, som for eksempel:

`["Per Hansen", "Hilde Bakken", "Siv Larsen" ]`    
`[70, 63, 47]`

Hva er datatypen til disse listene? Når vi oppretter en liste i `Python`, bruker vi den innebygde klassen `list`. Derfor kan vi si at `[70, 63, 47]` er et objekt av datatypen `list`! Hvis vi vil presisere at listen inneholder `int`-objekter, kan vi si at datatypen er `list[int]`. Her er et eksempel på et objekt av typen `list[Bok]`: 

`[Bok("Beatles"), Bok("Når villdyret våkner")]`

Vi ønsket at datafeltet `lånehistorikk` skulle lagre tidligere utlån. Nå vet vi hvilken datatype vi trenger, nemlig `list[Utlån]`! Vi kan legge til dette i klassediagrammet:  

<img src="/media/markdowncontent/assosiated_files/klasse_bok_utlaanshistorikk2.svg" width="120">

Vi kan også vise datatypen til parametre og returverdier: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_datatyper.svg" width="150">

Her definerer vi at parameteren `person` skal ha datatypen `Person`, og at returverdien skal ha datatypen  `bool`. Altså er returverdien enten `True` eller `False` (dette kan fortelle om utlånet/innleveringen ble godkjent eller ikke). 

