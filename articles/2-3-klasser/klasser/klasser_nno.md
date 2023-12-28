---
title: "Klassar"
belongs_to_chain: "Hva er en klasse?"
figures_to_include:
	- "oppskrift.svg"
	- "klasse.svg"
	- "objekter_fra_klasse.svg"
	- "objekter_metodekall.svg"
	- "klasser_med_navn.svg"
---

Me fokuserer no på malane for bøker og personar:

<img src="/media/markdowncontent/assosiated_files/oppskrift.svg" width="300">

Når me bruker malane får me altså objekt med visse datafelt. Men som nemnt i førre kapittel skal objekta ikkje berre ha datafelt, men også handlingar. Til dømes skal bøker kunna lånast ut og leverast inn. Derfor legg me til handlingar i malane:

<img src="/media/markdowncontent/assosiated_files/klasse.svg" width="300">

Her skriv me handlingane som funksjonar, for å visa at det nettopp er funksjonar me skal programmera. Meir om det seinare - no skal me sjå kva som skjer når me opprettar objekt frå malane:

<img src="/media/markdowncontent/assosiated_files/objekter_fra_klasse.svg" width="700">

Kvart objekt får altså handlingane frå malen. Dette er for å visa at når me skal utføra ei handling, må me først "gå inn" på eit spesifikt objekt, og deretter utføra handlinga på det objektet. Å gjera handlinga `lån_ut()` på det første bokobjektet (*Sofies verd*) kan gi eit anna resultat enn på det andre bokobjektet (*Beatles*). Her kan du sjå korleis handlingar kan ha ulikt resultat på ulike objekt:

<img src="/media/markdowncontent/assosiated_files/objekter_metodekall.svg" width="700">

No som malane både inneheld datafelt og handlingar, kan me seia at dei er klassar! Ein *klasse* er nemleg akkurat det - ein mal på objekt av same type, der me tek med både datafelt og handlingar. Me skal seinare sjå korleis ein programmerer ein klasse, men me bør alltid skissera klassane i eit diagram først. I eit slikt diagram må kvar klasse også ha eit namn med stor forbokstav:

<img src="/media/markdowncontent/assosiated_files/klasser_med_navn.svg" width="300">

Me har altså ein `Bok`-klasse og ein `Person`-klasse, og frå desse kan me oppretta `Bok`-objekt og `Person`-objekt.

Diagrammet ovanfor blir eit klassediagram *kalla*. Meir spesifikt har me laga ein enkel versjon av eit *UML-klassediagram*. UML betyr *Unified Modeling Language* og gir reglar for korleis me skal teikna, slik at alle kan forstå diagramma kvarandres. Ein treng ikkje å pugga desse reglane, men lære gjennom døme. Ved å følgja dømet over kan du allereie teikna enkle UML-klassediagram, og seinare skal me vise korleis ein legg til meir informasjon.

