---
title: "Objektdiagram og peikarar"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "objektdiagram_utlaan0.svg"
	- "objektdiagram_utlaan1.svg"
	- "objektdiagram_utlaan3.svg"
---

Me skal no visa ein nyttig måte å teikna objekt. Som døme opprettar me eit objekt frå kvar av klassane `Bok`, `Utlån` og `Person`:

<img src="/media/markdowncontent/assosiated_files/objektdiagram_utlaan0.svg" width="500">

Den nedste delen av figuren blir eit objektdiagram kalla, og er teikna på følgjande måte:

- Det første objektet har overskrifta `bok1: Bok`. Det betyr at variabelen med namn `bok1` held på objektet, og at datatypen til objektet er `Bok`. Dersom me ikkje ønskjer å ta med variabelnamn, kan me skriva `: Bok` i staden. Variabelnamn blir brukt eigentleg berre når me skal beskriva programkode:
	+ Når eit program blir køyrt, kan variabelen `bok1` halda på `Bok("Sofies verden")` på eit tidspunkt, men seinare halda på eit heilt anna objekt. Eit objektdiagram viser altså kva variablane inneheld på eit *spesifikt tidspunkt* under køyringa av programmet.
- Vi teiknar boksar for verdiane av objektet. Det første objektet har verdien `"Sofies verden"` på datafeltet `tittel`. Det er lov for eit objekt å mangla nokre verdiar, og dette blir vist med ein tom boks.

Tenk deg at Per Hansen nettopp har lånt boka *Sofies verd*. Korleis registrerer me dette i systemet? Det er tre ting me ønskjer å gjera:

1. Opprette eit `Utlån`-objekt som inneheld informasjon om utlånet.
2. Registrera utlånet i objektet `Person("Per Hansen")`.
3. Registrera utlånet i objektet `Bok("Sofies verden")`

I diagrammet ovanfor har me gjennomført det første steget, nemleg å oppretta eit `Utlån`-objekt, men førebels har objektet ingen verdiar. Kva verdi skal fyllast inn på datafeltet `bok`? For å spørja på ein annan måte, kva ønskjer du å få tilbake når du hentar denne verdien seinare? Det hadde ikkje vore så nyttig å berre få tittelen `"Sofies verden"`! Det du antakeleg ønskjer å få tilbake er objektet `Bok("Sofies verden")`, som er til venstre i diagrammet over. Korleis får me tak i dette objektet?

Ein stad i minnet til datamaskina ligg objektet `Bok("Sofies verden")`. For å kunna gjera operasjonar på objektet, må me fortelja datamaskina kvar i minnet det ligg. Korleis veit me det? Kvar gong me opprettar eit objekt, får me tildelt ei *minneadresse*, som gjer at me kan finna igjen objektet seinare. Me treng sjølvsagt ikkje å hugsa denne adressa når me kodar - faktisk er det slik at når me legg objektet i ein variabel, så er det minneadressa som blir lagra i variabelen! Formålet med variablar er derfor å ta vare på minneadresser, slik at me kan finna igjen objekta som me skal gjera operasjonar på!
 
Spørsmålet var altså kva me skal setja inn i datafeltet `bok` på `Utlån`-objektet. No veit me svaret - me skal setja inn minneadressa til objektet `Bok("Sofies verden")`. Dette blir vist med ei pil:

<img src="/media/markdowncontent/assosiated_files/objektdiagram_utlaan1.svg" width="500">

No blir det feil å seia at`Utlån`-objektet "inneheld" `Bok`-objektet. Me seier heller at `Utlån`-objektet har ein *peikar* til `Bok`-objektet. Slik fungerer det alltid - me set aldri eit objekt inn i eit anna objekt, men bruker peikarar slik at objekt kan finna kvarandre. No kan me sørgja for at både`Bok`-objektet og `Person`-objektet kan finna utlånet dei er ein del av:

<img src="/media/markdowncontent/assosiated_files/objektdiagram_utlaan3.svg" width="500">

Kan du sjå kva peikar som manglar i diagrammet ovanfor?

