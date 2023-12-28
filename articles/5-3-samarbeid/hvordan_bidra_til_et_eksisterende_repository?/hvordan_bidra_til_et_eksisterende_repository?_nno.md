---
title: "Korleis bidra til eit eksisterande repository?"
belongs_to_chain: "Samarbeid med Github"
figures_to_include:
---

Tenk deg at du har lyst til å bidra med kode i eit eksisterande repository, altså eit *Github*-prosjekt. Korleis går du fram? Det er nokon steig me alltid bør følgja:

1. Fork
2. Clone
3. Branch
4. Gjera endringar
5. Commit og push
6. Pull request

Her er det to funksjonar me endå ikkje har sett:

* *Fork* er ein funksjon i *Github* for å kopiera innhaldet i eit eksisterande *Github*-repository, og leggja det i vårt eige *Github*-repository.
* *Clone* er ein funksjon i *git* for å kopiera eit *Github*-repository til maskina vår, slik at me får eit lokalt repository. Dette blir kalla å *klona* eit *Github*-repository.

Det er ein viktig regel me bør følgja:

* Dersom me skal foreslå ei forbetring i eit repository som ikkje er vårt, så bør me ikkje klona det direkte til maskina vår. Først bør me oppretta ein fork, altså ein kopi til vår eigen *Github*-bruker. Deretter bør me klona denne kopien til maskina vår. Derfor er dei to første stega *fork* og *clone*.

Dei fire siste stega er kjende frå førre seksjon, med éin viktig forskjell. Denne gongen skal me nemleg ikkje oppretta ein pull request på vårt eige repository, men på det originale *Github*-prosjektet. Då sender me eit forslag til eigaren av det originale programmet, og pullen vår request kan gå gjennom fleire prosessar, avhengig av korleis bidrag blir handtert i det aktuelle prosjektet. Dei vanlegaste stega er:

* Code review
* Automatiske testar
* Merge

**Code review.**  Du kan be om at andre bidragsytarar i prosjektet ser gjennom forslaga dine. Det er mellom anna nyttig å få tilbakemeldingar av personar med inngåande kjennskap til programmet, for å sjekka forslaget ditt passar saman med resten av koden. I tillegg blir oppdaga feil lettare når nye auge går gjennom koden.

Ein person som gjennomfører ein code review kan leggja inn kommentarar på spesifikke kodelinjer. I kommentarane kan ein påpeika moglege feil, foreslå endringar eller be om oppklaringar. Personen som oppretta ein pull request kan deretter svara på tilbakemeldingane, og gjera ytterlegare endringar av koden om nødvendig. Etter nokon rundar med slik kommunikasjon, kan forslaget godkjennast av personen som gjer code review.

**Testar.** Dei fleste store prosjekt har definert automatiske testar som blir gjennomførte når ein pull request blir lagd inn. Dei viktigaste testane sjekkar at programmet ikkje gir feilmeldingar og produserer dei forventa resultata. Testane kan sjekka individuelle funksjonar, men også at endringane er riktig integrerte i resten av programmet.

Det er viktig at testane dekkjer den nye koden som blir foreslått i ein pull request. Dersom koden til dømes inneheld nye funksjonar, kan ein bli bede om å inkludera testdata, det vil seia ei liste med inndata og forventa utdata. Mange prosjekt køyrer ein *code coverage analysis*, som fortel kor stor del av koden som blir dekt av testane. Jo større deler av koden som blir testa, jo mindre sjanse er det for feil.

Det kan også vera testar som sjekkar at koden følgjer same stil som resten av prosjektet. I store prosjekt har det ofte høg prioritet at koden er ryddig, uniform og godt dokumentert.

**Merge.** Når eit forslag blir godkjent av alle som gjorde eit code review, og alle testar er gjennomførte, så er forslaget klart til å smeltast inn i originalprogrammet. Kanskje vil det vera nokre avsluttande kommentarar, diskusjonar og små endringar. Til slutt blir funksjonen brukt *merge* til å smelta endringane inn i programmet. Det må gjerast av ein bidragsytar med dei nødvendige privilega, eller det kan setjast opp ein automatisk prosess der merge skjer når alle code reviews har vorte merka godkjent, og alle testar er bestått.

**Aktivitet 1.** Gå inn på [first-contributions](https://github.com/firstcontributions/first-contributions#first-contributions), som er eit repository der ein kan øva seg på å bidra i *Github*-prosjekt. Følg stega på framsida (dei finst også på [norsk](https://github.com/firstcontributions/first-contributions/blob/main/translations/readme.no.md)). *I denne oppskrifta blir brukt ein annan måte å oppretta ein branch. Du kan velja mellom denne og måten vist i førre seksjon.*

**Aktivitet 2.**

1. Gå saman med ein klassekamerat. Foreslå ei endring i eit repository som er eigd av klassekameraten. Du skal følgja dei same stega som er beskrivne [her](https://github.com/firstcontributions/first-contributions#first-contributions), men bruka klassekameratens repository i staden.

*Denne aktiviteten er ekstra gøy dersom klassekameraten din har eit repository som inneheld kode, og du kan gjera ei lita forbetring, til dømes leggja til ein funksjon eller fiksa ein feil.*

2. Gå inn på den nye pullen din request, og legg til klassekameraten din som *Reviewer* (du finn denne funksjonen øvst til høgre på sida). Klassekameraten din vil no få ein notifikasjon på sin *Github*-bruker, og kan starta gjennomgangen av pullen din request. Få klassekameraten din til å skriva nokre kommentarar på spesifikke kodelinjer, og prøv å svara på desse.

3. Forsøk no å gjera ei endring i koden på pullen din request. Merk at pullen din request er knytt til ditt *Github*-repository som du oppretta i steg 1 (når du laga ein fork). Derfor kan du gjera endringar på vanleg måte, og bruka *add*, *commit* og *push* for å leggja endringane inn på ditt *Github*-repository. Pullen din request vil også oppdaterast når du gjer dette.

4. Be klassekameraten din om å merka sin code review som godkjent. Dette blir gjort  ved å trykkja på knappen *Review changes* (nedst på sidan for pullen din review), deretter kryssa av *Approve* og til slutt klikka *Submit review*. Klassekameraten din kan no leggja endringane dine inn i originalprogrammet, ved å trykkja på knappen *Merge*.

5. Byt roller og gjer stega 1-4 på nytt.

