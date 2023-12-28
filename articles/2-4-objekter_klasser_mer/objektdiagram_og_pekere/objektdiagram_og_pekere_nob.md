---
title: "Objektdiagram og pekere"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "objektdiagram_utlaan0.svg"
	- "objektdiagram_utlaan1.svg"
	- "objektdiagram_utlaan3.svg"
---

Vi skal nå vise en nyttig måte å tegne objekter. Som eksempel oppretter vi et objekt fra hver av klassene `Bok`, `Utlån` og `Person`:

<img src="/media/markdowncontent/assosiated_files/objektdiagram_utlaan0.svg" width="500">

Den nederste delen av figuren kalles et objektdiagram, og er tegnet på følgende måte: 

- Det første objektet har overskriften `bok1: Bok`. Det betyr at variabelen med navn `bok1` holder på objektet, og at datatypen til objektet er `Bok`. Dersom vi ikke ønsker å ta med variabelnavn, kan vi skrive `: Bok` i stedet. Variabelnavn brukes egentlig bare når vi skal beskrive programkode:
	+ Når et program kjøres, kan variabelen `bok1` holde på `Bok("Sofies verden")` på et tidspunkt, men senere holde på et helt annet objekt. Et objektdiagram viser altså hva variablene inneholder på et *spesifikt tidspunkt* under kjøringen av programmet. 
- Vi tegner bokser for objektets verdier. Det første objektet har verdien `"Sofies verden"` på datafeltet `tittel`. Det er lov for et objekt å mangle noen verdier, og dette vises med en tom boks. 

Tenk deg at Per Hansen nettopp har lånt boka *Sofies verden*. Hvordan registrerer vi dette i systemet? Det er tre ting vi ønsker å gjøre: 

1. Opprette et `Utlån`-objekt som inneholder informasjon om utlånet. 
2. Registrere utlånet i objektet `Person("Per Hansen")`. 
3. Registrere utlånet i objektet `Bok("Sofies verden")` 

I diagrammet ovenfor har vi gjennomført det første steget, nemlig å opprette et `Utlån`-objekt, men foreløpig har objektet ingen verdier. Hvilken verdi skal fylles inn på datafeltet `bok`? For å spørre på en annen måte, hva ønsker du å få tilbake når du henter denne verdien senere? Det hadde ikke vært så nyttig å bare få tittelen `"Sofies verden"`! Det du antagelig ønsker å få tilbake er objektet `Bok("Sofies verden")`, som er til venstre i diagrammet over. Hvordan får vi tak i dette objektet?

Et sted i datamaskinens minne ligger objektet `Bok("Sofies verden")`. For å kunne gjøre operasjoner på objektet, må vi fortelle datamaskinen hvor i minnet det ligger. Hvordan vet vi det? Hver gang vi oppretter et objekt, får vi tildelt en *minneadresse*, som gjør at vi kan finne igjen objektet senere. Vi trenger selvfølgelig ikke å huske denne adressen når vi koder - faktisk er det slik at når vi legger objektet i en variabel, så er det minneadressen som lagres i variabelen! Hensikten med variabler er derfor å ta vare på minneadresser, slik at vi kan finne igjen objektene som vi skal gjøre operasjoner på!
 
Spørsmålet var altså hva vi skal sette inn i datafeltet `bok` på `Utlån`-objektet. Nå vet vi svaret - vi skal sette inn minneadressen til objektet `Bok("Sofies verden")`. Dette vises med en pil: 

<img src="/media/markdowncontent/assosiated_files/objektdiagram_utlaan1.svg" width="500">

Nå blir det feil å si at`Utlån`-objektet "inneholder" `Bok`-objektet. Vi sier heller at `Utlån`-objektet har en *peker* til `Bok`-objektet. Slik fungerer det alltid - vi setter aldri et objekt inn i et annet objekt, men bruker pekere slik at objekter kan finne hverandre. Nå kan vi sørge for at både`Bok`-objektet og `Person`-objektet kan finne utlånet de er en del av: 

 <img src="/media/markdowncontent/assosiated_files/objektdiagram_utlaan3.svg" width="500">

Kan du se hvilken peker som mangler i diagrammet ovenfor? 

