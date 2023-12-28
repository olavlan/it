---
title: "Oppdeling av metodar"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok_vurdering.svg"
	- "klasse_bok_vurdering_delmetoder.svg"
---

Me bør navnsette metodar slik at det er lett å skjønna kva dei gjer. For å registrera at ei bok blir levert inn, er altså `lever_inn()` eit fornuftig val av namn:
* Namnet startar med eit verb som beskriv handlinga.
* Det er unødvendig å bruka namnet`lever_inn_bok()`, fordi metoden er i `Bok`-klassen, så me veit allereie at han berre blir brukte på `Bok`-objekt.

Eit viktig prinsipp er at **ein metode bør berre ha éi oppgåve**. Dette må me tenkja på når me skal leggja til ny funksjonalitet i bokprogrammet vårt. Kanskje det skal vera mogleg å skriva ei melding samtidig som ein leverer ei bok? Då bør me dela opp denne prosessen i to metodar:

- `lever_inn()` for å levera boka.
- `legg_til_anmeldelse(person, tekst)` for å leggja til ei melding av boka.

Det er kanskje freistande å leggja begge handlingane i ein metode, for det er jo berre lånetakaren som skal kunna skriva ei melding av boka? Men dette problemet bør me løysa på ein annan måte, til dømes med eit vilkår (`if`-setning) i den andre metoden. Det viktigaste er alltid å følgja prinsippet om éi oppgåve per metode.

For å sjå på eit meir interessant døme, skal me byrja å tenkja på korleis me kan rangera bøker. Me legg til eit datafelt og metode i klassediagrammet, markert i grønt:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_vurdering.svg" width="300">

Metoden `regn_ut_gjennomsnittsvurdering()` skal gi boka ein poengsum basert på meldingar frå ulike kjelder. Merk at namnet berre inneheld eitt verb, som er eit godt teikn på at me følgjer prinsippet om éi oppgåve. Men kva om metoden treng fleire steg for å komma fram til svaret? Til dømes kan han gjera følgjande steg:

1. Rekna ut gjennomsnittet av vurderingane til lånetakarane.
2. Rekna ut gjennomsnittet av brukarvurderingar på nett, frå sider som [*Bokelskere*](https://bokelskere.no/) og [*Goodreads*](https://www.goodreads.com/).
3. Viss boka er gitt ut etter 2010; rekna ut gjennomsnittet av litteraturmeldingar på nett (nettaviser).
4. Rekna ut eit endeleg gjennomsnitt basert på tala i punkt 1-3.

Metoden`regn_ut_gjennomsnittsvurdering()` skal berre ha éi oppgåve, nemleg å gjera utrekninga i det fjerde punktet. Men dei tre første stega må utførast først, så korleis handterer me denne situasjonen?  Løysinga er å definera nye metodar for dei tre første operasjonane:

1. `regn_ut_gjennomsnitt(anmeldelser)`
2. `hent_brukeranmeldelser_på_nett()`, deretter bruka metoden frå punkt 1 til å finna gjennomsnittet av meldingane me har henta.
3. `hent_litteraturanmeldelser_på_nett()`, deretter bruka metoden frå punkt 1

Me legg til desse metodane i klassediagrammet:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_vurdering_delmetoder.svg" width="300">

Metodane me har lagt til kallast gjerne *delmetodar*, fordi dei utfører delprosessar, og sørgjer for at`regn_ut_gjennomsnittsvurdering()` berre tek seg av sjølve utrekninga. Fordelen med denne oppdelinga er at det blir enklare å modifisera og utvida programmet seinare:

- Koden blir mykje lettare å lesa. Utan delmetodar ville koden til `regn_ut_gjennomsnittsvurdering()` antakeleg vorte svært lang og vanskeleg å få oversikt over. Ved å bruka delmetodar med gode namn, skjønner ein på kort tid kva fire hovudsteg som blir utførte. Lesbar kode er svært viktig dersom me ønskjer å jobba vidare med programmet seinare, og endå viktigare dersom me ønskjer at andre skal kunna utvida eller nytta delar av koden.
- Når me skal gjera ei bestemd endring i eit program, bør det alltid vera lett å finna dei rette kodelinjene! Å ha metodar som gjer fleire ting vil gi mykje hovudverk, fordi det kan bli umogleg å vita kva delar av programmet som må endrast for å oppnå ein bestemd funksjonalitet. Ved å følgja prinsippet om éi oppgåve, veit me alltid kva metode me skal gå til. Tenk deg til dømes at me ønskjer følgjande endringar i bokprogrammet:
	- Me kjem fram til at brukarmeldingar på nett bør telja mest, og ønskjer derfor å endra vektinga av dei ulike kjeldene. Dette er ei endring av utrekninga, og det er `regn_ut_gjennomsnittsvurdering()` som har denne oppgåva.
	- Me ønskjer å inkludera meldingar frå fleire nettsider. Denne oppgåva ligg hos metoden `hent_brukeranmeldelser_på_nett()`.
- Me kan gjenbruka delmetodane til andre formål. Til dømes, å henta ei oppdatert liste med nettmeldingar kan vera nyttig i andre delar av bokprogrammet vårt. Seinare ønskjer me kanskje å presentera meldingane, eller søkja etter stikkord i meldingane for å gi betre boktilrådingar.

