---
title: "Problem som kan løysast med algoritmar"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
---

Kva typa problem kan løysast med ein algoritme? La oss tenkja på følgjande problem:

> Reparera sykkelen

Dette problemet er ikkje tydeleg definert. For kva sykkel er det snakk om? Kva er gale med sykkelen? Og når kan me regna sykkelen som "reparert"?

Ein måte å vera presise på, er å definera utgangspunktet og ønskte resultat:

> **Problem** *Reparere sykkel*
**Utgangspunkt:** Ein sykkel $S$ med punktert hjul.
**Ønskte resultat:** At sykkelen $S$ ikkje har nokon punkterte hjul.

Her har me definert problemet på ein måte som ikkje kan misforståast:

* Me har gitt namn til objektet som problemet handlar om, slik at me kan referera eintydig til objektet. Det er vanleg å bruka store bokstavar som namn på objekt.
* I staden for å definera kva verbet "reparera" betyr, har me gitt ei presis skildring av kva som er ønskt sluttresultat.

Merk at denne definisjonen ikkje seier noko om korleis problemet kan løysast. For å løysa eit problem må me laga ein algoritme som kan gjera om startsituasjonen til det ønskte resultatet.

Når me skriv ein slik algoritme, må me hugsa at $S$ kan vera kva sykkel som helst. Eit steg i algoritmen kan til dømes vera "ta av det punkterte hjulet på sykkelen $S$". Her er det viktig at steget fungerer på alle syklar, ikkje berre ein spesifikk sykkel!

Det kan finnast mange algoritmar for å løysa eit bestemt problem. For å løysa problemet *Reparere sykkel* kan éin algoritme vera å lappa dekt, medan ein annan algoritme kan vera å skifta dekt.

Som eit anna døme kan me gi ein definisjon av problemet "å vaska klede":

> **Problem** *Vaske klede*
**Utgangspunkt:** Ei mengd klede $K$ og eit skap $S$.
**Ønskte resultat:** At kleda $K$ er reine, tørre, brettet og lagde i skapet $S$.

Merk at dette problemet har fleire relevante objekt, og me har gitt namn til alle.

Her burde ein kanskje ha definert kva som trengst for å kalla eit klesplagg "reint", men sidan problemet skal løysast av menneske, kan me tillata oss å ikkje definera alle ord. Me må derimot vera heilt presise når me definerer problem som skal løysast av ei datamaskin, som er tema for neste seksjon!

**Aktivitetsforslag:** Tenk over ei oppgåve du gjer regelmessig, til dømes å laga matpakke eller skifte sengetøy. Kva problem står du ovanfor før du tek fatt på oppgåva? Skriv ein presis definisjon av problemet, altså kva som er utgangspunktet og kva som er ønskt resultat. Forsøk å gi namn til dei relevante objekta i problemet.

