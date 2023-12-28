---
title: "Superklassar"
belongs_to_chain: "Arv"
figures_to_include:
	- "klasse_utlaansobjekt.svg"
	- "utlaansobjekter.svg"
	- "klasser_arv.svg"
	- "superklasse_prosess.svg"
---

Korleis kan me seia med éi setning kva `Film`-objektet og `Bok`-objektet har til felles? Me kan seia at dei begge er utlånsobjekt! Det kan vera namnet på basisklassen:

<img src="/media/markdowncontent/assosiated_files/klasse_utlaansobjekt.svg" width="120">

No kan me oppretta `Utlån`-objekt! Kva slags objekt er dette? Alle ting som me ønskjer å låna ut og som har ein tittel! Det kan til dømes eit spel eller ein teikneserie:

<img src="/media/markdowncontent/assosiated_files/utlaansobjekter.svg" width="350">

Det er lett å tenkja at me her bør oppretta nye klassar, til dømes med namn "Spill" og "Tegneserie". Men førebels ønskjer me ikkje å gjera spesifikke handlingar med spel eller teikneseriar. Alt me ønskjer å gjera er å låna dei ut, og då bør me vurdera dei som utlånsobjekt! Å vera veldig spesifikke er altså noko me prøver å unngå når me planlegg eit objektorientert program.

På bøker og filmar ønskjer me derimot å gjera spesifikke handlingar, som å henta informasjon og meldingar på nett. Derfor gir det meining å definera spesifikke klassar for bøker og filmar. Men sidan bøker og filmar også er utlånsobjekt, så må me sørgja for at `Bok` og `Film` arvar alle datafelta og metodane til `Utlånsobjekt`. Dette viser me med følgjande piler:

<img src="/media/markdowncontent/assosiated_files/klasser_arv.svg" width="400">
 
Måten me les diagrammet på er følgjande:

- Den første pila fortel at `Bok` arvar datafelta og metodane i `Utlånsobjekt`. Tilsvarande seier den andre pila at `Film` også arvar datafelta og metodane i `Utlånsobjekt`.
- Me seier at`Utlånsobjekt` er *superklassen* til `Bok` og `Film`.
- Me seier  at `Bok` og `Film` er *subklassene* til `Utlånsobjekt`.

For å samanfatta, så har me identifisert felles datafelt og metodar i klassane `Bok` og `Film`, og laga ein superklasse som inneheld desse. Følgjande figur viser heile prosessen:

<img src="/media/markdowncontent/assosiated_files/superklasse_prosess.svg" width="1000">

Det er fleire fordelar med å definera superklassar:

- Me unngår å repetera dei same metodane i fleire klassar. I staden definerer me desse éin stad, nemleg i superklassen. Det betyr at me også unngår duplisering av kode, og det blir lettare å gjera endringar. Viss me til dømes vil endra måten utlån blir registrert på, treng me berre å endra koden éin stad, nemleg i klassen `Utlånsobjekt`.
- Me kan gjenbruka superklassen til andre formål. Til dømes, dersom me seinare ønskjer eit utlånssystem for heilt andre ting enn bøker og filmar, så kan me gjenbruka klassen `Utlånsobjekt`.

