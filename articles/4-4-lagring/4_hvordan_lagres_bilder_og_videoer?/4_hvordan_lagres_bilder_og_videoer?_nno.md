---
title: "Korleis blir bilete og videoar lagra?"
belongs_to_chain: "Lagring av data"
figures_to_include:
	- "rainbow.svg"
	- "colors.svg"
	- "colors_coded.svg"
	- "rainbow_coded.svg"
---

Når me ser eit fotografert bilete på ein skjerm, ser me eigentleg på eit stort rutenett der kvar av rutene har ein farge. Eit døme er:

<img src="/media/markdowncontent/assosiated_files/rainbow.svg">

På eit *JPEG*-bilete med høg oppløysing er rutene så små at me ikkje kan sjå dei, men dersom du zoomar nok inn på eit bilete, vil du til slutt sjå dei einsfarga rutene. Desse blir kalla *pikslar*. Biletet over har 130 pikslar; det er 13 pikslar breitt og 10 pikslar høgt, så me kan seia at det har ein *dimensjon* på $13\times 10$ pikslar.

Korleis kan me lagra dette biletet på ei datamaskin? Prinsippet er ganske enkelt, for me treng berre å lagra alle pikslane som ein sekvens. Først må me gi ein binær kode til kvar farge som kan finnast i biletet. Biletet vårt består av følgjande fargar:

<img src="/media/markdowncontent/assosiated_files/colors.svg">

Sidan det er åtte fargar, treng me åtte binære kodar:

<img src="/media/markdowncontent/assosiated_files/colors_coded.svg">

No kan me skriva kvar piksel som ein binær kode:

<img src="/media/markdowncontent/assosiated_files/rainbow_coded.svg">

For å skriva dette som ein sekvens av teikn, altså ein bitstreng, kan me starta på pikselen øvst til venstre, og følgjer den same retninga som me ville lese ei bok.

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

Her har me teke med mellomrom og linjeskift for presentasjonen sin del, men hugs at dette eigentleg er ein sekvens som berre består av *0* og *1*! Denne sekvensen kan lagrast på ei datamaskin! Deretter kan biletet attskapast på ein skjerm, men det krevst litt ekstra informasjon. Datamaskina må nemleg vita korleis kodane skal omsetjast til fargar, og kor lange radene i biletet skal vera.

I denne seksjonen har me laget våre eigne fargekodar, men han gir oss berre høvet til å bruka ni fargar. I neste seksjon skal me sjå på korleis me kan få tilgang til over 16. millionar fargar ved å bruka *RGB*-fargekodar.

**Videoar.** Når me forstår korleis bilete blir lagra, så er det ikkje vanskeleg å forstå korleis ein video kan lagrast. Ein video er nemleg berre ein veldig rask sekvens av bilete!

