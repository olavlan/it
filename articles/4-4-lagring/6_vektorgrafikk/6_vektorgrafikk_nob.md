---
title: "Vektorgrafikk"
belongs_to_chain: "Lagring av data"
figures_to_include:
	- "circle-cross.svg"
---

Når et *JPEG*-forstørres nok, vil man til slutt se pikslene. Men du har kanskje sett bilder som aldri blir uskarpe, uansett hvor mye man forstørrer det? Dersom du ikke har sett slike bilder, kan du finne eksempler på [SVG Repo](https://www.svgrepo.com/). Her kan du søke etter illustrasjoner av hva som helst, og du kan forsøke å forstørre bildene så mye du vil for å se at de ikke blir uskarpe. 

Bildene på denne nettsiden har formatet *SVG*, som står for *Scalable Vector Graphics*. Når du lagrer et slikt bilde på datamaskinen, vil det **ikke** lagres som en sekvens av piksler. I stedet er det de geometriske objektene i bildet som lagres, og det er først når du åpner bildet at datamaskinen "tegner" de geometriske objektene som piksler. Når du forstørrer bildet, vil de geometriske objektene tegnes på nytt, men denne gangen større. Denne måten å lagre og tegne bilder på kalles *vektorgrafikk*.

Du lurer kanskje på hvordan man lagrer et geometrisk objekt? Gå inn på [Geogebra](https://www.geogebra.org/classic?lang=no) og forsøk å tegne noen figurer. Hvilke data må du lagre for å kunne tegne de samme figurene igjen senere? 

* For å tegne et bestemt linjestykke, trenger vi kun å lagre endepunktene.
* For å tegne en bestemt sirkel, trenger vi kun å lagre sentrum og radius.

Her er et enkelt eksempel på et *SVG*-bilde: 

<img src="/media/markdowncontent/assosiated_files/circle-cross.svg">

Dette bildet kan lagres med følgende *SVG*-kode: 

```xml
<svg>
  <circle cx="50" cy="50" r="50" fill="white" stroke="black" />
  <line x1="50" y1="0" x2="50" y2="100" stroke="black" />
  <line x1="0" y1="50" x2="100" y2="50" stroke="black" />
</svg>
```
Ser du hva de ulike verdiene betyr? Du kan gå inn på [*SVG Viewer*](https://www.svgviewer.dev/s/fpQJVmYj) og forsøke å endre noen av verdiene for å se hva som skjer!

Denne *SVG*-koden kan oversettes til en bitstreng og deretter lagres på datamaskinen. Som du kan tenke deg, vil disse kodelinjene ikke ta mye lagringsplass! Dersom vi i stedet hadde lagret bildet med piksler, for eksempel med dimensjonen $100\times 100$, ville det tatt mye mer plass! Dessuten ville sirkelen blitt uskarp ved forstørring. 

Bokstavene du nå leser er tegnet med vektorgrafikk, slik at du kan forstørre teksten uten at det blir uskarpt! [Her](https://www.geogebra.org/m/fJHKHWuR) kan du se hvordan bokstaven *r* kan tegnes (du må dra $t$-parameteren frem og tilbake). For å tegne bokstaver holder det ikke med linjestykker og sirkler, vi trenger mer kompliserte kurver. Men i prinsippet trenger vi bare å lagre *kontrollpunktene*, altså punktene som bestemmer hvordan kurvene skal tegnes. Se gjerne hvordan kurvene endrer seg når du flytter kontrollpunktene, for eksempel punktene $M_1$, $N_1$, $R_1$ og $S_1$. 

Som oppsummering kan vi si at vektorgrafikk alltid bør brukes for grafiske illustrasjoner som er tegnet med jevne kurver. Eksempler på dette er ikoner, logoer, flagg, bokstaver og andre tegn. Vektorgrafikk sparer lagringsplass og gjør at bildet aldri blir uskarpt ved forstørring. 

En annen viktig fordel med vektorgrafikk er at vi kan effektivt *tegne med programmering*! Kort sagt kan vi skrive kode som genererer diagrammer eller andre illustrasjoner. Dersom du synes dette virker spennende og ønsker å lære mer, kan du lese mer i neste seksjon.

Til slutt kan det nevnes at *SVG* også kan brukes til å lage jevne animasjoner! I følgende eksempel endrer vi radiusen til en sirkel: 

```xml
<svg height="100" width="100">
  <circle cy="50" cx="50">
     <animate
      attributeName="r"
      values="0;50;0"
      dur="10s"
      repeatCount="indefinite" />
  </circle>
</svg>
```
Lim denne koden inn i [*SVG Viewer*](https://www.svgviewer.dev/s/LfxtOdK1) for å se hva som skjer! Du kan også forsøke å endre på noen av verdiene i animasjonen.

Legg merke til hvor lite data som kreves for å lage denne animasjonen. Tenk deg hvor mye plass det ville tatt hvis vi skulle lagret animasjonen som en sekvens av *JPEG*-bilder i stedet!


**Aktivitetsforslag 1.** I neste seksjon skal vi se at en farge vanligvis lagres med 24 bits, så i denne oppgaven kan du anta at en piksel lagres med 24 bits. 

Tenk deg at du ønsker å lagre symbolet ❌ som et bilde med $500 \times 500$ piksler. Hvor mange bits trenger vi for å lagre bildet som piksler? 

Tenk deg at du i stedet vil lagre bildet med geometriske objekter. Tegn først figuren i [Geogebra](https://www.geogebra.org/classic?lang=no). Hvor mange geometriske  objekter trenger du? Hvilke data må vi lagre om hvert av objektene for å kunne tegne det på nytt senere? Kan du anslå hvor mange bits du trenger for å lagre disse dataene? Du kan anta at et tall lagres med 64 bits på en moderne datamaskin. 

Hva er forskjellen på å lagre ❌ som punktgrafikk og vektorgrafikk?

**Aktivitetsforslag 2.** Tegn en figur i [Geogebra](https://www.geogebra.org/classic?lang=no). Gå deretter til menyvalget "Last ned som...", og last ned både som *SVG* og som *PNG*. Sammenlign filstørrelsen til hver av bildene, og forsøk å forstørre opp begge bildene. Hva kan du si om de to formatene? 

