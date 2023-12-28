---
title: "Oppsummering og aktivitetar"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
---

**Oppsummering**

* I objektorientert programmering blir ofte brukt omgrepet *metode* i staden for *funksjon*, og *melding* i staden for *funksjonskall*. Å senda ei melding til eit objekt er å be objektet om å utføra ein av metodane sine.
* Datatypen til eit objekt er det same som namnet til klassen som objektet kjem frå.
* Alle objekt ligg fritt i minnet til datamaskina, og kvart objekt har ei unik minneadresse.  Peikarar sørgjer for at objekt kan finna kvarandre.
* Me bør følgja prinsippet om at ein metode berre skal ha éi oppgåve. Ein metode skal altså berre utføra éi handling. Dersom fleire steg er nødvendig, bør desse blir delegerte til delmetodar.
* Eit flytdiagram er ei skisse av stega i ein metode.
* Når eit objekt nyttar ein metode som blir tilboden av eit anna objekt, og får svar tilbake, har me kommunikasjon mellom objekt. Me seier også at objekta *samhandlar*. Metodane som kan nyttast i objektsamhandling blir offentlege metodar kalla. Metodane som berre kan brukast internt i eit objekt blir private metodar kalla.
* Grensesnittet til ein klasse er alle dei offentlege metodane. Dei offentlege metodane må haldast stabile, slik at kommunikasjonen mellom objekt ikkje blir øydelagd. For å gjera dette lettare, bør me halda grensesnittet så lite som mogleg.
* Kvar klasse har minst éin metode som blir brukt til å oppretta objekt frå klassen. Ein slik metode blir kalla ein konstruktør.
* Ein klasse bør berre ha eitt ansvar. Dersom nokre eigenskapar og metodar har eit meir spesifikt ansvar, kan dei trekkjast ut og danna ein ny klasse. Altså deler me opp ein klasse dersom han har meir enn eitt ansvar.

**Prosjektoppgåve 4.**

Ta utgangspunkt i *Prosjektoppgave 3* frå førre kapittel og gjer følgjande oppgåver:

1. Skriv opp nokre objekt som kjem frå klassane i klassediagrammet ditt (følg døma gitt i seksjonen *Skrivemåte for objekt*).
2. Gjer klassediagrammet meir detaljert ved å skriva datatypar på alle datafelt og metodar (følg døma gitt i seksjonen *Datatyper*). På metodane skal du skriva datatypen til returverdien.
3. Følg dømet i seksjonen *Objektdiagram og peikarar* til å teikna objekta frå punkt 1. Sørg for å få med peikarar mellom objekt!
4. Tenk over kva steg som må utførast for kvar av metodane i klassediagrammet. Kan du finna ein metode som krev fleire steg? Forsøk i så fall å dela opp denne metoden i delmetodar (følg dømet gitt i seksjonen *Oppdeling av metodar*).
5. Teikn eit flytdiagram for metoden i punkt 4 (følg dømet gitt i seksjonen *flytdiagram*).
6. Kan du laga ein metode som fungerer ved å senda meldingar til alle objekt? Her er nokre døme som kan vera til hjelp.
* Tenk at ein har klassane `Butikk` og `Vare`, og den sistnemnde har metoden `antall_dager_til_utgått()`. Då kan `Butikk` ha ein metode som listar alle varer som går ut om mindre enn éi veke.
* Tenk at ein har klassane `Videobibliotek` og `Video`, og den sistnemnde har metoden `komprimer_video()`. Då kan `Videobibliotek` ha ein metode som komprimerer alle videoane i biblioteket.
7. Vis korleis objekta i oppgåve 6 kommuniserer ved å følgja teikninga i seksjonen *Kommunikasjon mellom objekt*. Kva metode må vera offentleg for at kommunikasjonen skal vera mogleg?
8. Følg døma gitt i seksjonen *Konstruktører*, og definer minst éin konstruktør i kvar av klassane. Gjer klassediagrammet meir detaljert ved å leggja til konstruktørane, og dessutan å markera kva metodar som må vera offentlege. Marker datafelta og resten av metodane som private.
9. Vurder no om fleire av dei private metodane bør gjerast offentlege. Du må tenkja over om metoden berre skal brukast internt i eit objekt, eller om andre objekt skal kunna bruka metodane.
10. Følg dømet gitt i seksjonen *Dokumentasjon av metodar*; skriv ein dokumentasjon av alle metodar som du har valt å gjera offentlege.
11. Finn ut om ein av klassane dine har datafelt og metodar som kan leggjast i ein ny klasse. Gi eit passande namn til denne klassen og teikn den i diagrammet. Vis avhengnaden mellom dei to klassane etter oppdelinga (følg figurane i seksjonen *Oppdeling av klassar*).
