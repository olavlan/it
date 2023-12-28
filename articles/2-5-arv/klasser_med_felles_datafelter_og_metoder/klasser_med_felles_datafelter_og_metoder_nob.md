---
title: "Klasser med felles datafelter og metoder"
belongs_to_chain: "Arv"
figures_to_include:
	- "klasse_film1.svg"
	- "klasse_film_bok_felles.svg"
	- "superklasse0.svg"
	- "superklasse1.svg"
	- "superklasse2.svg"
---

I de forrige kapitlene planla vi et program for en boksamling. Tenk deg nå at vi også har filmer i samlingen, og at vi ønsker å kunne låne ut filmene, samt å hente og lagre informasjon om filmene på nett. 

Filmobjekter bør være med i modellen vår, fordi:

*  Et filmobjekt har relevante datafelter, for eksempel "Tittel", "Diskformat" og datafelter knyttet til lånestatus. 
* Et filmobjekt har relevante metoder, for eksempel "Lån ut", "Levér inn" og "Hent informasjon på nett".

Vi kan nå opprette en `Film`-klasse, det vil si en mal for alle filmobjekter:

<img src="/media/markdowncontent/assosiated_files/klasse_film1.svg" width="150">

Du har kanskje lagt merke til at klassen `Film` har noen datafelter og metoder som også finnes i klassen `Bok`?

<img src="/media/markdowncontent/assosiated_files/klasse_film_bok_felles.svg" width="400">

La oss se på hvordan et `Bok`-objekt og et `Film`-objekt opprettes fra sine klasser:

<img src="/media/markdowncontent/assosiated_files/superklasse0.svg" width="400">

Ved å plassere de røde datafeltene og metodene øverst, ser vi enda tydeligere hva de to objektene har til felles, og hva som skiller dem: 

<img src="/media/markdowncontent/assosiated_files/superklasse1.svg" width="400">

* Den øverste delen av objektene viser datafelter og metoder knyttet til utlån. Hvis vi kun ser på denne delen, er objektene av samme type - de er begge "utlånsobjekter". 
* Den nederste delen av objektene viser datafelter og metoder som er spesifikke for bøker og filmer, og som gjør at vi trenger to forskjellige klasser. 

Når vi har skissert `Film`-klassen, har vi altså gjentatt alle egenskaper og metoder knyttet til utlån, selv om `Bok`-klassen har akkurat de samme. Kan vi gjøre det bedre? Ja, her kan vi bruke *arv*! Måten vi gjør det på er å lage en basisklasse som inneholder de datafeltene og metodene som klassene har til felles:

<img src="/media/markdowncontent/assosiated_files/superklasse2.svg" width="400">

De to øverste pilene viser at `Film` -og `Bok`-klassen får alle datafeltene og metodene som finnes i basisklassen. Derfor trenger vi bare å skrive de spesifikke delene som handler om filmer og bøker. Når vi oppretter objekter, får vi med både basisdelene og de spesifikke delene. 


