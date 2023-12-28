---
title: "Vektorgrafikk"
belongs_to_chain: "Lagring av data"
figures_to_include:
	- "circle-cross.svg"
---

Når eit *JPEG*-blir nok forstørra, vil ein til slutt sjå pikslane. Men du har kanskje sett bilete som aldri blir uskarpe, same kor mykje ein forstørrar det? Dersom du ikkje har sett slike bilete, kan du finna døme på [SVG Repo](https://www.svgrepo.com/). Her kan du søkja etter illustrasjonar av kva som helst, og du kan prøva å forstørra bileta så mykje du vil for å sjå at dei ikkje blir uskarpe.

Bileta på denne nettsida har formatet *SVG*, som står for *Scalable Vector Graphics*. Når du lagrar eit slikt bilete på datamaskina, vil det **ikkje** lagrast som ein sekvens av pikslar. I staden er det dei geometriske objekta i biletet som blir lagra, og det er først når du opnar biletet at datamaskina "teiknar" dei geometriske objekta som pikslar. Når du forstørrar biletet, vil dei geometriske objekta teiknast på nytt, men denne gongen større. Denne måten å lagra og teikna bilete på blir kalla *vektorgrafikk*.

Du lurer kanskje på korleis ein lagrar eit geometrisk objekt? Gå inn på [Geogebra](https://www.geogebra.org/classic?lang=no) og forsøk å teikna nokre figurar. Kva data må du lagra for å kunna teikna dei same figurane igjen seinare?

* For å teikna eit bestemt linjestykke, treng me berre å lagra endepunkta.
* For å teikna ein bestemd sirkel, treng me berre å lagra sentrum og radius.

Her er eit enkelt døme på eit *SVG*-bilete:

<img src="/media/markdowncontent/assosiated_files/circle-cross.svg">

Dette biletet kan lagrast med  *følgjande *SVG*-kode:

```xml
<svg>
  <circle cx="50" cy="50" r="50" fill="white" stroke="black" />
  <line x1="50" y1="0" x2="50" y2="100" stroke="black" />
  <line x1="0" y1="50" x2="100" y2="50" stroke="black" />
</svg>
```
Ser du kva dei ulike verdiane betyr? Du kan gå inn på [*SVG Viewer*](https://www.svgviewer.dev/s/fpQJVmYj) og prøva å endra nokre av verdiane for å sjå kva som skjer!

Denne *SVG*-koden kan omsetjast til ein bitstreng og deretter blir lagra på datamaskina. Som du kan tenkja deg, vil desse kodelinjene ikkje ta mykje lagringsplass! Dersom me i staden hadde lagra biletet med pikslar, til dømes med dimensjonen $100\times 100$, ville det teke mykje meir plass! Dessutan ville sirkelen vorte uskarp ved forstørring.

Bokstavane du no lesar er teikna med vektorgrafikk, slik at du kan forstørra teksten utan at det blir uskarpt! [Her](https://www.geogebra.org/m/fjhkhwur) kan du sjå korleis bokstaven *r* kan teiknast (du må dra $t$-parameteren fram og tilbake). For å teikna bokstavar held det ikkje med linjestykke og sirklar, me treng meir kompliserte korger. Men i prinsippet treng me berre å lagra *kontrollpunkta*, altså punkta som bestemmer korleis korgene skal teiknast. Sjå gjerne korleis korgene endrar seg når du flyttar kontrollpunkta, til dømes punkta $M_1$, $N_1$, $R_1$ og $S_1$.

Som oppsummering kan me seia at vektorgrafikk alltid bør brukast for grafiske illustrasjonar som er teikna med jamne korger. Døme på dette er ikon, logoar, flagg, bokstavar og andre teikn. Vektorgrafikk sparer lagringsplass og gjer at biletet aldri blir uskarpt ved forstørring.

Ein annan viktig fordel med vektorgrafikk er at me kan effektivt *teikna med programmering*! Kort sagt kan me skriva kode som genererer diagram eller andre illustrasjonar. Dersom du synest dette verkar spennande og ønskjer å læra meir, kan du lesa meir i neste seksjon.

Til slutt kan det nemnast at *SVG* også kan brukast til å laga jamne animasjonar! I følgjande døme endrar me radiusen til ein sirkel:

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
Lim denne koden inn i [*SVG Viewer*](https://www.svgviewer.dev/s/LfxtOdK1) for å sjå kva som skjer! Du kan også prøva å endra på nokre av verdiane i animasjonen.

Legg merke til kor lite data som trengst for å laga denne animasjonen. Tenk deg kor mykje plass det ville teke viss me skulle lagra animasjonen som ein sekvens av *JPEG*-bilete i staden!


**Aktivitetsforslag 1.** I neste seksjon skal me sjå at ein farge vanlegvis blir lagra med 24 bitar, så i denne oppgåva kan du rekna med at ein piksel blir lagra med 24 bitar.

Tenk deg at du ønskjer å lagra symbolet ❌ som eit bilete med $500 \times 500$ pikslar. Kor mange bitar treng me for å lagra biletet som pikslar?

Tenk deg at du i staden vil lagra biletet med geometriske objekt. Teikn først figuren i [Geogebra](https://www.geogebra.org/classic?lang=no). Kor mange geometriske  objekt treng du? Kva data må me lagra om kvart av objekta for å kunna teikna det på nytt seinare? Kan du anslå kor mange bitar du treng for å lagra desse dataa? Du kan rekna med at eit tal blir lagra med 64 bitar på ei moderne datamaskin.

Kva er forskjellen på å lagra ❌ som punktgrafikk og vektorgrafikk?

**Aktivitetsforslag 2.** Teikn ein figur i [Geogebra](https://www.geogebra.org/classic?lang=no). Gå deretter til menyvalet "Last ned som...", og last ned både som *SVG* og som *PNG*. Samanlikn filstorleiken til kvart av bileta, og prøv å forstørra opp begge bileta. Kva kan du seia om dei to formata?

