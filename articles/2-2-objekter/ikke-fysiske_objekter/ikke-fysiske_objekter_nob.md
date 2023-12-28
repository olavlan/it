---
title: "Ikke-fysiske objekter"
belongs_to_chain: "Hva er objekter?"
figures_to_include:
	- "modell_bokhylle.svg"
	- "modell_utlaan.svg"
	- "modell_boksamling.svg"
---

Vi kan vurdere å inkludere andre objekter i modellen over vår boksamling. Kanskje vil vi at programmet skal holde orden på bokhyller, for å hjelpe oss å finne igjen og organisere bøker. Da er en bokhylle et relevant objekt:

- En bokhylle har egenskaper, nemlig hvilke bøker og bokkategorier den inneholder, samt kapasitet. 
- En bokhylle har handlinger,  for eksempel “Legg til bok”, “Fjern bok” og “Vis boktitler”. 

Vi kan nå utvide modellen (det røde objektet er en bokhylle): 

<img src="/media/markdowncontent/assosiated_files/modell_bokhylle.svg" width="500">

Er dette alle relevante objekter? Hvis vi kun vurderer fysiske objekter, er svaret kanskje ja. Men når vi programmerer, trenger ikke objektene å være fysiske ting. For eksempel, når vi låner en bok på biblioteket, blir det registrert et utlån. Et utlån er ikke noe vi kan ta og føle på, men det er likevel et relevant objekt: 

- Et utlån har egenskaper, nemlig hvilken bok og person det gjelder, samt startdato og frist for innlevering. 
- Et utlån har handlinger, for eksempel “Forleng lånetid”.

Hvis vi legger til utlån i modellen, får vi følgende diagram (det gule objektet er et utlån):

<img src="/media/markdowncontent/assosiated_files/modell_utlaan.svg" width="500">

Koblingene viser at et utlån knyttes til en person og en bok. 

Har vi nå inkludert alle relevante objekter? For å svare på det, bør vi gå tilbake til kravspesifikasjonen, og sjekke om vi mangler noen handlinger. Vi ønsket jo for eksempel å søke etter ledige bøker. Hvilket objekt gjøres denne handlingen på? På hele boksamlingen! Dette er et relevant objekt: 

- En boksamling har egenskaper, nemlig hvilke bokhyller og bøker den inneholder. 
- En boksamling har handlinger, for eksempel “Søk etter ledig bok” eller “Vis ledige bøker”. 

Hvis vi legger til dette objektet, får vi følgende diagram (det oransje objektet er en boksamling): 

<img src="/media/markdowncontent/assosiated_files/modell_boksamling.svg" width="500">

Som vist i diagrammet, kan en boksamling godt inneholde flere bokhyller. 

