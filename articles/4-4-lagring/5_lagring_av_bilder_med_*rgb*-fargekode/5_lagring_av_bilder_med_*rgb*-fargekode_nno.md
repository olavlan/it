---
title: "Lagring av bilete med *RGB*-fargekode"
belongs_to_chain: "Lagring av data"
figures_to_include:
	- "france_flag.svg"
	- "france_flag_rgb.svg"
	- "france_flag_bin.svg"
	- "unknown.svg"
---

I førre kapittel laga me våre eigne binære kodar for fargar, men det finst ein standardisert måte å gjera dette på, som tek utgangspunkt i at alle fargar kan lagast ved å blanda tre *primærfargar*. Rød, grøn og blå blir brukte som primærfargar, og derfor blir denne standarden kalla for *RGB*.

I [fargeveljaren](https://www.google.com/search?q=color%20selector) på *Google*  kan du velja kva farge som helst og sjå kva *RGB*-koden til fargen er. Utforsk gjerne fargeveljaren, til dømes ved å finna *RGB*-koden til følgjande fargar:
* Heilt kvitt
* Heilt svart
* Rød
* Grønn
* Blå
* Lilla
* Lysegrøn
* Mørkegrøn
* Oransje
* Brun
* Grå

Ein *RGB*-fargekode blir skriven på forma *(0-255*, *0-255*, *0-255)*, altså tre tal mellom 0 og 255. Det første talet fortel intensiteten av rød, og dei to neste tala er intensiteten av høvesvis grøn og blå. For å få ein heilt grøn farge bruker me derfor koden *(255, 0, 0)*. Me kan tenkja på svart som fråvær av farge, så koden  blir *(0, 0, 0)*. Motsett kan me tenkja på kvit som nærvær av alle fargar, altså *(255, 255, 255)*. Låge tal gir mørke fargar og høge tal gir lyse fargar. Ein mørk lilla farge kan me oppnå ved å blanda litt raud og blå, til dømes *(50, 0, 50)*.

Kvifor må tala vera mellom 0 og 255? La oss skriva desse tala med det binære talsystemet:

0: *0000 0000*   
255: *1111 1111*  

255 er altså det høgaste talet me kan skriva med 8 bitar! Tenk deg at me skal lagra fargen *(50, 100, 150)* på minnet til datamaskina. I det binære talsystemet blir *RGB*-koden *(00110010, 01100100, 10010110)*. Dette er ein bitsekvens som kan lagrast på minnet til datamaskina!


No tek me utgangspunkt i følgjande bilete, som har 6 pikslar:

<img src="/media/markdowncontent/assosiated_files/france_flag.svg">

For å lagra dette biletet på datamaskina, må me først skriva fargane med *RGB*-kode:

<img src="/media/markdowncontent/assosiated_files/france_flag_rgb.svg">

Sjekk gjerne at desse fargekodane stemmer med det me har lært om *RGB*! No kan me skriva tala med det binære talsystemet:

<img src="/media/markdowncontent/assosiated_files/france_flag_bin.svg">

No kan me lagra biletet som ein bitstreng:

```
0000 0000 	0101 0101	1010 0100
1111 1111	1111 1111	1111 1111
1110 1111	0100 0001	0011 0101
0000 0000 	0101 0101	1010 0100
1111 1111	1111 1111	1111 1111
1110 1111	0100 0001	0011 0101
```

Her har me skrive kvar piksel på ei linje, men eigentleg er dette ein sekvens av *0* og *1* utan linjeskift eller mellomrom.

Merk at me treng 8 bitar for å lagra mengda raud, og tilsvarande for grøn og blå. Til saman treng me altså $8\cdot 3 = 24$ bitar for å lagra fargen til éin piksel. Det er ganske mange bitar for berre éin piksel, men til gjengjeld gir det oss tilgang til veldig mange fargar! Kor mange? Sidan ein *RGB*-kode er på forma *(0-255*, *0-255*, *0-255)*, kan me velja mellom 256 verdiar i kvar av dei tre komponentane. Talet på kombinasjonar blir då

$$256\cdot 256 \cdot 256 = 16777216,$$

altså nesten 17 millionar fargar!

24-bits *RGB*-fargekodar blir brukte av nesten alle datamaskiner, nettbrett og smarttelefonar, og i nesten alle biletformat. [Denne](https://en.wikipedia.org/wiki/color_depth#Comparison) samanlikninga viser at me kanskje kunne brukt færre bitar, ettersom det menneskelege auget ikkje kan skilja mellom så mange ulike fargar!

**Aktivitetsforslag 1.** Me har lagra eit bilete med følgjande bitsekvens:

```
0000 0000	1000 1100	0100 0101
1111 0100	1111 0101	1111 0000
1100 1101	0010 0001	0010 1010
0000 0000	1000 1100	0100 0101
1111 0100	1111 0101	1111 0000
1100 1101	0010 0001	0010 1010
```

Dimensjonen til biletet er $3 \times 2$ pikslar, og du skal finna fargen i kvar piksel:

<img src="/media/markdowncontent/assosiated_files/unknown.svg">

Biletet er lagra med *RGB*-kode, det vil seia at kvar piksel inneheld $3\cdot 8 = 24$ bit med data. Den første pikselen er øvst til venstre til venstre i biletet, og dei neste pikslane er registrerte etter vanleg leseretning.

Finn *RGB*-koden som høyrer til kvar piksel, og bruk deretter [fargeveljaren](https://www.google.com/search?q=color%20selector)  i *Google* til å fargeleggja pikslane (du kan skriva inn din eigen verdi i feltet *RGB*). Kva viser biletet?

**Aktivitetsforslag 2.** Finn eit enkelt bilete som du kan teikna med nokre få pikslar, til dømes eit flagg. Fargelegg kvar piksel, og bruk [fargeveljaren](https://www.google.com/search?q=color%20selector)  i *Google* til å finna *RGB*-kodar som er mest mogleg lik kvar farge. Oversett *RGB*-tala til binære tal og skriv biletet som ein bitstreng.

