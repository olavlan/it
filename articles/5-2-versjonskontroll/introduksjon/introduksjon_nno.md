---
title: "Introduksjon"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

Versjonskontroll er eit viktig verktøy i utviklingsprosjekt for informasjonsteknologi. Det gir fleire fordelar, inkludert:

- Sporing av endringar: Versjonskontrollsystemet held #styr på alle endringar som blir gjorde i kjeldekoden, slik at utviklarane kan sjå kven som gjorde kva, når og kvifor. Dette gjer det lettare å finna og feilsøke eventuelle problem.
- Reversering til tidlegare versjonar: Versjonskontrollsystemet gir moglegheit for å gå tilbake til ein tidlegare versjon av koden viss det blir oppdaga feil eller andre problem.
- Fleire utviklarar på same kodebasen: Versjonskontrollsystemet gjer det mogleg for fleire utviklarar å jobba samtidig på same kodebasen. Dette kan vera nyttig i store prosjekt med fleire deltakarar.
- Branches: Versjonskontrollsystemet gir også høvet til å arbeida på ulike branches. Dette kan vera nyttig for å utvikla nye funksjonar, testa nye idear, eller for å halda koden meir stabil.
- Integrera endringar: Versjonskontrollsystemet gir moglegheit for å integrera endringar frå fleire branches og dermed sørgjer for å halda koden synkronisert.
- Deling av kode: Versjonskontrollsystemet gjer det lettare å dela koden med andre utviklarar eller open kjeldekode-prosjekt.
- Backup: Versjonskontrollsystemet gir også moglegheit for å ha backup av koden din, slik at du kan retta opp igjen koden din til ein tidlegare versjon viss noko skulle skje.

Det finst fleire verktøy for versjonskontroll, som Git, SVN og Mercurial, kvar med sine eigne fordelar og ulemper. Det er viktig å velja eit verktøy som passar best til prosjektet ditt og teamet ditt. Git er ofte brukt i open kjeldekode-prosjekt, medan SVN og Mercurial er meir vanlege i kommersielle prosjekt.

**Git.** Git er eit open kjeldekode-verktøy for versjonskontroll. Det gjer det mogleg å spora endringar i kjeldekoden og gjera det mogleg å reversering til tidlegare versjonar av koden. Det gir også moglegheit for fleire utviklarar å jobba samtidig på same kodebasen utan å skapa konfliktar.

Nokre av dei viktigaste funksjonane i Git inkluderer:

- Commits: Ein commit er ei lagring av endringar i koden. Kvar commit har ein unik ID, ei skildring av endringane som er gjorde og informasjon om kven som gjorde endringane.
- Branches: Git gir høvet til å arbeida med fleire branches av koden samtidig. Dette gjer det lettare å utvikla nye funksjonar, testa nye idear, eller for å halda koden stabil.
- Merging: Git gir moglegheit for å integrera endringar frå fleire branches og dermed sørgjer for å halda koden synkronisert.
- Remote repositories: Git gir moglegheit for å lagra koden din på eit remote repository, som kan vera tilgjengeleg for andre utviklarar eller open kjeldekode-prosjekt.
- Collaboration: Git gjer det lettare å samarbeida med andre utviklarar ved å gi moglegheit for å dela kode, merge endringar og halda koden synkronisert.
- Version history: Git gir fullstendig historie av alle versjonar av koden, slik at ein kan sjå kven som gjorde endringar, når dei vart gjorde, og kva som vart endra.
- Local and Remote: Git gir moglegheit for å ha ein lokal versjon av koden din, og dessutan å ha ein remote kopi som kan synkroniserast med andre utviklarars kode og gjer det lettare å jobba på same prosjekt samtidig.

Git er eit av dei mest populære verktøya for versjonskontroll og blir brukte av mange utviklarar og organisasjonar over heile verda. Det er lett å setja opp og bruka, og har eit stort fellesskap som gir støtte og hjelp.

**Tenester for versjonskontroll basert på Git.** GitHub og GitLab er begge tenester for versjonskontroll basert på Git, men dei har nokre forskjellar i funksjonar og bruksområde.

GitHub er ei skybasert teneste som tilbyr hosting av Git-repositorier. Det er veldig populært blant open kjeldekode-utviklarar og gir enkel tilgang til kode og samarbeid med andre utviklarar. GitHub gir også verktøy for å dela og samarbeida om kode, og dessutan integrasjonar med andre verktøy som issue tracking og pull requests.

GitLab, på den andre sida, er både ein skybasert og ein on-premises løysing som gir hosting av Git-repositorier. Den gir mange av dei same funksjonane som GitHub, men legg også til verktøy for kontinuerleg integrasjon og levering, #pipeline management og static code analysis. GitLab gir også moglegheit for å ha full kontroll over dataa og infrastrukturen, noko som kan vera viktig for organisasjonar som ønskjer å halda dataa internt.

Begge verktøya har eit stort fellesskap av utviklarar og gir mange verktøy for å samarbeida og dela kode. Likevel, viss du ønskjer å ha full kontroll over dataa og infrastrukturen, og har behov for verktøy for kontinuerleg integrasjon og levering, kan GitLab vera eit betre val, medan GitHub er meir populært for open kjeldekode-prosjekt og samarbeid med andre utviklarar.

