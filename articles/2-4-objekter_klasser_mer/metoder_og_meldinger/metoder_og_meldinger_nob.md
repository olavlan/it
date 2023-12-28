---
title: "Metoder og meldinger"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasser_med_navn.svg"
---

I de ulike klassene har vi definert datafelter og handlinger: 

<img src="/media/markdowncontent/assosiated_files/klasser_med_navn.svg" width="300">

Merk at datafeltene kommer øverst, deretter handlingene, og at vi skiller datafeltene og handlingene med en linje. 

Handlinger, altså ting vi kan gjøre med objekter, kalles vanligvis *metoder*. Vi kan si følgende om `Bok`-klassen: 

- Klassen har datafeltene `tittel`, `forfatter`og `sideantall`, og metodene `lån_ut(person)` og `lever_inn()`. 
- Vi kan bruke klassen til å opprette `Bok`-objekter. Hvert objekt får datafeltene og metodene som er definert i klassen. Deretter kan datafeltene fylles med verdier, og metodene behandler disse verdiene. 

Vi kan be et objekt om å utføre en av sine metoder. Det kalles å *sende en melding* til objektet.

- Hvis vi vil registrere innlevering av boka *Sofies verden*, må vi sende en melding til objektet`Bok("Sofies verden")`. Mer spesifikt må vi be objektet om å utføre metoden `lever_inn()`. 
- Hvis vi ønsker at Per Hansen skal få en anbefaling, må vi be objektet `Person("Per Hansen")` om å utføre metoden `få_anbefaling()`. Metoden behandler verdiene i objektet og gir et svar tilbake (*foreløpig finnes ingen relevante verdier å behandle, men senere kan vi legge til datafelter som `interesser` og `favorittkategori` i `Person`-klassen*).  

