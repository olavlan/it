---
title: "Oppsummering og aktiviteter"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
---

**Oppsummering**

* I objektorientert programmering brukes ofte begrepet *metode* i stedet for *funksjon*, og *melding* i stedet for *funksjonskall*. Å sende en melding til et objekt er å be objektet om å utføre en av sine metoder. 
* Datatypen til et objekt er det samme som navnet til klassen som objektet kommer fra. 
* Alle objekter ligger fritt i datamaskinens minne, og hvert objekt har en unik minneadresse.  Pekere sørger for at objekter kan finne hverandre.
* Vi bør følge prinsippet om at en metode bare skal ha én oppgave. En metode skal altså bare utføre én handling. Dersom flere steg er nødvendig, bør disse delegeres til delmetoder. 
* Et flytdiagram er en skisse av stegene i en metode. 
* Når et objekt benytter en metode som tilbys av et annet objekt, og får svar tilbake, har vi kommunikasjon mellom objekter. Vi sier også at objektene *samhandler*. Metodene som kan benyttes i objektsamhandling kalles offentlige metoder. Metodene som bare kan brukes innad i et objekt kalles private metoder. 
* Grensesnittet til en klasse er alle de offentlige metodene. De offentlige metodene må holdes stabile, slik at kommunikasjonen mellom objekter ikke ødelegges. For å gjøre dette lettere, bør vi holde grensesnittet så lite som mulig. 
* Hver klasse har minst én metode som brukes til å opprette objekter fra klassen. En slik metode kalles en konstruktør. 
* En klasse bør kun ha ett ansvar. Dersom noen egenskaper og metoder har et mer spesifikt ansvar, kan de trekkes ut og danne en ny klasse. Altså deler vi opp en klasse dersom den har mer enn ett ansvar.

**Prosjektoppgave 4.**

Ta utgangspunkt i *Prosjektoppgave 3* fra forrige kapittel og gjør følgende oppgaver:

1. Skriv opp noen objekter som kommer fra klassene i klassediagrammet ditt (følg eksemplene gitt i seksjonen *Skrivemåte for objekter*). 
2. Gjør klassediagrammet mer detaljert ved å skrive datatyper på alle datafelter og metoder (følg eksemplene gitt i seksjonen *Datatyper*). På metodene skal du skrive datatypen til returverdien.
3. Følg eksemplet i seksjonen *Objektdiagram og pekere* til å tegne objektene fra punkt 1. Sørg for å få med pekere mellom objekter!
4. Tenk over hvilke steg som må utføres for hver av metodene i klassediagrammet. Kan du finne en metode som krever flere steg? Forsøk i så fall å dele opp denne metoden i delmetoder (følg eksemplet gitt i seksjonen *Oppdeling av metoder*).
5. Tegn et flytdiagram for metoden i punkt 4 (følg eksemplet gitt i seksjonen *flytdiagram*).
6. Kan du lage en metode som fungerer ved å sende meldinger til alle objekter? Her er noen eksempler som kan være til hjelp.
    * Tenk at man har klassene `Butikk` og `Vare`, og den sistnevnte har metoden `antall_dager_til_utgått()`. Da kan `Butikk` ha en metode som lister alle varer som utgår om mindre enn én uke.
    * Tenk at man har klassene `Videobibliotek` og `Video`, og den sistnevnte har metoden `komprimer_video()`. Da kan `Videobibliotek` ha en metode som komprimerer alle videoene i biblioteket.
7. Vis hvordan objektene i oppgave 6 kommuniserer ved å følge tegningen i seksjonen *Kommunikasjon mellom objekter*. Hvilken metode må være offentlig for at kommunikasjonen skal være mulig? 
8. Følg eksemplene gitt i seksjonen *Konstruktører*, og definer minst én konstruktør i hver av klassene. Gjør klassediagrammet mer detaljert ved å legge til konstruktørene, samt å markere hvilke metoder som må være offentlige. Marker datafeltene og resten av metodene som private.
9. Vurder nå om flere av de private metodene bør gjøres offentlige. Du må tenke over om metoden bare skal brukes innad i et objekt, eller om andre objekter skal kunne bruke metodene.
10. Følg eksemplet gitt i seksjonen *Dokumentasjon av metoder*; skriv en dokumentasjon av alle metoder som du har valgt å gjøre offentlige. 
11. Finn ut om en av klassene dine har datafelter og metoder som kan legges i en ny klasse. Gi et passende navn til denne klassen og tegn den i diagrammet. Vis avhengigheten mellom de to klassene etter oppdelingen (følg figurene i seksjonen *Oppdeling av klasser*). 
