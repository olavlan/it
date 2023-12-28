---
title: "Kommunikasjon mellom objekt"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok_objektkommunikasjon1.svg"
	- "klasse_bok_privat.svg"
	- "klasse_bok_privat_offentlig.svg"
	- "klasse_bok_offentlig.svg"
	- "grensesnitt.svg"
---

Objekt kan senda meldingar til kvarandre. Det vil seia at eit objekt kan be eit anna objekt om å utføra ein av metodane sine, og få svar tilbake. Meldingar mellom objekt er viktig for å fullføra planen om å rangera bøker i bokprogrammet vårt. Me skal no definera metoden som rangerer bøker. I kva klasse bør metoden vera? Sidan me gjer noko med alle bøkene, altså heile boksamlinga, bør me leggja metoden i `Boksamling`-klassen.

Me tek no utgangspunkt i følgjande klassediagram, der relevante datafelt og metodar er skrivne i grønt:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_objektkommunikasjon1.svg" width="400">

Det er altså metoden`vis_rangert_liste()` som skal rangera bøkene. Kva steg treng metoden? Først må kvar bok ha ein poengsum, og deretter kan me sortera bøkene etter poeng. Stega er altså:

1. Rekna ut poengsummen til kvar bok i lista `bøker`. Me gjer dette ved å senda meldinga`regn_ut_gjennomsnittsvurdering()` til kvart `Bok`-objekt. Me lagrar tala me får tilbake.
2. Sortera lista `bøker` basert på tala me fann i punkt 1
3. Vise den sorterte lista.

For at dette skal fungera, må `Bok`-objekta tilby metoden `regn_ut_gjennomsnittsvurdering()` til andre objekt. Kva betyr det?  Av metodane som finst i eit`Bok`-objekt, er nokre *offentlege* og andre *private*. Kva er forskjellen?

* Alle objekt kan be om at `Bok`-objektet utfører ein av dei offentlege metodane sine.
* Ingen andre objekt kan be om at `Bok`-objektet utfører ein av dei private metodane sine, ikkje eingong andre `Bok`-objekt. Ein privat metode kan berre brukast som byggjeblokk til andre metodar i det same objektet, altså som ein delmetode.

Me bruker `Bok`-klassen, det vil seia malen på ei bok, til å definera kva metodar som skal vera offentlege og private. La oss sjå korleis me kan setja alle metodar til å vera private:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_privat.svg" width="250">

Me skriv altså eit minusteikn framfor metodenamnet for å visa at han er privat. No skal me gjera nokre av metodane offentlege. Til dømes ønskjer me å tilby metodane for utlån og innlevering til andre objekt. Og for å kunna rangera bøker, må metoden `regn_ut_gjennomsnittsvurdering()` også vera offentleg. For å gjera ein metode offentleg, endrar me minusteiknet til eit plussteikn:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_privat_offentlig.svg" width="250">

No lurer du kanskje på kva som er poenget med private metodar? Kvifor ikkje berre gjera alle metodar offentlege? For å forklara det tek me utgangspunkt i dømet over, der me har eit`Boksamling`-objekt og fleire `Bok`-objekt. Me lèt som me er `Boksamling`-objektet. Me inneheld altså ein metode for å rangera bøker, og me utfører denne handlinga ved å senda meldingar til `Bok`-objekt og få svar tilbake. Me aner ikkje kva prosessar som skjer inni `Bok`-objekta, men me stoler på at dei alltid svarer oss på den måten me forventar.

Me kan godta at nokon `Bok`-objekt ikkje klarer å finna meldingar, men me må alltid få eit svar som me kan tolka. Det kan til dømes fungera på følgjande måte:

* Viss svaret er eit tal mellom 0 og 10, så har `Bok`-objektet funne meldingar og rekna ut ei vurdering.
* Viss svaret er -1, betyr det at `Bok`-objektet ikkje har funne nokon meldingar.
 
Ei slik løysing kan me vera fornøgde med. Same kor dårleg `Bok`-objekta er til å finna meldingar, så blir me i alle fall aldri overraska - me veit kva svar me kan få, og korleis dei skal tolkast. Men viss `Bok`-objekta på eit seinare tidspunkt sluttar å gi svar eller gir eit uventa svar, så har me grunn til å vera skuffa! Då vil heile rangeringsfunksjonen vår slutta å fungera.

Kva kan me læra av dette tankeeksperimentet? Når me tilbyr ein metode til andre objekt, må me forplikta oss til følgjande punkt:

* At me aldri endrar namnet eller parametrane til metoden.
* At metoden gir svar i alle tilfelle, sjølv når han ikkje fungerer slik me ønskjer. Me bør gi ei god skildring av kva dei ulike svara betyr.
* At metoden for all framtid gir eit av dei forventa svara.

Viss me bryt eitt av desse punkta, kan me øydeleggja kommunikasjonen mellom mange objekt! Som ein generell regel bør me starta med å gjera alle metodar private, og først når det oppstår behov for å tilby ein metode, kan me gjera den offentleg. Då må me hugsa å følgja krava lista ovanfor, som kort sagt seier at ein offentleg metode må haldast stabil for all framtid.

*Grensesnittet* til eit objekt er lista av dei offentlege metodane. Altså er grensesnittet til `Bok`-objekt følgjande:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_offentlig.svg" width="250">

For å skjønna kvifor me bruker ordet "grensesnitt", kan me tenkja på objekt som avgrensa område. Inni objektet har me alle dei private metodane, medan langs grensa har me dei offentlege metodane. Det er altså langs grensa objektet tilbyr funksjonaliteten sin til omverda:

<img src="/media/markdowncontent/assosiated_files/grensesnitt.svg" width="1000">

Kommunikasjonen mellom objekt er vist med grøn pil, medan kommunikasjon internt i eit objekt er vist med raude piler. Merk korleis `Bok`-objektet bruker delmetodar til å byggja opp ein offentleg metode, som deretter blir brukt til å rangera bøker i `Boksamling`-objektet.

Dei indre metodane er private, og me kan endra og sletta dei etter behov. Men metodane i grensesnittet må haldast stabilt, slik at kommunikasjonen på tvers av objekt alltid fungerer.

Me avsluttar denne seksjonen med to viktige punkt:

* Her har me snakka om objekt, men me bestemmer grensesnittet når me lagar klassar. Me kan derfor seia at klassen `Bok` har eit grensesnitt, og at alle`Bok`-objekt får dette grensesnittet. Det gir meining, for det ville vore rart om ein metode var offentleg for eit `Bok`-objekt, men privat for eit anna `Bok`-objekt. Det ville gjort det å umogleg å ha ei løkke som går gjennom alle bøker og kallar på metoden.
* Me har fokusert på kva *metodar* som er offentlege og private, men *datafelt* kan også vera offentlege eller private. Men som grunnregel **bør me gjera alle datafelt private**. Kva ville skjedd dersom me hadde gjort eitt datafelt offentleg? Eit objekt med eit offentleg datafelt mistar kontrollen over seg sjølv, fordi alle andre objekt har direkte tilgang til datafeltet, og kan endra verdien til kva som helst. Slik mangel på kontroll kan ha uføreseielege konsekvensar. I staden bruker me metodar som deler verdiar med omverda på ein trygg måte:
	- Me kan oppretta ein metode som gir lesetilgang til eit datafelt. Metoden vil returnera verdien som finst på datafeltet, utan å gi tilgang til sjølve datafeltet. Dette blir kalla ein *getter*-metode (frå engelsk "get value").
	- Me kan oppretta ein metode som gir endringstilgang til eit datafelt. Ein slik metode tek imot ein parametersverdi og sjekkar om denne verdien kan setjast inn i datafeltet. Dette blir kalla ein *setjar*-metode (frå engelsk "set value"). Når eit objekt har ein setjar-metode for eit bestemt datafelt, betyr det at andre objekt kan  senda ein "førespurnad" om å setja ein ny verdi inn i datafeltet. Objektet som får førespurnaden kan velja å godta eller avslå førespurnaden, og har dermed full kontroll over seg sjølv. Slik unngår me alle uvisser.

