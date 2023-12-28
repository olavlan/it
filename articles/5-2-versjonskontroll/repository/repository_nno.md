---
title: "Repository"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

Har du eit kodeprosjekt som du gjerne vil leggja ut på Github, slik at andre personar kan bruka programmet, sjå koden og foreslå endringar? Då kan du leggja prosjektet i eit *repository* på Github!

Eit repository er ei mappe av filer som er tilgjengeleg på ein nettadresse på forma *github.com/brukernavn/prosjektnavn*. Som eit døme kan me gå inn på prosjektet [*Flask*](https://github.com/pallets/flask), som er ein Python-pakke for å utvikla nettsider. Her ser me at at eit repository eigentleg består av mange ting, mellom anna:

* Ei kort skildring av programmet.
* Alle mapper og filer i prosjektet. Dette inkluderer programfiler, konfigurasjonsfiler og alt anna som er relevant.
* Ei spesiell fil med namnet *README* inneheld ei lengre skildring av programmet. Her blir gitt oblant anna installasjonsinstruksar, døme på bruk, og annan nyttig informasjon. *README*-fila blir automatisk presentert på framsida og skal skrivast i tekstformatet [Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

I tillegg vil du sjå ei rekkje knappar øvst, mellom anna *Issues* og *Pull requests*:
* Under *Issues* kan ein melda frå om problem og feil med programmet.
* Under *Pull requests* kan ein leggja inn sin eigen versjon av programmet, med eventuelle forbetringar eller retting av feil. Eigaren av programmet kan deretter vurdera å smelta endringane inn i hovudversjonen av programmet. Me skal sjå nærare på dette i dei neste seksjonane.

*Issues* og *Pull requests* er døme på korleis ein kan samarbeida om å forbetra eit program. Då må ein først ha publisert programmet sitt som eit *Github*-repository. Dersom ein ikkje har behov for samarbeid, kan ein i staden lasta ned `git` på maskina si. Det gir moglegheit for å oppretta eit *lokalt repository*, der du kan gjera mykje av det same som på *Github*, men alt skjer på maskina di.

Kva er fordelane med å leggja programmet sitt i eit lokalt repository? To viktige grunnar er:

* Ein kan lagra alle tidlegare **versjonar** av programmet sitt. Viss noko går gale eller ein angrar på ei endring, kan ein enkelt gå tilbake til ein tidlegare versjon. Dette blir kalla *versjonshandtering*. Når ein har gjort nokre endringar, kan ein oppretta ein versjon ved å gjennomføra ein *commit*. Du kan sjølv prøva å gjera ein commit i aktiviteten nedanfor.
* Ein kan laga skilde **greiner** av prosjektet for å testa ut nye idéer utan å påverka hovudversjonen av programmet. Dette blir kalla å oppretta ein *branch*. Dersom ein er fornøgd med ein branch, kan ein deretter smelta han inn i hovudversjonen av programmet. Me skal sjå nærare på branches i neste seksjon.

