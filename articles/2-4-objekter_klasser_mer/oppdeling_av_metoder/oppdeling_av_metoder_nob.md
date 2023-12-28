---
title: "Oppdeling av metoder"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok_vurdering.svg"
	- "klasse_bok_vurdering_delmetoder.svg"
---

Vi bør navnsette metoder slik at det er lett å skjønne hva de gjør. For å registrere at en bok leveres inn, er altså `lever_inn()` et fornuftig valg av navn:
* Navnet starter med et verb som beskriver handlingen. 
* Det er unødvendig å bruke navnet`lever_inn_bok()`, fordi metoden er i `Bok`-klassen, så vi vet allerede at den bare brukes på `Bok`-objekter.  

Et viktig prinsipp er at **en metode bør kun ha én oppgave**. Dette må vi tenke på når vi skal legge til ny funksjonalitet i bokprogrammet vårt. Kanskje det skal være mulig å skrive en anmeldelse samtidig som man leverer en bok? Da bør vi dele opp denne prosessen i to metoder: 

- `lever_inn()` for å levere boka.
- `legg_til_anmeldelse(person, tekst)` for å legge til en anmeldelse av boka.

Det er kanskje fristende å legge begge handlingene i en metode, for det er jo bare lånetakeren som skal kunne skrive en anmeldelse av boka? Men dette problemet bør vi løse på en annen måte, for eksempel med en betingelse (`if`-setning) i den andre metoden. Det viktigste er alltid å følge prinsippet om én oppgave per metode. 

For å se på et mer interessant eksempel, skal vi begynne å tenke på hvordan vi kan rangere bøker. Vi legger til et datafelt og metode i klassediagrammet, markert i grønt: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_vurdering.svg" width="300">

Metoden `regn_ut_gjennomsnittsvurdering()` skal gi boka en poengsum basert på anmeldelser fra ulike kilder. Merk at navnet bare inneholder ett verb, som er et godt tegn på at vi følger prinsippet om én oppgave. Men hva om metoden trenger flere steg for å komme fram til svaret? For eksempel kan den gjøre følgende steg:

1. Regne ut gjennomsnittet av lånetakernes vurderinger.
2. Regne ut gjennomsnittet av brukervurderinger på nett, fra sider som [*Bokelskere*](https://bokelskere.no/) og [*Goodreads*](https://www.goodreads.com/). 
3. Hvis boken er utgitt etter 2010; regne ut gjennomsnittet av litteraturanmeldelser på nett (nettaviser).
4. Regne ut et endelig gjennomsnitt basert på tallene i punkt 1-3. 

Metoden`regn_ut_gjennomsnittsvurdering()` skal kun ha én oppgave, nemlig å gjøre utregningen i det fjerde punktet. Men de tre første stegene må utføres først, så hvordan håndterer vi denne situasjonen?  Løsningen er å definere nye metoder for de tre første operasjonene:

1. `regn_ut_gjennomsnitt(anmeldelser)`
2. `hent_brukeranmeldelser_på_nett()`, deretter bruke metoden fra punkt 1 til å finne gjennomsnittet av anmeldelsene vi har hentet.
3. `hent_litteraturanmeldelser_på_nett()`, deretter bruke metoden fra punkt 1.

Vi legger til disse metodene i klassediagrammet: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_vurdering_delmetoder.svg" width="300">

Metodene vi har lagt til kalles gjerne *delmetoder*, fordi de utfører delprosesser, og sørger for at`regn_ut_gjennomsnittsvurdering()` kun tar seg av selve utregningen. Fordelen med denne oppdelingen er at det blir enklere å modifisere og utvide programmet senere:

- Koden blir mye lettere å lese. Uten delmetoder ville koden til `regn_ut_gjennomsnittsvurdering()` antagelig blitt svært lang og vanskelig å få oversikt over. Ved å bruke delmetoder med gode navn, skjønner man på kort tid hvilke fire hovedsteg som utføres. Lesbar kode er svært viktig dersom vi ønsker å jobbe videre med programmet senere, og enda viktigere dersom vi ønsker at andre skal kunne utvide eller benytte deler av koden. 
- Når vi skal gjøre en bestemt endring i et program, bør det alltid være lett å finne de riktige kodelinjene! Å ha metoder som gjør flere ting vil gi mye hodepine, fordi det kan bli umulig å vite hvilke deler av programmet som må endres for å oppnå en bestemt funksjonalitet. Ved å følge prinsippet om én oppgave, vet vi alltid hvilken metode vi skal gå til. Tenk deg for eksempel at vi ønsker følgende endringer i bokprogrammet:
	- Vi kommer fram til at brukeranmeldelser på nett bør telle mest, og ønsker derfor å endre vektingen av de ulike kildene. Dette er en endring av utregningen, og det er `regn_ut_gjennomsnittsvurdering()` som har denne oppgaven. 
	- Vi ønsker å inkludere anmeldelser fra flere nettsider. Denne oppgaven ligger hos metoden `hent_brukeranmeldelser_på_nett()`. 
- Vi kan gjenbruke delmetodene til andre formål. For eksempel, å hente en oppdatert liste med nettanmeldelser kan være nyttig i andre deler av bokprogrammet vårt. Senere ønsker vi kanskje å presentere anmeldelsene, eller søke etter stikkord i anmeldelsene for å gi bedre bokanbefalinger. 

