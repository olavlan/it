---
title: "Kommunikasjon mellom objekter"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok_objektkommunikasjon1.svg"
	- "klasse_bok_privat.svg"
	- "klasse_bok_privat_offentlig.svg"
	- "klasse_bok_offentlig.svg"
	- "grensesnitt.svg"
---

Objekter kan sende meldinger til hverandre. Det vil si at et objekt kan be et annet objekt om å utføre en av sine metoder, og få svar tilbake. Meldinger mellom objekter er viktig for å fullføre planen om å rangere bøker i bokprogrammet vårt. Vi skal nå definere metoden som rangerer bøker. I hvilken klasse bør metoden være? Siden vi gjør noe med alle bøkene, altså hele boksamlingen, bør vi legge metoden i `Boksamling`-klassen.

Vi tar nå utgangspunkt i følgende klassediagram, der relevante datafelter og metoder er skrevet i grønt:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_objektkommunikasjon1.svg" width="400">

Det er altså metoden`vis_rangert_liste()` som skal rangere bøkene. Hvilke steg trenger metoden? Først må hver bok ha en poengsum, og deretter kan vi sortere bøkene etter poeng. Stegene er altså:

1. Regne ut poengsummen til hver bok i listen `bøker`. Vi gjør dette ved å sende meldingen`regn_ut_gjennomsnittsvurdering()` til hvert `Bok`-objekt. Vi lagrer tallene vi får tilbake. 
2. Sortere listen `bøker` basert på tallene vi fant i punkt 1. 
3. Vise den sorterte listen. 

For at dette skal fungere, må `Bok`-objektene tilby metoden `regn_ut_gjennomsnittsvurdering()` til andre objekter. Hva betyr det?  Av metodene som finnes i et`Bok`-objekt, er noen *offentlige* og andre *private*. Hva er forskjellen? 

* Alle objekter kan be om at `Bok`-objektet utfører en av sine offentlige metoder.
* Ingen andre objekter kan be om at `Bok`-objektet utfører en av sine private metoder, ikke engang andre `Bok`-objekter. En privat metode kan kun brukes som byggeblokk til andre metoder i det samme objektet, altså som en delmetode. 

Vi bruker `Bok`-klassen, det vil si malen på en bok, til å definere hvilke metoder som skal være offentlige og private. La oss se hvordan vi kan sette alle metoder til å være private: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_privat.svg" width="250">

Vi skriver altså et minustegn foran metodenavnet for å vise at den er privat. Nå skal vi gjøre noen av metodene offentlige. For eksempel ønsker vi å tilby metodene for utlån og innlevering til andre objekter. Og for å kunne rangere bøker, må metoden `regn_ut_gjennomsnittsvurdering()` også være offentlig. For å gjøre en metode offentlig, endrer vi minustegnet til et plusstegn:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_privat_offentlig.svg" width="250">

Nå lurer du kanskje på hva som er poenget med private metoder? Hvorfor ikke bare gjøre alle metoder offentlige? For å forklare det tar vi utgangspunkt i eksempelet over, der vi har et`Boksamling`-objekt og flere `Bok`-objekter. Vi later som vi er `Boksamling`-objektet. Vi inneholder altså en metode for å rangere bøker, og vi utfører denne handlingen ved å sende meldinger til `Bok`-objekter og få svar tilbake. Vi aner ikke hvilke prosesser som skjer inni `Bok`-objektene, men vi stoler på at de alltid svarer oss på den måten vi forventer. 

Vi kan godta at noen `Bok`-objekter ikke klarer å finne anmeldelser, men vi må alltid få et svar som vi kan tolke. Det kan for eksempel fungere på følgende måte: 

* Hvis svaret er et tall mellom 0 og 10, så har `Bok`-objektet funnet anmeldelser og regnet ut en vurdering. 
* Hvis svaret er -1, betyr det at `Bok`-objektet ikke har funnet noen anmeldelser. 
 
En slik løsning kan vi være fornøyde med. Uansett hvor dårlig `Bok`-objektene er til å finne anmeldelser, så blir vi i hvert fall aldri overrasket - vi vet hvilke svar vi kan få, og hvordan de skal tolkes. Men hvis `Bok`-objektene på et senere tidspunkt slutter å gi svar eller gir et uventet svar, så har vi grunn til å være skuffet! Da vil hele rangeringsfunksjonen vår slutte å fungere. 

Hva kan vi lære av dette tankeeksperimentet? Når vi tilbyr en metode til andre objekter, må vi forplikte oss til følgende punkter: 

* At vi aldri endrer navnet eller parameterne til metoden. 
* At metoden gir svar i alle tilfeller, selv når den ikke fungerer slik vi ønsker. Vi bør gi en god beskrivelse av hva de ulike svarene betyr.
* At metoden for all fremtid gir et av de forventede svarene. 

Hvis vi bryter ett av disse punktene, kan vi ødelegge kommunikasjonen mellom mange objekter! Som en generell regel bør vi starte med å gjøre alle metoder private, og først når det oppstår behov for å tilby en metode, kan vi gjøre den offentlig. Da må vi huske å følge kravene listet ovenfor, som kort sagt sier at en offentlig metode må holdes stabil for all fremtid.

*Grensesnittet* til et objekt er listen av de offentlige metodene. Altså er grensesnittet til `Bok`-objekter følgende: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_offentlig.svg" width="250">

For å skjønne hvorfor vi bruker ordet "grensesnitt", kan vi tenke på objekter som avgrensede områder. Inni objektet har vi alle de private metodene, mens langs grensen har vi de offentlige metodene. Det er altså langs grensen objektet tilbyr sin funksjonalitet til omverdenen:

<img src="/media/markdowncontent/assosiated_files/grensesnitt.svg" width="1000">

Kommunikasjonen mellom objekter er vist med grønn pil, mens kommunikasjon innad i et objekt er vist med røde piler. Merk hvordan `Bok`-objektet bruker delmetoder til å bygge opp en offentlig metode, som deretter brukes til å rangere bøker i `Boksamling`-objektet.

De indre metodene er private, og vi kan endre og slette dem etter behov. Men metodene i grensesnittet må holdes stabilt, slik at kommunikasjonen på tvers av objekter alltid fungerer.

Vi avslutter denne seksjonen med to viktige punkter: 

* Her har vi snakket om objekter, men vi bestemmer grensesnittet når vi lager klasser. Vi kan derfor si at klassen `Bok` har et grensesnitt, og at alle`Bok`-objekter får dette grensesnittet. Det gir mening, for det ville vært rart om en metode var offentlig for et `Bok`-objekt, men privat for et annet `Bok`-objekt. Det ville gjort det å umulig å ha en løkke som går gjennom alle bøker og kaller på metoden.
* Vi har fokusert på hvilke *metoder* som er offentlige og private, men *datafelter* kan også være offentlige eller private. Men som grunnregel **bør vi gjøre alle datafelter private**. Hva ville skjedd dersom vi hadde gjort ett datafelt offentlig? Et objekt med et offentlig datafelt mister kontrollen over seg selv, fordi alle andre objekter har direkte tilgang til datafeltet, og kan endre verdien til hva som helst. Slik mangel på kontroll kan ha uforutsigbare konsekvenser. I stedet bruker vi metoder som deler verdier med omverdenen på en trygg måte: 
	- Vi kan opprette en metode som gir lesetilgang til et datafelt. Metoden vil returnere verdien som finnes på datafeltet, uten å gi tilgang til selve datafeltet. Dette kalles en *getter*-metode (fra engelsk "get value").
	- Vi kan opprette en metode som gir endringstilgang til et datafelt. En slik metode tar imot en parameterverdi og sjekker om denne verdien kan settes inn i datafeltet. Dette kalles en *setter*-metode (fra engelsk "set value"). Når et objekt har en setter-metode for et bestemt datafelt, betyr det at andre objekter kan  sende en "forespørsel" om å sette en ny verdi inn i datafeltet. Objektet som mottar forespørselen kan velge å godta eller avslå forespørselen, og har dermed full kontroll over seg selv. Slik unngår vi alle uforutsigbarheter. 

