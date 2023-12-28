---
title: "Skrivemåte for objekt"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasser_med_navn.svg"
---

Frå førre kapittel har me følgjande klassediagram:

<img src="/media/markdowncontent/assosiated_files/klasser_med_navn.svg" width="300">

Dette er målar som me bruker til å oppretta objekt. Tenk deg at me har *Sofies verd* i bokhylla, og ønskjer å registrera boka i systemet. Då opprettar eit `Bok`-objekt og set inn rette verdiar.

I bokhylla har me altså ei fysisk bok, og i minnet til datamaskina har me eit objekt som representerer boka. I dei neste seksjonane vil det vera nyttig å skilja mellom desse tinga. For å snakka om objektet som ligg i minnet til datamaskina kan me derfor bruka følgjande skrivemåte:

`Bok("Sofies verden")`

Først seier me kva klasse objektet kjem frå, deretter skriv me dei viktigaste verdiane i parentesar. Dersom me ønskte å ta med forfattarnamnet, kunne me ha skrive `Bok("Sofies verden", "Jostein Gaarder")`. No kan me oppretta to andre `Bok`-objekt:

`Bok("Beatles")`
`Bok("Når villdyret våkner")`

Tilsvarande kan me oppretta tre `Person`-objekt:

`Person("Per Hansen")`
`Person("Hilde Bakken")`
`Person("Siv Larsen")`

