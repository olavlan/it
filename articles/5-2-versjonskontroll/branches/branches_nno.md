---
title: "Branches"
belongs_to_chain: "Versjonskontroll"
figures_to_include:
---

Som nemnt i førre seksjon, er *branches* (*greiner* på norsk) ein måte å testa ut nye idéer utan å påverka hovudversjonen av programmet ditt. Ein branch er i utgangspunktet berre ein kopi av alle filene i programmet.

Branches er noko du vil sjå i eit kva som helst *Github*-repository av ein viss storleik. Viss du til dømes går inn på prosjektet [Flask](https://github.com/pallets/flask), vil du sjå at det står *8 branches* like over lista av filer. Til venstre for dette står det *main*, som er hovudversjonen av programmet. Ved å trykkja på *main*, vil du få opp ein nedtrekkmeny der du kan velja ein annan branch av programmet.

Hovudversjonen av eit program er ein branch som gjerne har namnet *master* eller *main*. Det er hovudversjonen me først ser når me går inn på eit *Github*-repository, og som ofte er den mest stabile versjonen av programmet. Når ein vil leggja til ny funksjonalitet i eit program, er det vanleg å oppretta ein ny branch, der ein fritt kan endra og leggja til kode.

[Denne](https://docs.github.com/assets/cb-2058/mw-1440/images/help/branches/pr-retargeting-diagram1.webp) figuren viser at *main* er som stammen i eit tre, medan andre branches er som greinar. Figuren viser også eit par andre ting:
* Dersom ein til slutt er fornøgd med endringane, kan ein smelta ein branch inn i hovudversjonen. Dette blir kalla ein *merge*. I figuren skjer det til dømes ein merge av *feature1* inn i *main*. Kva skjer eigentleg her? Viss mogleg, så vil alle endringane som vart gjorde i *feature1* blir lagde inn i *main*. Men merk at *main* også kan ha vorte endra i mellomtida! Då kan ulike tilfelle oppstå:
* Endringane i *feature1* og endringane i *main* er på ulike filer. Desse endringane kjem ikkje i vegen for kvarandre, og ein kan gjera ein merge.
* Ei endring i *feature1* er på same fil som ei endring i *main*.
* Dersom endringane er på ulike stader i fila, så kan ein framleis gjera ein merge, fordi *Github* vil sørgja for at begge endringane kjem med i fila.
* Dersom endringa er på same kodelinje, så vil *Github* varsla om at ein har ein konflikt, og at merge ikkje kan skje! Då må ein løysa denne konflikten (endra koden) før ein kan gjera ein merge.
* Legg merke til at branches kan opprettast oppå kvarandre! Det kan til dømes vera aktuelt når ein skal utvikla ein ny versjon av eit program. Då kan ein oppretta ein branch som heiter noko slikt som *v2.0*. Viss den nye versjonen skal ha tre nye funksjonar, så kan *v2.0* ha tre nye branches. Etter kvart som  dei nye funksjonane er klare, kan dei smeltast inn i *v2.0*, og til slutt kan *v2.0* blir smelta inn i hovudversjonen.

Kva er poenget med branches? Det er fleire viktige fordelar:
* Ein får ein **trygg** måte å testa ut nye idéer, leggja til funksjonalitet eller fikse feil. Det er trygt fordi ein ikkje treng å bekymra seg for å påverka hovudversjonen av programmet, som gjerne skal haldast mest mogleg stabil.
* Sidan kvar branch kan sjåast på som ein versjon av programmet, kan ein jobba med fleire versjonar samtidig, og til slutt bestemma seg for kva versjonar ein vil smelta inn i den endelege utgåva. Dette gir **fleksibilitet** til å koda utan å gjera nokre forpliktande avgjerder om korleis det ferdige programmet skal vera.
* Nye funksjonar kan **testast** på ein branch før det blir sett inn i hovudversjonen. Brukarar av programmet vil setja pris på at alle funksjonane i hovudversjonen er grundig testa.
* **Samarbeid**: Som me skal sjå nærare på i dei neste seksjonane, gjer branches at fleire personar kan jobba samtidig på det same prosjektet. Ved at kvar person jobbar på kvar sin branch, unngår ein å komma i vegen for kvarandre. Til slutt blir dei ulike greinene smelta saman, og eventuelle konfliktar blir løyste.

Tryggleik, fleksibilitet, testing og samarbeid er altså nokre stikkord som beskriv kvifor branches er så nyttig.

