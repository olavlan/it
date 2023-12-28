---
title: "Branches"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

Som nevnt i forrige seksjon, er *branches* (*grener* på norsk) en måte å teste ut nye idéer uten å påvirke hovedversjonen av programmet ditt. En branch er i utgangspunktet bare en kopi av alle filene i programmet. 

Branches er noe du vil se i et hvilket som helst *Github*-repository av en viss størrelse. Hvis du for eksempel går inn på prosjektet [Flask](https://github.com/pallets/flask), vil du se at det står *8 branches* like over listen av filer. Til venstre for dette står det *main*, som er hovedversjonen av programmet. Ved å trykke på *main*, vil du få opp en nedtrekksmeny der du kan velge en annen branch av programmet.

Hovedversjonen av et program er en branch som gjerne har navnet *master* eller *main*. Det er hovedversjonen vi først ser når vi går inn på et *Github*-repository, og som ofte er den mest stabile versjonen av programmet. Når man vil legge til ny funksjonalitet i et program, er det vanlig å opprette en ny branch, der man fritt kan endre og legge til kode. 

[Denne](https://docs.github.com/assets/cb-2058/mw-1440/images/help/branches/pr-retargeting-diagram1.webp) figuren viser at *main* er som stammen i et tre, mens andre branches er som grener. Figuren viser også et par andre ting: 
* Dersom man til slutt er fornøyd med endringene, kan man smelte en branch inn i hovedversjonen. Dette kalles en *merge*. I figuren skjer det for eksempel en merge av *feature1* inn i *main*. Hva skjer egentlig her? Hvis mulig, så vil alle endringene som ble gjort i *feature1* legges inn i *main*. Men merk at *main* også kan ha blitt endret i mellomtiden! Da kan ulike tilfeller oppstå:
    * Endringene i *feature1* og endringene i *main* er på forskjellige filer. Disse endringene kommer ikke i veien for hverandre, og man kan gjøre en merge.
    * En endring i *feature1* er på samme fil som en endring i *main*.
        * Dersom endringene er på ulike steder i filen, så kan man fortsatt gjøre en merge, fordi *Github* vil sørge for at begge endringene kommer med i filen.
        * Dersom endringen er på samme kodelinje, så vil *Github* varsle om at man har en konflikt, og at merge ikke kan skje! Da må man løse denne konflikten (endre koden) før man kan gjøre en merge.
* Legg merke til at branches kan opprettes oppå hverandre! Det kan for eksempel være aktuelt når man skal utvikle en ny versjon av et program. Da kan man opprette en branch som heter noe slikt som *v2.0*. Hvis den nye versjonen skal ha tre nye funksjoner, så kan *v2.0* ha tre nye branches. Etter hvert som  de nye funksjonene er klare, kan de smeltes inn i *v2.0*, og til slutt kan *v2.0* smeltes inn i hovedversjonen. 

Hva er poenget med branches? Det er flere viktige fordeler:
* Man får en **trygg** måte å teste ut nye idéer, legge til funksjonalitet eller fikse feil. Det er trygt fordi man ikke trenger å bekymre seg for å påvirke hovedversjonen av programmet, som gjerne skal holdes mest mulig stabil.
* Siden hver branch kan sees på som en versjon av programmet, kan man jobbe med flere versjoner samtidig, og til slutt bestemme seg for hvilke versjoner man vil smelte inn i den endelige utgaven. Dette gir **fleksibilitet** til å kode uten å gjøre noen forpliktende avgjørelser om hvordan det ferdige programmet skal være.
* Nye funksjoner kan **testes** på en branch før det settes inn i hovedversjonen. Brukere av programmet vil sette pris på at alle funksjonene i hovedversjonen er grundig testet.
* **Samarbeid**: Som vi skal se nærmere på i de neste seksjonene, gjør branches at flere personer kan jobbe samtidig på det samme prosjektet. Ved at hver person jobber på hver sin branch, unngår man å komme i veien for hverandre. Til slutt smeltes de ulike grenene sammen, og eventuelle konflikter løses.

Trygghet, fleksibilitet, testing og samarbeid er altså noen stikkord som beskriver hvorfor branches er så nyttig.

