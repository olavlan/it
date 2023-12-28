---
title: "Flytdiagram"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "flytdiagram_bokvurdering.svg"
---

Metoden `regn_ut_gjennomsnittsvurdering()` frå førre seksjon utfører fleire steg for å rekna ut ein gjennomsnittvurdering av ei bok. Me kan visa desse stega i eit *flytdiagram*:

<img src="/media/markdowncontent/assosiated_files/flytdiagram_bokvurdering.svg" width="1000">

Dette ser kanskje komplisert ut, men me treng ikkje å vita mykje for å forstå eit slikt diagram. Me byrjar med å forklara dei ulike blokkene:

1. I den grøne delen finn me gjennomsnittet av vurderingane til lånetakarane.
2. I den blå delen finn me gjennomsnittet av brukarvurderingar på nett.
3. I den lilla delen finn me gjennomsnittet frå litteraturmeldingar på nett.
4. I den raude delen reknar me ut det endelege gjennomsnittet.

Slik fargelegging er ikkje nødvendig, men gjer det lettare å forstå heilskapen. Merk også korleis me kan plassera boksane slik at diagrammet blir meir oversiktleg.

No må me vita kva dei ulike boksane betyr. I vårt døme har me fire typar boksar:

- **Sirkel/ellipse** markerer start og slutt på metoden.
- **Rektangel** er ein operasjon, til dømes ein metode.
- **Parallellogram** er data. I vårt døme kjem desse før og etter metodar, for å visa inndata og utdata til metodane.
- **Diamant** er eit val. Basert på valet blir bestemd vidare rute i flytdiagrammet.
	- I flytdiagrammet vårt har me éin valboks. Merk at den lilla delen av flytdiagrammet berre blir utført viss me svarer "Ja" på valboksen.
	- Me kan velja sjølv kva som skal vera alternativa i ein valboks. Det må ikkje vera "Ja" og "Nei", og det kan vera fleire enn to alternativ.
	
Det finst andre typar boksar, men med desse boksane kan me teikna flytdiagram for dei fleste metodar.

