---
title: "Ikke-fysiske objekt"
belongs_to_chain: "Hva er objekter?"
figures_to_include:
	- "modell_bokhylle.svg"
	- "modell_utlaan.svg"
	- "modell_boksamling.svg"
---

Me kan vurdera å inkludera andre objekt i modellen over boksamlinga vår. Kanskje vil me at programmet skal halda orden på bokhyller, for å hjelpa oss å finna igjen og organisera bøker. Då er ei bokhylle eit relevant objekt:

- Ei bokhylle har eigenskapar, nemleg kva bøker og bokkategoriar ho inneheld, og dessutan kapasitet.
- Ei bokhylle har handlingar,  til dømes “Legg til bok”, “Fjern bok” og “Vis boktitlar”.

Me kan no utvida modellen (det raude objektet er ei bokhylle):

<img src="/media/markdowncontent/assosiated_files/modell_bokhylle.svg" width="500">

Er dette alle relevante objekt? Viss me berre vurderer fysiske objekt, er svaret kanskje ja. Men når me programmerer, treng ikkje objekta å vera fysiske ting. Til dømes, når me låner ei bok på biblioteket, blir det registrert eit utlån. Eit utlån er ikkje noko me kan ta og kjenna på, men det er likevel eit relevant objekt:

- Eit utlån har eigenskapar, nemleg kva bok og person det gjeld, og dessutan startdato og frist for innlevering.
- Eit utlån har handlingar, til dømes “Forleng lånetid”.

Viss me legg til utlån i modellen, får me følgjande diagram (det gule objektet er eit utlån):

<img src="/media/markdowncontent/assosiated_files/modell_utlaan.svg" width="500">

Koplingane viser at eit utlån blir knytt til ein person og ei bok.

Har me no inkludert alle relevante objekt? For å svara på det, bør me gå tilbake til kravspesifikasjonen, og sjekka om me manglar nokre handlingar. Vi ønsket jo til dømes å søkja etter ledige bøker. Kva objekt blir gjort denne handlinga på? På heile boksamlinga! Dette er eit relevant objekt:

- Ei boksamling har eigenskapar, nemleg kva bokhyller og bøker ho inneheld.
- Ei boksamling har handlingar, til dømes “Søk etter ledig bok” eller “Vis ledige bøker”.

Viss me legg til dette objektet, får me følgjande diagram (det oransje objektet er ei boksamling):

<img src="/media/markdowncontent/assosiated_files/modell_boksamling.svg" width="500">

Som vist i diagrammet, kan ei boksamling godt innehalda fleire bokhyller.

