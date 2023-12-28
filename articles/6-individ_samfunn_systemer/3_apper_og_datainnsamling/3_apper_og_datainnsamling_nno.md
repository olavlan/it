---
title: "Appar og datainnsamling"
belongs_to_chain: "Individ, samfunn og systemer"
figures_to_include:
---

I dag er det vanskeleg å tenkja seg ein kvardag utan ein smarttelefon med ei rekkje applikasjonar. Korleis skal me senda melding til den personen som me ikkje har nummeret til? Korleis skal me betala bussbilletten? Korleis skal me høyra på musikk på bussen? Dette er døme på korleis **appar** har vorte uunnværlege, både med tanke på sosial interaksjon, praktiske sider av kvardagen, og dessutan avslapning og rekreasjon.

Du har antakeleg brukt ruteplanleggjaren i *Google Maps*, som ikkje berre gir deg den raskaste ruta, men også fortel kor lang tid reisa vil tek, trafikken teke i betraktning. Det kan også henda at du har funne nokon av *Tiktok* -eller *Instagram*-kontoane du liker best gjennom tilrådingar i appen. Dette er to døme på appar som bruker **datainnsamling** til å forbetra brukaropplevinga.

Mange av appane me bruker er avhengige av å samla data for å fungera godt. Nokon måtar appar samlar data på er:

- **Data skrive inn av brukaren.** Det kan til dømes vera snakk om personleg data som namn, alder og kjønn.
- **Lokasjondata.** Ein app kan lagra posisjonen din, både når appen er open og når han køyrer i bakgrunnen.
- **Sensordata.** Ein app kan lagra informasjon frå sensorar på telefonen, som til dømes mikrofonen eller kameraet.
- **Brukarmønster.** I prinsippet kan alle handlingar du gjer i appen lagrast. Til dømes kan ein musikkapp lagra alle låtane du har spelt av, og på kva tidspunkt.
- **Integrasjon på tvers av plattformer.** På mange appar vil ein logga inn med same brukarprofil som på nettsider eller andre plattformer. Appen vil då kunna ha tilgang til data knytt til brukarprofilen, men registrert utanfor appen.
- **Innlogging med tredjepart.** Nokre appar tilbyr innlogging med til dømes *Google* eller *Facebook*. Ofte godtek ein samtidig at appen kan henta delar av dataa knytt til brukaren din, og senda data tilbake.

Data som blir samla inn kan anten lagrast lokalt, det vil seia på smarttelefonen sin lagringsdisk, eller det kan lagrast i ein database hos firmaet som står bak appen. I det siste tilfellet vil dataa lagrast saman med eit unikt id-nummer, som fortel kva mobileining informasjonen kjem frå. Seinare kan appen henta den rette informasjonen frå databasen, ved å søkja opp id-nummeret.

Innsamling av data kan brukast til reelle forbetringar av appen, som brukaren har nytte og glede av. Døme er:

**Tilpassa brukaropplevingar.**  Appar som *YouTube*, *Instagram* og *Tiktok* kan tilrå kanalar, videoar og innlegg basert på kva du har sett mest på, eller kva du har likt eller kommentert. Ein musikkstrøymingsapp kan foreslå nye låtar og artistar basert på lyttehistorikken din. Læringsappar som *KhanAcademy* eller *Duolingo* kan lagra data om progresjonen din, og bruka det til å tilrå og tilpassa læringsmaterialet.

**Forbetre tenester.** Mange appar samlar data for å forbetra tenestene til appen. Her er det ikkje snakk om tilpassa funksjonar for den enkelte brukaren, men forbetra appen for alle brukarar.
* *Google Maps* samlar lokasjondata frå reisande for å estimera trafikken på vegar eller forseinkingar i offentleg transport, og bruker dette til å tilrå betre ruter. Vidare blir brukt lokasjondata til å kontinuerleg oppdatera kartdatabasen med nye vegar, gater og landemerke. Appen kan også estimera kor folksamt det er på offentlege stader, som gjer at ein kan planleggja gjeremål og aktivitetar til rolegare tidspunkt.
* Det er verd å nemna at dataa frå *Google Maps* også kan brukast til samfunnsnyttige formål, til dømes i samband med by -og vegplanlegging, eller til å henta kritisk informasjon om personars lokasjon i nødssituasjonar, slik som ved naturkatastrofar eller ulykker.
* Appar for offentleg transport kan på same måte bruka lokasjondata frå reisande til å forbetra nøyaktigheita av avgangstider, reisetider og gi betre ruteforslag.
* Nokre vêrmeldingsappar kan henta data frå brukaren for å forbetra vêrmeldingar og eventuelle varslingar om ekstremvêr. Appane kan til dømes la brukaren gi tilbakemeldingar om lokale vêrforhold eller henta lufttrykkmålingar frå sensoren til smarttelefonen.
* Som konklusjon kan me seia at appar som hentar lokasjondata, eventuelt saman med anna brukardata, gir betre informasjon og tenester knytt til lokale forhold. Slike tenester kan vera svært nyttig for både individ og samfunn, og dei blir betre jo fleire som bidreg med sine data.
* [*Crowdsourcing*](https://no.wikipedia.org/wiki/nettdugnad) er ein måte å løysa oppgåver basert på små og gjerne frivillige bidrag frå mange menneske. Teknologiane me har sett på følgjer slike prinsipp, og viser den store nytteverdien som kan genererast av mange brukardata. Rett nok er teknologien eigd av *Google* og andre selskap, men informasjonen som blir produsert blir halden ikkje skjult, og kan hentast til bruk i eigne program gjennom *Web-APIer* som blir tilboden av til dømes *Google*. (Sjå seksjonen om *Web-API-er* i kapittelet *Datahåndtering - Utveksling og sikring av data*).
  
Datainnsamling i appar skaper likevel nokre store bekymringar, særleg knytt til personvern:
* **Samling av sensitive data.** Som me såg i førre seksjon, er sensitive data spesielt sårbare for misbruk, og konsekvensane for enkeltpersonar kan vera store.
* **Deling og sal av persondata.** Når persondata blir delt eller blir selt til ein tredjepart, mistar brukaren i stor grad kontrollen over sine data, og risikoen for misbruk aukar.
* **Datatryggleik.** Mange firma samlar inn data utan å gjera tilstrekkelege grep for å verna dataa mot lekkasje og tjuveri.
* **Invasiv datainnsamling.** Mange appar samlar inn persondata som ikkje er nødvendige for funksjonen til appen, med mål om å skapa detaljerte brukarprofilar, som mellom anna kan brukast til målretta reklame.
* **Permanent lagring av lokasjondata.** Sjølv om lokasjondataa samla inn av *Google Maps* kan brukast til svært nyttige formål på kort sikt, er det problematisk at dataa blir lagra permanent. Dersom ein har brukt *Google Maps* i lengre tid, vil ein ha etterlate seg eit stort digitalt fotavtrykk over rørslene sine. Desse dataa er spesielt sårbare for misbruk, og kan koplast til spesifikke personar sjølv om dei ikkje inneheld personinformasjon.

Som eit konkret døme på bekymringane rundt datainnsamling blir den glimrande saka tilrådd [*Avslørt av mobilen*](https://www.nrk.no/norge/xl/avslort-av-mobilen-1.14911685), publisert på *NRK* i 2020. Her blir det fortalt korleis ein kunne betala eit britisk selskap 35.000 kroner for omfattande mengder lokasjondata, som gav informasjon om rørslene til titusenvis av nordmenn i 2019

I denne databasen kunne ein henta alle registrerte rørsler frå ei bestemd mobileining, og ofte kunne eigaren av mobilen identifiserast, ettersom rørslemønsteret leivde liten tvil om bustadadresse, arbeidsstad og liknande informasjon.

Det britiske selskapet hadde altså gjort det til forretning å kjøpa lokasjondata frå ei rekkje populære appar, og deretter selja dei vidare. Mange av appane hadde lokasjonsporing utan at det var nødvendig eller relevant for funksjonen til appen. Desse selskapa prøver ofte å forsvara seg med at dataa dei samlar inn er anonyme, sjølv om dataa er så detaljerte at identifisering kan oppnåast relativt enkelt.

Detaljert lokasjondata er svært sårbare for misbruk. Dei kan til dømes fortelja om opphald på sjukehus, psykiatriske institusjonar og krisesenter, som ein lesa meir om i [oppfølgingssakene](https://www.nrk.no/emne/mobilsporing-1.14925990).

