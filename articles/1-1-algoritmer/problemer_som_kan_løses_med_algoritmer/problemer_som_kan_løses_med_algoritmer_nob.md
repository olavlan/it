---
title: "Problemer som kan løses med algoritmer"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
---

Hvilke type problemer kan løses med en algoritme? La oss tenke på følgende problem: 

> Reparere sykkelen

Dette problemet er ikke tydelig definert. For hvilken sykkel er det snakk om? Hva er galt med sykkelen? Og når kan vi regne sykkelen som "reparert"? 

En måte å være presise på, er å definere utgangspunktet og ønsket resultat:

> **Problem** *Reparere sykkel*   
**Utgangspunkt:** En sykkel $S$ med punktert hjul.    
**Ønsket resultat:** At sykkelen $S$ ikke har noen punkterte hjul. 

Her har vi definert problemet på en måte som ikke kan misforstås: 

* Vi har gitt navn til objektet som problemet handler om, slik at vi kan referere entydig til objektet. Det er vanlig å bruke store bokstaver som navn på objekter. 
* Istedenfor å definere hva verbet "reparere" betyr, har vi gitt en presis beskrivelse av hva som er ønsket sluttresultat. 

Merk at denne definisjonen ikke sier noe om hvordan problemet kan løses. For å løse et problem må vi lage en algoritme som kan gjøre om startsituasjonen til det ønskede resultatet.

Når vi skriver en slik algoritme, må vi huske at $S$ kan være en hvilken som helst sykkel. Et steg i algoritmen kan for eksempel være "ta av det punkterte hjulet på sykkelen $S$". Her er det viktig at steget fungerer på alle sykler, ikke bare en spesifikk sykkel!

Det kan finnes mange algoritmer for å løse et bestemt problem. For å løse problemet *Reparere sykkel* kan én algoritme være å lappe dekket, mens en annen algoritme kan være å skifte dekket. 

Som et annet eksempel kan vi gi en definisjon av problemet "å vaske klær":

> **Problem** *Vaske klær*    
**Utgangspunkt:** En mengde klær $K$ og et skap $S$.   
**Ønsket resultat:** At klærne $K$ er rene, tørre, brettet og lagt i skapet $S$.

Merk at dette problemet har flere relevante objekter, og vi har gitt navn til alle. 

Her burde man kanskje ha definert hva som kreves for å kalle et klesplagg "rent", men siden problemet skal løses av mennesker, kan vi tillate oss å ikke definere alle ord. Vi må derimot være helt presise når vi definerer problemer som skal løses av en datamaskin, som er tema for neste seksjon!

**Aktivitetsforslag:** Tenk over en oppgave du gjør regelmessig, for eksempel å lage matpakke eller skifte sengetøy. Hvilket problem står du ovenfor før du tar fatt på oppgaven? Skriv en presis definisjon av problemet, altså hva som er utgangspunktet og hva som er ønsket resultat. Forsøk å gi navn til de relevante objektene i problemet. 

