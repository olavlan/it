---
title: "Flytdiagram"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "flytdiagram_bokvurdering.svg"
---

Metoden `regn_ut_gjennomsnittsvurdering()` fra forrige seksjon utfører flere steg for å regne ut en gjennomsnittvurdering av en bok. Vi kan vise disse stegene i et *flytdiagram*: 

<img src="/media/markdowncontent/assosiated_files/flytdiagram_bokvurdering.svg" width="1000">

Dette ser kanskje komplisert ut, men vi trenger ikke å vite mye for å forstå et slikt diagram. Vi begynner med å forklare de ulike blokkene:

1. I den grønne delen finner vi gjennomsnittet av lånetakernes vurderinger.
2. I den blå delen finner vi gjennomsnittet av brukervurderinger på nett.
3. I den lilla delen finner vi gjennomsnittet fra litteraturanmeldelser på nett.
4. I den røde delen regner vi ut det endelige gjennomsnittet.

Slik fargelegging er ikke nødvendig, men gjør det lettere å forstå helheten. Merk også hvordan vi kan plassere boksene slik at diagrammet blir mer oversiktlig.  

Nå må vi vite hva de ulike boksene betyr. I vårt eksempel har vi fire typer bokser: 

- **Sirkel/ellipse** markerer start og slutt på metoden.
- **Rektangel** er en operasjon, for eksempel en metode.
- **Parallellogram** er data. I vårt eksempel kommer disse før og etter metoder, for å vise inndata og utdata til metodene. 
- **Diamant** er et valg. Basert på valget bestemmes videre rute i flytdiagrammet. 
	- I vårt flytdiagram har vi én valgboks. Merk at den lilla delen av flytdiagrammet bare utføres hvis vi svarer "Ja" på valgboksen. 
	- Vi kan velge selv hva som skal være alternativene i en valgboks. Det må ikke være "Ja" og "Nei", og det kan være flere enn to alternativer.
	
Det finnes andre typer bokser, men med disse boksene kan vi tegne flytdiagram for de fleste metoder. 

