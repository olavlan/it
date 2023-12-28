---
title: "Metodar og meldingar"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasser_med_navn.svg"
---

I dei ulike klassane har me definert datafelt og handlingar:

<img src="/media/markdowncontent/assosiated_files/klasser_med_navn.svg" width="300">

Merk at datafelta kjem øvst, deretter handlingane, og at me skil datafelta og handlingane med ei linje.

Handlingar, altså ting me kan gjera med objekt, blir vanlegvis kalla *metodar*. Me kan seia følgjande om `Bok`-klassen:

- Klassen har datafelta `tittel`, `forfatter`og `sideantall`, og metodane `lån_ut(person)` og `lever_inn()`.
- Me kan bruka klassen til å oppretta `Bok`-objekt. Kvart objekt får datafelta og metodane som er definerte i klassen. Deretter kan datafelta fyllast med verdiar, og metodane behandlar desse verdiane.

Me kan be eit objekt om å utføra ein av metodane sine. Det blir kalla å *senda ei melding* til objektet.

- Viss me vil registrera innlevering av boka *Sofies verd*, må me senda ei melding til objektet`Bok("Sofies verden")`. Meir spesifikt må me be objektet om å utføra metoden `lever_inn()`.
- Viss me ønskjer at Per Hansen skal få ei tilråding, må me be objektet `Person("Per Hansen")` om å utføra metoden `få_anbefaling()`. Metoden behandlar verdiane i objektet og gir eit svar tilbake (*førebels finst ingen relevante verdiar å behandla, men seinare kan me leggja til datafelt som `interesser` og `favorittkategori` i `Person`-klassen*).

