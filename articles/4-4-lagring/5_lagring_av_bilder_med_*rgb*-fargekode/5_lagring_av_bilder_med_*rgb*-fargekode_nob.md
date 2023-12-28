---
title: "Lagring av bilder med *RGB*-fargekode"
belongs_to_chain: "Lagring av data"
figures_to_include:
	- "france_flag.svg"
	- "france_flag_rgb.svg"
	- "france_flag_bin.svg"
	- "unknown.svg"
---

I forrige kapittel lagde vi våre egne binære koder for farger, men det finnes en standardisert måte å gjøre dette på, som tar utgangspunkt i at alle farger kan lages ved å blande tre *primærfarger*. Rød, grønn og blå brukes som primærfarger, og derfor kalles denne standarden for *RGB*. 

I [fargevelgeren](https://www.google.com/search?q=color%20selector) på *Google*  kan du velge en hvilken som helst farge og se hva *RGB*-koden til fargen er. Utforsk gjerne fargevelgeren, for eksempel ved å finne *RGB*-koden til følgende farger:
* Helt hvitt
* Helt svart
* Rød
* Grønn
* Blå
* Lilla
* Lysegrønn
* Mørkegrønn
* Oransje
* Brun
* Grå

En *RGB*-fargekode skrives på formen *(0-255*, *0-255*, *0-255)*, altså tre tall mellom 0 og 255. Det første tallet forteller intensiteten av rød, og de to neste tallene er intensiteten av henholdsvis grønn og blå. For å få en helt grønn farge bruker vi derfor koden *(255, 0, 0)*. Vi kan tenke på svart som fravær av farge, så koden  blir *(0, 0, 0)*. Motsatt kan vi tenke på hvit som tilstedeværelse av alle farger, altså *(255, 255, 255)*. Lave tall gir mørke farger og høye tall gir lyse farger. En mørk lilla farge kan vi oppnå ved å blande litt rød og blå, for eksempel *(50, 0, 50)*.

Hvorfor må tallene være mellom 0 og 255? La oss skrive disse tallene med det binære tallsystemet: 

0: *0000 0000*   
255: *1111 1111*  

255 er altså det høyeste tallet vi kan skrive med 8 bit! Tenk deg at vi skal lagre fargen *(50, 100, 150)* på datamaskinens minne. I det binære tallsystemet blir *RGB*-koden *(00110010, 01100100, 10010110)*. Dette er en bitsekvens som kan lagres på datamaskinens minne! 


Nå tar vi utgangspunkt i følgende bilde, som har 6 piksler:

<img src="/media/markdowncontent/assosiated_files/france_flag.svg">

For å lagre dette bildet på datamaskinen, må vi først skrive fargene med *RGB*-kode: 

<img src="/media/markdowncontent/assosiated_files/france_flag_rgb.svg">

Sjekk gjerne at disse fargekodene stemmer med det vi har lært om *RGB*! Nå kan vi skrive tallene med det binære tallsystemet: 

<img src="/media/markdowncontent/assosiated_files/france_flag_bin.svg">

Nå kan vi lagre bildet som en bitstreng: 

```
0000 0000 	0101 0101	1010 0100
1111 1111	1111 1111	1111 1111
1110 1111	0100 0001	0011 0101
0000 0000 	0101 0101	1010 0100
1111 1111	1111 1111	1111 1111
1110 1111	0100 0001	0011 0101
```

Her har vi skrevet hver piksel på en linje, men egentlig er dette en sekvens av *0* og *1* uten linjeskift eller mellomrom. 

Merk at vi trenger 8 bit for å lagre mengden rød, og tilsvarende for grønn og blå. Til sammen trenger vi altså $8\cdot 3 = 24$ bits for å lagre fargen til én piksel. Det er ganske mange bits for bare én piksel, men til gjengjeld gir det oss tilgang til veldig mange farger! Hvor mange? Siden en *RGB*-kode er på formen *(0-255*, *0-255*, *0-255)*, kan vi velge mellom 256 verdier i hver av de tre komponentene. Antall kombinasjoner blir da

$$256\cdot 256 \cdot 256 = 16777216,$$

altså nesten 17 millioner farger! 

24-bits *RGB*-fargekoder brukes av nesten alle datamaskiner, nettbrett og smarttelefoner, og i nesten alle bildeformater. [Denne](https://en.wikipedia.org/wiki/Color_depth#Comparison) sammenligningen viser at vi kanskje kunne brukt færre bits, ettersom det menneskelige øyet ikke kan skille mellom så mange forskjellige farger!

**Aktivitetsforslag 1.** Vi har lagret et bilde med følgende bitsekvens:

```
0000 0000	1000 1100	0100 0101
1111 0100	1111 0101	1111 0000
1100 1101	0010 0001	0010 1010
0000 0000	1000 1100	0100 0101
1111 0100	1111 0101	1111 0000
1100 1101	0010 0001	0010 1010
```

Dimensjonen til bildet er $3 \times 2$ piksler, og du skal finne fargen i hver piksel:

<img src="/media/markdowncontent/assosiated_files/unknown.svg">

Bildet er lagret med *RGB*-kode, det vil si at hver piksel inneholder $3\cdot 8 = 24$ bit med data. Den første pikselen er øverst til venstre til venstre i bildet, og de neste pikslene er registrert etter vanlig leseretning. 

Finn *RGB*-koden som hører til hver piksel, og bruk deretter [fargevelgeren](https://www.google.com/search?q=color%20selector)  i *Google* til å fargelegge pikslene (du kan skrive inn din egen verdi i feltet *RGB*). Hva viser bildet?

**Aktivitetsforslag 2.** Finn et enkelt bilde som du kan tegne med noen få piksler, for eksempel et flagg. Fargelegg hver piksel, og bruk [fargevelgeren](https://www.google.com/search?q=color%20selector)  i *Google* til å finne *RGB*-koder som er mest mulig lik hver farge. Oversett *RGB*-tallene til binære tall og skriv bildet som en bitstreng. 

