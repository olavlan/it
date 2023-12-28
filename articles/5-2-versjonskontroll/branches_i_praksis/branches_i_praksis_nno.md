---
title: "Branches i praksis"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

Gjer først aktiviteten frå førre seksjon. No skal me oppretta ein ny branch i prosjektet.

1. Opne kommandolinjeprogrammet og gå inn på prosjektmappa:

```bash
cd "My project"
```

2. Viss du jobbar med eit eksisterande prosjekt, kan du no tenkja på ein funksjonalitet du har lyst til å leggja til. Opprett ein ny branch med kommandoen gitt under. Erstatt gjerne *feature1* med eit passande namn (bruk bindestrek i staden for mellomrom).

```bash
git branch feature1
```

Sjekk no kva branches som eksisterer med følgjande kommando:

```bash
git branch
```

Her vil du sjå både *master* (hovudgreina) og din nye *branch*. Ei stjerne (*) markerer at det er *master* du jobbar med no.

3. No skal du oppretta ei eiga mappe for din nye branch, slik at du kan jobba med dine to branches kvar for seg. Bruk kommandoen under, men endre først *feature1* til namnet på din nye branch.

```bash
git worktree add "../feature1" feature1
```

Her har me lagt vår nye branch *feature1* i mappa *../feature1*. Merk at *../* navigerer ei mappe tilbake, slik at våre to branches hamnar på same nivå i mappehierarkiet.

4. Bruk filutforskaren på maskina di til å gå inn på den nye mappa. Du vil sjå at filene frå *master* har vorte kopierte til denne mappa.

Gå også inn på den nye mappa i kommandolinja:

```bash
cd "../feature1"
```

Prøv igjen å sjekka kva branches som eksisterer:

```bash
git branch
```

Sidan du er inne på mappa til din nye branch, er denne no markert med stjerne (*). Du vil også sjå at *master* er markert med pluss (+), fordi det er hovudgreina.

5. Gjer nokre endringar i din nye branch (endre nokon filer i den nye mappa). Gjer deretter alle filer klare for commit og gjennomfør ein commit:

```bash
git add --all
git commit -m "Description of changes"
```

Last opp filene til ditt *Github*-repository med kommandoen under. Det er viktig at du erstattar *feature1* med namnet på din nye branch.

```bash
git push origin feature1
```

Igjen vil du bli beden om brukarnamn og passord, og du må hugsa å bruka ditt *Personal Access Token* som passord.

6. Gå inn på nettadressen til ditt *Github*-repository. Like over lista av filer skal det no stå *2 branches*, og til venstre for dette kan du skifta mellom dei med ein nedtrekkmeny. Gå inn på din nye branch og sjekk at filene er endra (du kan opna filene ved å trykkja på dei). Sjekk også at *master* ikkje har desse endringane.

Førestill deg at din nye branch (som du oppretta i førre seksjon) er ferdig, det vil seia at den nye funksjonaliteten er grundig testa og fungerer.  Du ønskjer no at din nye branch skal smeltast inn i *master*.

7. Gå inn på nettadressen til ditt *Github*-repository og trykk på *Pull requests*. Klikk deretter på *New pull request*. Du vil no sjå to nedtrekkmenyar, der den eine er merkt *base* og den andre er merkt *compare*. Du skal velja *master* på *base*, og din nye branch på *compare*. Dette betyr at du ønskjer å smelta din nye branch inn i *master* (legg merke til pila som viser dette).
8. Dersom det står *Able to merge*, kan du no trykkja på *Create pull request*. Du kan no gi eit namn til pullen din request og leggja inn eventuelle kommentarar (namn og kommentarar skal gjerne fortelja kva forbetringar som er gjorde i din nye branch). Klikk til slutt på *Create pull request* igjen.
9. Du vil no sjå den nye pullen din request. Ein pull request er ein førespurnad om å smelta din nye branch inn i *master*. Sidan du er på ditt eige repository, har du høve til å godta førespurnaden ved å trykkja på *Merge pull request*. Du kan no gjera det.
10. Gå til framsida av ditt repository og sjekk at *master* har fått endringane du gjorde i den nye branchen.

**Ekstra 1.** Følg stega 2-5 til å oppretta ein ny branch frå *mastar*. Forsøk no å gjera ei endring i både  *master* og din nye branch. Endringa skal vera på same fil, men ulik kodelinje. Hugs å køyra følgjande kommandoar for å leggja til endringane:

```bash
git add --all
git commit -m "Description of changes"
git push origin master
```
Hugs at kommandoane må køyrast i kvar branch.

Følg stega 7-10 til å smelta din nye branch inn i *master*. Kva skjer med fila som vart endra i både *master* og din nye branch?

**Ekstra 2.** Gjenta oppgåva over, men gjer ei endring på same kodelinje! Kva skjer når du prøver å smelta din nye branch inn i *master*?
