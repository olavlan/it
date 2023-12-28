---
title: "Repository"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

Har du et kodeprosjekt som du gjerne vil legge ut på Github, slik at andre personer kan bruke programmet, se koden og foreslå endringer? Da kan du legge prosjektet i et *repository* på Github! 

Et repository er en mappe av filer som er tilgjengelig på en nettadresse på formen *github.com/brukernavn/prosjektnavn*. Som et eksempel kan vi gå inn på prosjektet [*Flask*](https://github.com/pallets/flask), som er en Python-pakke for å utvikle nettsider. Her ser vi at at et repository egentlig består av mange ting, blant annet: 

* En kort beskrivelse av programmet.
* Alle mapper og filer i prosjektet. Dette inkluderer programfiler, konfigurasjonsfiler og alt annet som er relevant.
* En spesiell fil med navnet *README* inneholder en lengre beskrivelse av programmet. Her gis oblant annet installasjonsinstrukser, eksempler på bruk, og annen nyttig informasjon. *README*-filen blir automatisk presentert på forsiden og skal skrives i tekstformatet [Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

I tillegg vil du se en rekke knapper øverst, blant annet *Issues* og *Pull requests*:
* Under *Issues* kan man melde fra om problemer og feil med programmet.
* Under *Pull requests* kan man legge inn sin egen versjon av programmet, med eventuelle forbedringer eller retting av feil. Eieren av programmet kan deretter vurdere å smelte endringene inn i hovedversjonen av programmet. Vi skal se nærmere på dette i de neste seksjonene.

*Issues* og *Pull requests* er eksempler på hvordan man kan samarbeide om å forbedre et program. Da må man først ha publisert programmet sitt som et *Github*-repository. Dersom man ikke har behov for samarbeid, kan man i stedet laste ned `git` på maskinen sin. Det gir mulighet for å opprette et *lokalt repository*, der du kan gjøre mye av det samme som på *Github*, men alt skjer på din maskin. 

Hva er fordelene med å legge programmet sitt i et lokalt repository? To viktige grunner er:

* Man kan lagre alle tidligere **versjoner** av programmet sitt. Hvis noe går galt eller man angrer på en endring, kan man enkelt gå tilbake til en tidligere versjon. Dette kalles *versjonshåndtering*. Når man har gjort noen endringer, kan man opprette en versjon ved å gjennomføre en *commit*. Du kan selv forsøke å gjøre en commit i aktiviteten nedenfor.
* Man kan lage adskilte **grener** av prosjektet for å teste ut nye idéer uten å påvirke hovedversjonen av programmet. Dette kalles å opprette en *branch*. Dersom man er fornøyd med en branch, kan man deretter smelte den inn i hovedversjonen av programmet. Vi skal se nærmere på branches i neste seksjon.

