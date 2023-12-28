---
title: "Konstruktørar"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "konstruktor0.svg"
	- "konstruktor1.svg"
	- "konstruktor2.svg"
	- "konstruktor3.svg"
---

Når me seier at me "opprettar objekt frå ein klasse", kan me sjå for oss følgjande diagram:

<img src="/media/markdowncontent/assosiated_files/konstruktor0.svg" width="300">

Men korleis opprettar me eigentleg objekt når me skriv kode? Svaret er at  alle klassar må ha ein spesiell metode for å oppretta objekt, som blir kalla ein *konstruktør* (fordi han "konstruerer" objekt).

Korleis legg me til ein konstruktør i klassen? Me definerer ein metode med same namn som klassen, og med nokre ønskte parametrar. Ein konstruktør for `Bok`-klassen kan derfor vera `Bok(tittel, forfatter, antall_sider)`. Følgjande figur viser korleis me bruker konstruktøren til å oppretta objekt:

<img src="/media/markdowncontent/assosiated_files/konstruktor1.svg" width="600">

Ein konstruktør utan kode vil berre oppretta eit tomt objekt. Viss me ønskjer gjera operasjonar på det nyoppretta objektet, må me skriva kode i konstruktøren. I dømet over gjer konstruktøren følgjande operasjon med det nye objektet:

* Fyller datafelta `tittel`, `forfatter` og `antall_sider` med verdiane som vart gitt i parametrane.

Denne operasjonen skjer altså ikkje automatisk - me må skriva kode som "flyttar" parametrane til datafelta. Å fylla datafelta med verdiar er hovudoppgåva til ein konstruktør. Det er trass alt ikkje så interessant å oppretta masse tomme objekt, for me ønskjer jo at dei nye objekta skal representera spesifikke bøker. Det kan godt henda at konstruktøren gjer meir komplekse ting, som i følgjande døme:

<img src="/media/markdowncontent/assosiated_files/konstruktor2.svg" width="400">

Her har me definert ein annan konstruktør, med ISBN som parameter (alle utgitte bøker har eit unikt nummer kalla ISBN). Me ser at objekta blir fylte med rette verdiar. Det betyr at konstruktøren gjer følgjande operasjonar:

1. Brukar ISBN-nummeret til å henta informasjon om boka, til dømes frå ein nettdatabase.
2. Fyller datafelta `tittel`, `forfatter` og `antall_sider` med verdiane som vart funne i førre punkt.

Igjen bør det nemnast at hovudoppgåva til konstruktøren er den andre operasjonen. For å følgja prinsippet om éi oppgåve, bør me derfor delegera det første steget til ein annan metode, som til dømes kan heita`hent_informasjon(isbn)`.

I programmeringsspråket Java kunne me inkludert begge konstruktørane me har definert. Klassediagrammet blir då:

<img src="/media/markdowncontent/assosiated_files/konstruktor3.svg" width="200">

Her har me altså to ulike måtar å oppretta `Bok`-objekt på. Det ser kanskje rart ut å ha to metodar med same namn, men sidan dei har ulike talet på parametrar,  blir dei rekna som ulike metodar i Java.

Dette fungerer derimot ikkje i Python. Viss me definerer to metodar med same namn, så vil Python rekna den siste metoden som den mest oppdaterte versjonen, og den første metoden vil overskrives. Det betyr at me berre kan ha éin konstruktør i Python. Men som me skal visa i implementasjonsdelen, kan me sørgja for at den eine konstruktøren kan brukast på ulike måtar, slik at me likevel oppnår funksjonaliteten som er gitt i klassediagrammet.

