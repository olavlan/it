---
title: "Klassar med felles datafelt og metodar"
belongs_to_chain: "Arv"
figures_to_include:
	- "klasse_film1.svg"
	- "klasse_film_bok_felles.svg"
	- "superklasse0.svg"
	- "superklasse1.svg"
	- "superklasse2.svg"
---

I dei førre kapitla planla me eit program for ei boksamling. Tenk deg no at me også har filmar i samlinga, og at me ønskjer å kunna låna ut filmane, og dessutan å henta og lagra informasjon om filmane på nett.

Filmobjekt bør vera med i modellen vår, fordi:

*  Eit filmobjekt har relevante datafelt, til dømes "Tittel", "Diskformat" og datafelt knytt til lånestatus.
* Eit filmobjekt har relevante metodar, til dømes "Lån ut", "Levér inn" og "Hent informasjon på nett".

Me kan no oppretta ein `Film`-klasse, det vil seia ein mal for alle filmobjekt:

<img src="/media/markdowncontent/assosiated_files/klasse_film1.svg" width="150">

Du har kanskje lagt merke til at klassen `Film` har nokon datafelt og metodar som også finst i klassen `Bok`?

<img src="/media/markdowncontent/assosiated_files/klasse_film_bok_felles.svg" width="400">

La oss sjå på korleis eit `Bok`-objekt og eit `Film`-objekt blir oppretta frå klassane sine:

<img src="/media/markdowncontent/assosiated_files/superklasse0.svg" width="400">

Ved å plassera dei raude datafelta og metodane øvst, ser me endå tydelegare kva dei to objekta har til felles, og kva som skil dei:

<img src="/media/markdowncontent/assosiated_files/superklasse1.svg" width="400">

* Den øvste delen av objekta viser datafelt og metodar knytt til utlån. Viss me berre ser på denne delen, er objekta av same type - dei er begge "utlånsobjekt".
* Den nedste delen av objekta viser datafelt og metodar som er spesifikke for bøker og filmar, og som gjer at me treng to ulike klassar.

Når me har skissert `Film`-klassen, har me altså gjenteke alle eigenskapar og metodar knytt til utlån, sjølv om `Bok`-klassen har akkurat dei same. Kan me gjera det betre? Ja, her kan me bruka *arv*! Måten me gjer det på er å laga ein basisklasse som inneheld dei datafelta og metodane som klassane har til felles:

<img src="/media/markdowncontent/assosiated_files/superklasse2.svg" width="400">

Dei to øvste pilene viser at `Film` -og `Bok`-klassen får alle datafelta og metodane som finst i basisklassen. Derfor treng me berre å skriva dei spesifikke delane som handlar om filmar og bøker. Når me opprettar objekt, får me med både basisdelane og dei spesifikke delane.


