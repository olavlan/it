# Versjonskontroll

## Introduksjon

Versjonskontroll er et viktig verktøy i utviklingsprosjekter for informasjonsteknologi. Det gir flere fordeler, inkludert:

- Sporing av endringer: Versjonskontrollsystemet holder styr på alle endringer som gjøres i kildekoden, slik at utviklerne kan se hvem som gjorde hva, når og hvorfor. Dette gjør det lettere å finne og feilsøke eventuelle problemer.
- Reversering til tidligere versjoner: Versjonskontrollsystemet gir mulighet for å gå tilbake til en tidligere versjon av koden hvis det oppdages feil eller andre problemer.
- Flere utviklere på samme kodebasen: Versjonskontrollsystemet gjør det mulig for flere utviklere å jobbe samtidig på samme kodebasen. Dette kan være nyttig i store prosjekter med flere deltakere.
- Branches: Versjonskontrollsystemet gir også muligheten til å arbeide på ulike branches. Dette kan være nyttig for å utvikle nye funksjoner, teste nye ideer, eller for å holde koden mer stabil.
- Integrere endringer: Versjonskontrollsystemet gir mulighet for å integrere endringer fra flere branches og dermed sørger for å holde koden synkronisert.
- Deling av kode: Versjonskontrollsystemet gjør det lettere å dele koden med andre utviklere eller åpen kildekode-prosjekter.
- Backup: Versjonskontrollsystemet gir også mulighet for å ha backup av koden din, slik at du kan gjenopprette koden din til en tidligere versjon hvis noe skulle skje.

Det finnes flere verktøy for versjonskontroll, som Git, SVN og Mercurial, hver med sine egne fordeler og ulemper. Det er viktig å velge et verktøy som passer best til ditt prosjekt og teamet ditt. Git er ofte brukt i åpen kildekode-prosjekter, mens SVN og Mercurial er mer vanlige i kommersielle prosjekter.

**Git.** Git er et åpen kildekode-verktøy for versjonskontroll. Det gjør det mulig å spore endringer i kildekoden og gjøre det mulig å reversering til tidligere versjoner av koden. Det gir også mulighet for flere utviklere å jobbe samtidig på samme kodebasen uten å skape konflikter.

Noen av de viktigste funksjonene i Git inkluderer:

- Commits: En commit er en lagring av endringer i koden. Hver commit har en unik ID, en beskrivelse av endringene som er gjort og informasjon om hvem som gjorde endringene.
- Branches: Git gir muligheten til å arbeide med flere branches av koden samtidig. Dette gjør det lettere å utvikle nye funksjoner, teste nye ideer, eller for å holde koden stabil.
- Merging: Git gir mulighet for å integrere endringer fra flere branches og dermed sørger for å holde koden synkronisert.
- Remote repositories: Git gir mulighet for å lagre koden din på et remote repository, som kan være tilgjengelig for andre utviklere eller åpen kildekode-prosjekter.
- Collaboration: Git gjør det lettere å samarbeide med andre utviklere ved å gi mulighet for å dele kode, merge endringer og holde koden synkronisert.
- Version history: Git gir fullstendig historie av alle versjoner av koden, slik at man kan se hvem som gjorde endringer, når de ble gjort, og hva som ble endret.
- Local and Remote: Git gir mulighet for å ha en lokal versjon av koden din, samt å ha en remote kopi som kan synkroniseres med andre utvikleres kode og gjør det lettere å jobbe på samme prosjekt samtidig.

Git er et av de mest populære verktøyene for versjonskontroll og brukes av mange utviklere og organisasjoner over hele verden. Det er lett å sette opp og bruke, og har et stort fellesskap som gir støtte og hjelp.

**Tjenester for versjonskontroll basert på Git.** GitHub og GitLab er begge tjenester for versjonskontroll basert på Git, men de har noen forskjeller i funksjoner og bruksområder.

GitHub er en skybasert tjeneste som tilbyr hosting av Git-repositorier. Det er veldig populært blant åpen kildekode-utviklere og gir enkel tilgang til kode og samarbeid med andre utviklere. GitHub gir også verktøy for å dele og samarbeide om kode, samt integrasjoner med andre verktøy som issue tracking og pull requests.

GitLab, på den annen side, er både en skybasert og en on-premises løsning som gir hosting av Git-repositorier. Den gir mange av de samme funksjonene som GitHub, men legger også til verktøy for kontinuerlig integrasjon og levering, pipeline management og static code analysis. GitLab gir også mulighet for å ha full kontroll over dataene og infrastrukturen, noe som kan være viktig for organisasjoner som ønsker å holde dataene internt.

Begge verktøyene har et stort fellesskap av utviklere og gir mange verktøy for å samarbeide og dele kode. Imidlertid, hvis du ønsker å ha full kontroll over dataene og infrastrukturen, og har behov for verktøy for kontinuerlig integrasjon og levering, kan GitLab være et bedre valg, mens GitHub er mer populært for åpen kildekode-prosjekter og samarbeid med andre utviklere.

## Repository

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

## Repository i praksis

I denne oppgaven skal du forsøke å opprette ditt eget repository. Du kan ta utgangspunkt i et kodeprosjekt du allerede har, eller et prosjekt du kunne tenke deg å begynne på. 

Først må vi gjøre litt oppsett:

1. Installer *git* på maskinen din ved å følge [instruksjonene](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for Linux, Mac eller Windows.
2. Logg inn på [*Github*](https://github.com/) eller opprett en bruker.
3. For å senere kunne logge inn på *Github* på kommandolinjen, må vi opprette en *Personal Access Token*. Klikk på profilbildet ditt, og deretter på *Settings*. Trykk på *Developer settings*, som du finner helt nederst på siden. Klikk så på *Personal access tokens* - *Tokens (classic)*, og deretter på *Generate a new token (classic)*. Under *Select scope* skal du krysse av *repo*. Du kan velge navn og varighet etter eget ønske. Når du har trykket *Generate token* kommer det opp et passord som du må kopiere og lagre i en tekstfil! Dette er din *Personal access token*! Du kan når som helst gjenta prosessen dersom noe ikke fungerer.

Nå er vi klare for å opprette vår første repository.

4. Når du er på *Github*-forsiden, klikk på *+*, og deretter *New repository*. Under *Repository name*, velg et passende navn på prosjektet. 
5. Bruk kommandolinjeprogrammet (*Terminal* på Linux og Mac, *cmd.exe* på Windows) til å gå inn på mappen der du har lagret prosjektet (hvis du ikke har et eksisterende prosjekt, opprett en mappe og legg inn en testfil):

```bash
cd "My project"
```

Vis gjerne innholdet for å sjekke at du er på riktig mappe:
```bash
ls
```

6. Gjør mappen din til et lokalt repository ved å bruke kommandoen `git init`:

```bash
git init
```

7. Koble mappen til ditt *Github*-repository (fra steg 2) med kommandoen under. Du skal sette inn nettadressen til ditt eget *Github*-repository!

```bash
git remote add origin https://github.com/username/repository_name
```

8. Gjør alle filene klare for commit med følgende kommando:

```bash
git add --all
```

9. Gjør din første commit:

```bash
git commit -m "My first commit"
```

10. Last opp filene til ditt *Github*-repository med kommandoen:

```bash
git push origin master
```
Du vil nå bli bedt om å skrive inn brukernavnet og passordet til din *Github*-bruker. Når du blir bedt om passord, skal du skrive inn ditt *Personal access token* som du opprettet i steg 3!

11. Åpne en av filene i den lokale prosjektmappen, og gjør noen endringer og tillegg. Gjenta deretter steg 8-10:

```bash
git add --all
git commit -m "Description of changes"
git push origin master
```

12. Gå inn på nettadressen til ditt *Github*-repository. Under den grønne *Code*-knappen skal det nå stå *2 commits*. Trykk på teksten for å komme du til en liste over alle commits du har gjort. Ved å trykke på din siste commit kan du se en oversikt over alle endringer du gjorde i forrige steg. Forsøk også å trykke på din første commit, og deretter på *View files*. Dette viser alle filene slik de var før du gjorde endringene.

## Branches

Som nevnt i forrige seksjon, er *branches* (*grener* på norsk) en måte å teste ut nye idéer uten å påvirke hovedversjonen av programmet ditt. En branch er i utgangspunktet bare en kopi av alle filene i programmet. 

Branches er noe du vil se i et hvilket som helst *Github*-repository av en viss størrelse. Hvis du for eksempel går inn på prosjektet [Flask](https://github.com/pallets/flask), vil du se at det står *8 branches* like over listen av filer. Til venstre for dette står det *main*, som er hovedversjonen av programmet. Ved å trykke på *main*, vil du få opp en nedtrekksmeny der du kan velge en annen branch av programmet.

Hovedversjonen av et program er en branch som gjerne har navnet *master* eller *main*. Det er hovedversjonen vi først ser når vi går inn på et *Github*-repository, og som ofte er den mest stabile versjonen av programmet. Når man vil legge til ny funksjonalitet i et program, er det vanlig å opprette en ny branch, der man fritt kan endre og legge til kode. 

[Denne](https://docs.github.com/assets/cb-2058/mw-1440/images/help/branches/pr-retargeting-diagram1.webp) figuren viser at *main* er som stammen i et tre, mens andre branches er som grener. Figuren viser også et par andre ting: 
* Dersom man til slutt er fornøyd med endringene, kan man smelte en branch inn i hovedversjonen. Dette kalles en *merge*. I figuren skjer det for eksempel en merge av *feature1* inn i *main*. Hva skjer egentlig her? Hvis mulig, så vil alle endringene som ble gjort i *feature1* legges inn i *main*. Men merk at *main* også kan ha blitt endret i mellomtiden! Da kan ulike tilfeller oppstå:
    * Endringene i *feature1* og endringene i *main* er på forskjellige filer. Disse endringene kommer ikke i veien for hverandre, og man kan gjøre en merge.
    * En endring i *feature1* er på samme fil som en endring i *main*.
        * Dersom endringene er på ulike steder i filen, så kan man fortsatt gjøre en merge, fordi *Github* vil sørge for at begge endringene kommer med i filen.
        * Dersom endringen er på samme kodelinje, så vil *Github* varsle om at man har en konflikt, og at merge ikke kan skje! Da må man løse denne konflikten (endre koden) før man kan gjøre en merge.
* Legg merke til at branches kan opprettes oppå hverandre! Det kan for eksempel være aktuelt når man skal utvikle en ny versjon av et program. Da kan man opprette en branch som heter noe slikt som *v2.0*. Hvis den nye versjonen skal ha tre nye funksjoner, så kan *v2.0* ha tre nye branches. Etter hvert som  de nye funksjonene er klare, kan de smeltes inn i *v2.0*, og til slutt kan *v2.0* smeltes inn i hovedversjonen. 

Hva er poenget med branches? Det er flere viktige fordeler:
* Man får en **trygg** måte å teste ut nye idéer, legge til funksjonalitet eller fikse feil. Det er trygt fordi man ikke trenger å bekymre seg for å påvirke hovedversjonen av programmet, som gjerne skal holdes mest mulig stabil.
* Siden hver branch kan sees på som en versjon av programmet, kan man jobbe med flere versjoner samtidig, og til slutt bestemme seg for hvilke versjoner man vil smelte inn i den endelige utgaven. Dette gir **fleksibilitet** til å kode uten å gjøre noen forpliktende avgjørelser om hvordan det ferdige programmet skal være.
* Nye funksjoner kan **testes** på en branch før det settes inn i hovedversjonen. Brukere av programmet vil sette pris på at alle funksjonene i hovedversjonen er grundig testet.
* **Samarbeid**: Som vi skal se nærmere på i de neste seksjonene, gjør branches at flere personer kan jobbe samtidig på det samme prosjektet. Ved at hver person jobber på hver sin branch, unngår man å komme i veien for hverandre. Til slutt smeltes de ulike grenene sammen, og eventuelle konflikter løses.

Trygghet, fleksibilitet, testing og samarbeid er altså noen stikkord som beskriver hvorfor branches er så nyttig.

## Branches i praksis

Gjør først aktiviteten fra forrige seksjon. Nå skal vi opprette en ny branch i prosjektet. 

1. Åpne kommandolinjeprogrammet og gå inn på prosjektmappen:

```bash
cd "My project"
```

2. Hvis du jobber med et eksisterende prosjekt, kan du nå tenke på en funksjonalitet du har lyst til å legge til. Opprett en ny branch med kommandoen gitt under. Erstatt gjerne *feature1* med et passende navn (bruk bindestrek i stedet for mellomrom).

```bash
git branch feature1
```

Sjekk nå hvilke branches som eksisterer med følgende kommando:

```bash
git branch
```

Her vil du se både *master* (hovedgrenen) og din nye *branch*. En stjerne (*) markerer at det er *master* du jobber med nå. 

3. Nå skal du opprette en egen mappe for din nye branch, slik at du kan jobbe med dine to branches hver for seg. Bruk kommandoen under, men endre først *feature1* til navnet på din nye branch. 

```bash
git worktree add "../feature1" feature1
```

Her har vi lagt vår nye branch *feature1* i mappen *../feature1*. Merk at *../* navigerer en mappe tilbake, slik at våre to branches havner på samme nivå i mappehierarkiet. 

4. Bruk filutforskeren på din maskin til å gå inn på den nye mappen. Du vil se at filene fra *master* har blitt kopiert til denne mappen.

Gå også inn på den nye mappen i kommandolinjen:

```bash
cd "../feature1"
```

Prøv igjen å sjekke hvilke branches som eksisterer: 

```bash
git branch
```

Siden du er inne på mappen til din nye branch, er denne nå markert med stjerne (*). Du vil også se at *master* er markert med pluss (+), fordi det er hovedgrenen.  

5. Gjør noen endringer i din nye branch (endre noen filer i den nye mappen). Gjør deretter alle filer klare for commit og gjennomfør en commit:

```bash
git add --all
git commit -m "Description of changes"
```

Last opp filene til ditt *Github*-repository med kommandoen under. Det er viktig at du erstatter *feature1* med navnet på din nye branch.

```bash
git push origin feature1
```

Igjen vil du bli bedt om brukernavn og passord, og du må huske å bruke ditt *Personal Access Token* som passord. 

6. Gå inn på nettadressen til ditt *Github*-repository. Like over listen av filer skal det nå stå *2 branches*, og til venstre for dette kan du skifte mellom dem med en nedtrekksmeny. Gå inn på din nye branch og sjekk at filene er endret (du kan åpne filene ved å trykke på dem). Sjekk også at *master* ikke har disse endringene.

Forestill deg at din nye branch (som du opprettet i forrige seksjon) er ferdig, det vil si at den nye funksjonaliteten er grundig testet og fungerer.  Du ønsker nå at din nye branch skal smeltes inn i *master*. 

7. Gå inn på nettadressen til ditt *Github*-repository og trykk på *Pull requests*. Klikk deretter på *New pull request*. Du vil nå se to nedtrekksmenyer, der den ene er merket *base* og den andre er merket *compare*. Du skal velge *master* på *base*, og din nye branch på *compare*. Dette betyr at du ønsker å smelte din nye branch inn i *master* (legg merke til pilen som viser dette).
8. Dersom det står *Able to merge*, kan du nå trykke på *Create pull request*. Du kan nå gi et navn til din pull request og legge inn eventuelle kommentarer (navn og kommentarer skal gjerne fortelle hvilke forbedringer som er gjort i din nye branch). Klikk til slutt på *Create pull request* igjen.
9. Du vil nå se din nye pull request. En pull request er en forespørsel om å smelte din nye branch inn i *master*. Siden du er på ditt eget repository, har du mulighet til å godta forespørselen ved å trykke på *Merge pull request*. Du kan nå gjøre det.
10. Gå til forsiden av ditt repository og sjekk at *master* har fått endringene du gjorde i den nye branchen.

**Ekstra 1.** Følg stegene 2-5 til å opprette en ny branch fra *master*. Forsøk nå å gjøre en endring i både  *master* og din nye branch. Endringen skal være på samme fil, men forskjellig kodelinje. Husk å kjøre følgende kommandoer for å legge til endringene: 

```bash
git add --all
git commit -m "Description of changes"
git push origin master
```
Husk at kommandoene må kjøres i hver branch. 

Følg stegene 7-10 til å smelte din nye branch inn i *master*. Hva skjer med filen som ble endret i både *master* og din nye branch?

**Ekstra 2.** Gjenta oppgaven over, men gjør en endring på samme kodelinje! Hva skjer når du prøver å smelte din nye branch inn i *master*?
