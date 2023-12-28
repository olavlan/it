---
title: "Repository i praksis"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

I denne oppgåva skal du prøva å oppretta ditt eige repository. Du kan ta utgangspunkt i eit kodeprosjekt du allereie har, eller eit prosjekt du kunne tenkja deg å byrja på.

Først må me gjera litt oppsett:

1. Installer *git* på maskina di ved å følgja [instruksjonane](https://git-scm.com/book/en/v2/getting-started-installing-git) for Linux, Mac eller Windows.
2. Logg inn på [*Github*](https://github.com/) eller opprett ein brukar.
3. For å seinare kunna logga inn på *Github* på kommandolinja, må me oppretta ein *Personal Access Token*. Klikk på profilbiletet ditt, og deretter på *Settings*. Trykk på *Developer settings*, som du finn heilt nedst på sida. Klikk så på *Personal access tokens* - *Tokens (classic)*, og deretter på *Generate a new token (classic)*. Under *Select scope* skal du kryssa av *repo*. Du kan velja namn og varigheit etter eige ønske. Når du har trykt *Generate token* kjem det opp eit passord som du må kopiera og lagra i ei tekstfil! Dette er din *Personal access token*! Du kan når som helst gjenta prosessen dersom noko ikkje fungerer.

No er me klare for å oppretta vår første repository.

4. Når du er på *Github*-framsida, klikk på *+*, og deretter *New repository*. Under *Repository name*, vel eit passande namn på prosjektet.
5. Bruk kommandolinjeprogrammet (*Terminal* på Linux og Mac, *cmd.exa* på Windows) til å gå inn på mappa der du har lagra prosjektet (viss du ikkje har eit eksisterande prosjekt, opprett ei mappe og legg inn ei testfil):

```bash
cd "My project"
```

Viser gjerne innhaldet for å sjekka at du er på rett mappe:
```bash
ls
```

6. Gjer mappa di til eit lokalt repository ved å bruka kommandoen `git init`:

```bash
git init
```

7. Kople mappa til ditt *Github*-repository (frå steig 2) med kommandoen under. Du skal setja inn nettadressen til ditt eige *Github*-repository!

```bash
git remote add origin https://github.com/username/repository_name
```

8. Gjer alle filene klare for commit med følgjande kommando:

```bash
git add --all
```

9. Gjer din første commit:

```bash
git commit -m "My first commit"
```

10. Last opp filene til ditt *Github*-repository med kommandoen:

```bash
git push origin master
```
Du vil no bli bede om å skriva inn brukarnamnet og passordet til din *Github*-bruker. Når du blir beden om passord, skal du skriva inn ditt *Personal access token* som du oppretta i steg 3!

11. Opne ei av filene i den lokale prosjektmappa, og gjer nokre endringar og tillegg. Gjenta deretter steg 8-10:

```bash
git add --all
git commit -m "Description of changes"
git push origin master
```

12. Gå inn på nettadressen til ditt *Github*-repository. Under den grøne *Code*-knappen skal det no stå *2 commits*. Trykk på teksten for å komma du til ei liste over alle commits du har gjort. Ved å trykkja på din siste commit kan du sjå ei oversikt over alle endringar du gjorde i førre steg. Forsøk også å trykkja på din første commit, og deretter på *View blir filt*. Dette viser alle filene slik dei var før du gjorde endringane.

