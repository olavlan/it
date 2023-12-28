---
title: "Skrivemåte for objekter"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasser_med_navn.svg"
---

Fra forrige kapittel har vi følgende klassediagram:

<img src="/media/markdowncontent/assosiated_files/klasser_med_navn.svg" width="300">

Dette er maler som vi bruker til å opprette objekter. Tenk deg at vi har *Sofies verden* i bokhylla, og ønsker å registrere boka i systemet. Da oppretter et `Bok`-objekt og setter inn riktige verdier. 

I bokhylla har vi altså en fysisk bok, og i datamaskinens minne har vi et objekt som representerer boka. I de neste seksjonene vil det være nyttig å skille mellom disse tingene. For å snakke om objektet som ligger i datamaskinens minne kan vi derfor bruke følgende skrivemåte: 

`Bok("Sofies verden")` 

Først sier vi hvilken klasse objektet kommer fra, deretter skriver vi de viktigste verdiene i parenteser. Dersom vi ønsket å ta med forfatternavnet, kunne vi ha skrevet `Bok("Sofies verden", "Jostein Gaarder")`. Nå kan vi opprette to andre `Bok`-objekter:

`Bok("Beatles")`    
`Bok("Når villdyret våkner")`   

Tilsvarende kan vi opprette tre `Person`-objekter: 

`Person("Per Hansen")`   
`Person("Hilde Bakken")`   
`Person("Siv Larsen")`  

