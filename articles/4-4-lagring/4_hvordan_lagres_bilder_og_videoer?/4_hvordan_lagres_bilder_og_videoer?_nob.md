---
title: "Hvordan lagres bilder og videoer?"
belongs_to_chain: "Lagring av data"
figures_to_include:
	- "rainbow.svg"
	- "colors.svg"
	- "colors_coded.svg"
	- "rainbow_coded.svg"
---

Når vi ser et fotografert bilde på en skjerm, ser vi egentlig på et stort rutenett der hver av rutene har en farge. Et eksempel er: 

<img src="/media/markdowncontent/assosiated_files/rainbow.svg">

På et *JPEG*-bilde med høy oppløsning er rutene så små at vi ikke kan se dem, men dersom du zoomer nok inn på et bilde, vil du til slutt se de ensfargede rutene. Disse kalles *piksler*. Bildet over har 130 piksler; det er 13 piksler bredt og 10 piksler høyt, så vi kan si at det har en *dimensjon* på $13\times 10$ piksler. 

Hvordan kan vi lagre dette bildet på en datamaskin? Prinsippet er ganske enkelt, for vi trenger bare å lagre alle pikslene som en sekvens. Først må vi gi en binær kode til hver farge som kan forekomme i bildet. Vårt bilde består av følgende farger: 

<img src="/media/markdowncontent/assosiated_files/colors.svg">

Siden det er åtte farger, trenger vi åtte binære koder:

<img src="/media/markdowncontent/assosiated_files/colors_coded.svg">

Nå kan vi skrive hver piksel som en binær kode: 

<img src="/media/markdowncontent/assosiated_files/rainbow_coded.svg">

For å skrive dette som en sekvens av tegn, altså en bitstreng, kan vi starte på pikselen øverst til venstre, og følger den samme retningen som vi ville lest en bok.

```
000 000 000 000 000 000 000 000 000 000 000 000 000 
000 000 110 110 111 000 000 000 000 000 000 000 000 
000 110 110 110 110 111 001 001 001 000 000 000 000
000 000 001 001 010 010 010 010 010 001 001 000 000
000 001 001 010 011 011 011 011 011 010 001 001 000
000 001 010 011 011 100 100 100 011 011 010 001 000
000 001 010 011 100 100 101 100 100 011 010 001 000
000 001 010 011 100 101 000 101 100 011 010 001 000
000 001 010 110 110 111 000 101 100 011 010 001 000
000 000 110 110 110 110 111 000 000 000 000 000 000
```

Her har vi tatt med mellomrom og linjeskift for presentasjonen sin del, men husk at dette egentlig er en sekvens som kun består av *0* og *1*! Denne sekvensen kan lagres på en datamaskin! Deretter kan bildet gjenskapes på en skjerm, men det kreves litt ekstra informasjon. Datamaskinen må nemlig vite hvordan kodene skal oversettes til farger, og hvor lange radene i bildet skal være. 

I denne seksjonen har vi laget våre egne fargekoder, men den gir oss bare muligheten til å bruke ni farger. I neste seksjon skal vi se på hvordan vi kan få tilgang til over 16. millioner farger ved å bruke *RGB*-fargekoder. 

**Videoer.** Når vi forstår hvordan bilder lagres, så er det ikke vanskelig å forstå hvordan en video kan lagres. En video er nemlig bare en veldig rask sekvens av bilder! 

