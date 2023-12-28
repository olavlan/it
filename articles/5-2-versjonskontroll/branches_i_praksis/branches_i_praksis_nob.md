---
title: "Branches i praksis"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

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
