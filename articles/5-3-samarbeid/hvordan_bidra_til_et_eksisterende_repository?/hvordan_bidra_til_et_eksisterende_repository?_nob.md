---
title: "Hvordan bidra til et eksisterende repository?"
belongs_to_chain: "Samarbeid med Github"
figures_to_include:
---

Tenk deg at du har lyst til å bidra med kode i et eksisterende repository, altså et *Github*-prosjekt. Hvordan går du fram? Det er noen steg vi alltid bør følge: 

1. Fork
2. Clone
3. Branch
4. Gjøre endringer
5. Commit og push
6. Pull request

Her er det to funksjoner vi enda ikke har sett: 

* *Fork* er en funksjon i *Github* for å kopiere innholdet i et eksisterende *Github*-repository, og legge det i vårt eget *Github*-repository.
* *Clone* er en funksjon i *git* for å kopiere et *Github*-repository til vår maskin, slik at vi får et lokalt repository. Dette kalles å *klone* et *Github*-repository.

Det er en viktig regel vi bør følge:

* Dersom vi skal foreslå en forbedring i et repository som ikke er vårt, så bør vi ikke klone det direkte til maskinen vår. Først bør vi opprette en fork, altså en kopi til vår egen *Github*-bruker. Deretter bør vi klone denne kopien til maskinen vår. Derfor er de to første stegene *fork* og *clone*.

De fire siste stegene er kjent fra forrige seksjon, med én viktig forskjell. Denne gangen skal vi nemlig ikke opprette en pull request på vårt eget repository, men på det originale *Github*-prosjektet. Da sender vi et forslag til eieren av det originale programmet, og vår pull request vil kunne gå gjennom flere prosesser, avhengig av hvordan bidrag håndteres i det aktuelle prosjektet. De vanligste stegene er: 

* Code review
* Automatiske tester
* Merge

**Code review.**  Du kan be om at andre bidragsytere i prosjektet ser gjennom forslagene dine. Det er blant annet nyttig å få tilbakemeldinger av personer med inngående kjennskap til programmet, for å sjekke forslaget ditt passer sammen med resten av koden. I tillegg oppdages feil lettere når nye øyne går gjennom koden. 

En person som gjennomfører en code review kan legge inn kommentarer på spesifikke kodelinjer. I kommentarene kan man påpeke mulige feil, foreslå endringer eller be om oppklaringer. Personen som opprettet en pull request kan deretter svare på tilbakemeldingene, og gjøre ytterligere endringer av koden om nødvendig. Etter noen runder med slik kommunikasjon, kan forslaget godkjennes av personen som gjør code review.

**Tester.** De fleste store prosjekter har definert automatiske tester som gjennomføres når en pull request legges inn. De viktigste testene sjekker at programmet ikke gir feilmeldinger og produserer de forventede resultatene. Testene kan sjekke individuelle funksjoner, men også at endringene er riktig integrert i resten av programmet.

Det er viktig at testene dekker den nye koden som foreslås i en pull request. Dersom koden for eksempel inneholder nye funksjoner, kan man bli bedt om å inkludere testdata, det vil si en liste med inndata og forventet utdata. Mange prosjekter kjører en *code coverage analysis*, som forteller hvor stor del av koden som blir dekket av testene. Jo større deler av koden som blir testet, jo mindre sjanse er det for feil.

Det kan også være tester som sjekker at koden følger samme stil som resten av prosjektet. I store prosjekter har det ofte høy prioritet at koden er ryddig, uniform og godt dokumentert.

**Merge.** Når et forslag blir godkjent av alle som gjorde et code review, og alle tester er gjennomført, så er forslaget klart til å smeltes inn i originalprogrammet. Kanskje vil det være noen avsluttende kommentarer, diskusjoner og små endringer. Til slutt brukes funksjonen *merge* til å smelte endringene inn i programmet. Det må gjøres av en bidragsyter med de nødvendige privileger, eller det kan settes opp en automatisk prosess der merge skjer når alle code reviews har blitt merket godkjent, og alle tester er bestått. 

**Aktivitet 1.** Gå inn på [first-contributions](https://github.com/firstcontributions/first-contributions#first-contributions), som er et repository der man kan øve seg på å bidra i *Github*-prosjekter. Følg stegene på forsiden (de finnes også på [norsk](https://github.com/firstcontributions/first-contributions/blob/main/translations/README.no.md)). *I denne oppskriften brukes en annen måte å opprette en branch. Du kan velge mellom denne og måten vist i forrige seksjon.*

**Aktivitet 2.** 

1. Gå sammen med en klassekamerat. Foreslå en endring i et repository som eies av klassekameraten. Du skal følge de samme stegene som er beskrevet [her](https://github.com/firstcontributions/first-contributions#first-contributions), men bruke klassekameratens repository i stedet. 

*Denne aktiviteten er ekstra gøy dersom klassekameraten din har et repository som inneholder kode, og du kan gjøre en liten forbedring, for eksempel legge til en funksjon eller fikse en feil.*

2. Gå inn på din nye pull request, og legg til klassekameraten din som *Reviewer* (du finner denne funksjonen øverst til høyre på siden). Klassekameraten din vil nå få en notifikasjon på sin *Github*-bruker, og kan starte gjennomgangen av din pull request. Få klassekameraten din til å skrive noen kommentarer på spesifikke kodelinjer, og forsøk å svare på disse. 

3. Forsøk nå å gjøre en endring i koden på din pull request. Merk at din pull request er knyttet til ditt *Github*-repository som du opprettet i steg 1 (når du lagde en fork). Derfor kan du gjøre endringer på vanlig måte, og bruke *add*, *commit* og *push* for å legge endringene inn på ditt *Github*-repository. Din pull request vil også oppdateres når du gjør dette.

4. Be klassekameraten din om å merke sin code review som godkjent. Dette gjøres  ved å trykke på knappen *Review changes* (nederst på siden for din pull review), deretter krysse av *Approve* og til slutt klikke *Submit review*. Klassekameraten din kan nå legge endringene dine inn i originalprogrammet, ved å trykke på knappen *Merge*.

5. Bytt roller og gjør stegene 1-4 på nytt.

