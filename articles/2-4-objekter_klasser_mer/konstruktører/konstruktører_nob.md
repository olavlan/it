---
title: "Konstruktører"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "konstruktor0.svg"
	- "konstruktor1.svg"
	- "konstruktor2.svg"
	- "konstruktor3.svg"
---

Når vi sier at vi "oppretter objekter fra en klasse", kan vi se for oss følgende diagram:

<img src="/media/markdowncontent/assosiated_files/konstruktor0.svg" width="300">

Men hvordan oppretter vi egentlig objekter når vi skriver kode? Svaret er at  alle klasser må ha en spesiell metode for å opprette objekter, som kalles en *konstruktør* (fordi den "konstruerer" objekter). 

Hvordan legger vi til en konstruktør i klassen? Vi definerer en metode med samme navn som klassen, og med noen ønskede parametre. En konstruktør for `Bok`-klassen kan derfor være `Bok(tittel, forfatter, antall_sider)`. Følgende figur viser hvordan vi bruker konstruktøren til å opprette objekter: 

<img src="/media/markdowncontent/assosiated_files/konstruktor1.svg" width="600">

En konstruktør uten kode vil bare opprette et tomt objekt. Hvis vi ønsker gjøre operasjoner på det nyopprettede objektet, må vi skrive kode i konstruktøren. I eksempelet over gjør konstruktøren følgende operasjon med det nye objektet: 

* Fyller datafeltene `tittel`, `forfatter` og `antall_sider` med verdiene som ble gitt i parametrene. 

Denne operasjonen skjer altså ikke automatisk - vi må skrive kode som "flytter" parametrene til datafeltene. Å fylle datafeltene med verdier er hovedoppgaven til en konstruktør. Det er tross alt ikke så interessant å opprette masse tomme objekter, for vi ønsker jo at de nye objektene skal representere spesifikke bøker. Det kan godt hende at konstruktøren gjør mer komplekse ting, som i følgende eksempel: 

<img src="/media/markdowncontent/assosiated_files/konstruktor2.svg" width="400">

Her har vi definert en annen konstruktør, med ISBN som parameter (alle utgitte bøker har et unikt nummer kalt ISBN). Vi ser at objektene blir fylt med riktige verdier. Det betyr at konstruktøren gjør følgende operasjoner: 

1. Bruker ISBN-nummeret til å hente informasjon om boka, for eksempel fra en nettdatabase. 
2. Fyller datafeltene `tittel`, `forfatter` og `antall_sider` med verdiene som ble funnet i forrige punkt. 

Igjen bør det nevnes at konstruktørens hovedoppgave er den andre operasjonen. For å følge prinsippet om én oppgave, bør vi derfor delegere det første steget til en annen metode, som for eksempel kan hete`hent_informasjon(isbn)`.

I programmeringsspråket Java kunne vi inkludert begge konstruktørene vi har definert. Klassediagrammet blir da:

<img src="/media/markdowncontent/assosiated_files/konstruktor3.svg" width="200">

Her har vi altså to forskjellige måter å opprette `Bok`-objekter på. Det ser kanskje rart ut å ha to metoder med samme navn, men siden de har forskjellige antall parametre,  regnes de som forskjellige metoder i Java. 

Dette fungerer derimot ikke i Python. Hvis vi definerer to metoder med samme navn, så vil Python regne den siste metoden som den mest oppdaterte versjonen, og den første metoden vil overskrives. Det betyr at vi bare kan ha én konstruktør i Python. Men som vi skal vise i implementasjonsdelen, kan vi sørge for at den ene konstruktøren kan brukes på forskjellige måter, slik at vi likevel oppnår funksjonaliteten som er gitt i klassediagrammet. 

