---
title: "Repository i praksis"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

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

