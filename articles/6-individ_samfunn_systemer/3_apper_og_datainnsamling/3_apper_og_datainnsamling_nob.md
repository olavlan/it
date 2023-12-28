---
title: "Apper og datainnsamling"
belongs_to_chain: "Individ, samfunn og systemer"
figures_to_include:
---

I dag er det vanskelig å tenke seg en hverdag uten en smarttelefon med en rekke applikasjoner. Hvordan skal vi sende melding til den personen som vi ikke har nummeret til? Hvordan skal vi betale bussbilletten? Hvordan skal vi høre på musikk på bussen? Dette er eksempler på hvordan **apper** har blitt uunnværlige, både med tanke på sosial interaksjon, praktiske sider av hverdagen, samt avslapning og rekreasjon. 

Du har antagelig brukt ruteplanleggeren i *Google Maps*, som ikke bare gir deg den raskeste ruten, men også forteller hvor lang tid reisen vil tar, trafikken tatt i betraktning. Det kan også hende at du har funnet noen av *Tiktok* -eller *Instagram*-kontoene du liker best gjennom anbefalinger i appen. Dette er to eksempler på apper som bruker **datainnsamling** til å forbedre brukeropplevelsen.

Mange av appene vi bruker er avhengige av å samle data for å fungere godt. Noen måter apper samler data på er: 

- **Data skrevet inn av brukeren.** Det kan for eksempel være snakk om personlig data som navn, alder og kjønn. 
- **Lokasjonsdata.** En app kan lagre posisjonen din, både når appen er åpen og når den kjører i bakgrunnen.
- **Sensordata.** En app kan lagre informasjon fra sensorer på telefonen, som for eksempel mikrofonen eller kameraet. 
- **Brukermønstre.** I prinsippet kan alle handlinger du gjør i appen lagres. For eksempel kan en musikkapp lagre alle låtene du har spilt av, og på hvilket tidspunkt.
- **Integrasjon på tvers av plattformer.** På mange apper vil man logge inn med samme brukerprofil som på nettsider eller andre plattformer. Appen vil da kunne ha tilgang til data tilknyttet brukerprofilen, men registrert utenfor appen. 
- **Innlogging med tredjepart.** Noen apper tilbyr innlogging med for eksempel *Google* eller *Facebook*. Ofte godtar man samtidig at appen kan hente deler av dataene knyttet til brukeren din, og sende data tilbake. 

Data som samles inn kan enten lagres lokalt, det vil si på smarttelefonen sin lagringsdisk, eller det kan lagres i en database hos firmaet som står bak appen. I det siste tilfellet vil dataene lagres sammen med et unikt id-nummer, som forteller hvilken mobilenhet informasjonen kommer fra. Senere kan appen hente den riktige informasjonen fra databasen, ved å søke opp id-nummeret. 

Innsamling av data kan brukes til reelle forbedringer av appen, som brukeren har nytte og glede av. Eksempler er: 

**Tilpasse brukeropplevelser.**  Apper som *Youtube*, *Instagram* og *Tiktok* kan anbefale kanaler, videoer og innlegg basert på hva du har sett mest på, eller hva du har likt eller kommentert. En musikkstrømmingsapp kan foreslå nye låter og artister basert på din lyttehistorikk. Læringsapper som *KhanAcademy* eller *Duolingo* kan lagre data om din progresjon, og bruke det til å anbefale og tilpasse læringsmaterialet.

**Forbedre tjenester.** Mange apper samler data for å forbedre tjenestene til appen. Her er det ikke snakk om tilpasse funksjoner for den enkelte brukeren, men forbedre appen for alle brukere.
* *Google Maps* samler lokasjonsdata fra reisende for å estimere trafikken på veier eller forsinkelser i offentlig transport, og bruker dette til å anbefale bedre ruter. Videre brukes lokasjonsdata til å kontinuerlig oppdatere kartdatabasen med nye veier, gater og landemerker. Appen kan også estimere hvor folksomt det er på offentlige steder, som gjør at man kan planlegge gjøremål og aktiviteter til roligere tidspunkter. 
* Det er verdt å nevne at dataene fra *Google Maps* også kan brukes til samfunnsnyttige formål, for eksempel i forbindelse med by -og veiplanlegging, eller til å hente kritisk informasjon om personers lokasjon i nødssituasjoner, slik som ved naturkatastrofer eller ulykker. 
* Apper for offentlig transport kan på samme måte bruke lokasjonsdata fra reisende til å forbedre nøyaktigheten av avgangstider, reisetider og gi bedre ruteforslag.
* Noen værmeldingsapper kan hente data fra brukeren for å forbedre værmeldinger og eventuelle varslinger om ekstremvær. Appene kan for eksempel la brukeren gi tilbakemeldinger om lokale værforhold eller hente lufttrykksmålinger fra smarttelefonens sensor. 
* Som konklusjon kan vi si at apper som henter lokasjonsdata, eventuelt sammen med annen brukerdata, gir bedre informasjon og tjenester knyttet til lokale forhold. Slike tjenester kan være svært nyttig for både individ og samfunn, og de blir bedre jo flere som bidrar med sine data.
* [*Crowdsourcing*](https://no.wikipedia.org/wiki/Nettdugnad) er en måte å løse oppgaver basert på små og gjerne frivillige bidrag fra et stort antall mennesker. Teknologiene vi har sett på følger slike prinsipper, og viser den store nytteverdien som kan genereres av et stort antall brukerdata. Riktignok eies teknologien av *Google* og andre selskaper, men informasjonen som produseres holdes ikke skjult, og kan hentes til bruk i egne programmer gjennom *Web-APIer* som tilbys av for eksempel *Google*. (Se seksjonen om *Web-API-er* i kapittelet *Datahåndtering - Utveksling og sikring av data*).
  
Datainnsamling i apper skaper imidlertid noen store bekymringer, særlig knyttet til personvern:
* **Samling av sensitive data.** Som vi så i forrige seksjon, er sensitive data spesielt sårbare for misbruk, og konsekvensene for enkeltpersoner kan være store.
* **Deling og salg av persondata.** Når persondata deles eller selges til en tredjepart, mister brukeren i stor grad kontrollen over sine data, og risikoen for misbruk øker. 
* **Datasikkerhet.** Mange firmaer samler inn data uten å gjøre tilstrekkelige grep for å beskytte dataene mot lekkasje og tyveri. 
* **Invasiv datainnsamling.** Mange apper samler inn persondata som ikke er nødvendige for appens funksjon, med mål om å skape detaljerte brukerprofiler, som blant annet kan brukes til målrettet reklame.
* **Permanent lagring av lokasjonsdata.** Selv om lokasjonsdataene samlet inn av *Google Maps* kan brukes til svært nyttige formål på kort sikt, er det problematisk at dataene lagres permanent. Dersom man har brukt *Google Maps* i lengre tid, vil man ha etterlatt seg et stort digitalt fotavtrykk over sine bevegelser. Disse dataene er spesielt sårbare for misbruk, og kan kobles til spesifikke personer selv om de ikke inneholder personinformasjon. 

Som et konkret eksempel på bekymringene rundt datainnsamling anbefales den glimrende saken [*Avslørt av mobilen*](https://www.nrk.no/norge/xl/avslort-av-mobilen-1.14911685), publisert på *NRK* i 2020. Her fortelles det hvordan man kunne betale et britisk selskap 35.000 kroner for omfattende mengder lokasjonsdata, som ga informasjon om bevegelsene til titusener av nordmenn i 2019. 

I denne databasen kunne man hente alle registrerte bevegelser fra en bestemt mobilenhet, og ofte kunne eieren av mobilen identifiseres, ettersom bevegelsesmønstret levnet liten tvil om bostedsadresse, arbeidssted og lignende informasjon. 

Det britiske selskapet hadde altså gjort det til forretning å kjøpe lokasjonsdata fra en rekke populære apper, og deretter selge dem videre. Mange av appene hadde lokasjonssporing uten at det var nødvendig eller relevant for appens funksjon. Disse selskapene prøver ofte å forsvare seg med at dataene de samler inn er anonyme, selv om dataene er så detaljerte at identifisering kan oppnås relativt enkelt. 

Detaljert lokasjonsdata er svært sårbare for misbruk. De kan for eksempel fortelle om opphold på sykehus, psykiatriske institusjoner og krisesentre, som man lese mer om i [oppfølgingssakene](https://www.nrk.no/emne/mobilsporing-1.14925990).  

