---
title: "Issues"
belongs_to_chain: "Samarbeid med Github"
figures_to_include:
---

Når du går inn på et repository på Github, vil du som regel se knappen *Issues*. Her kan hvem som helst opprette et såkalt *issue*, og som navnet tilsier er dette måten å rapportere om en feil i programmet. Som regel oppretter man også et issue for å foreslå ny funksjonalitet eller andre forbedringer av prosjektet. Listen over *issues* blir derfor en slags *todo*-liste for et repository. 

Issues og pull requests er tett knyttet sammen. Når man ønsker en spesifikk forbedring av et repository, er følgende prosess vanlig: 

1. Noen oppretter et issue der den ønskede forbedringen beskrives. Det kan være snakk om å fikse en feil, legge til ny funksjonalitet eller forbedre eksisterende kode.
2. Når man har opprettet et issue, er det her man diskuterer den ønskede forbedringen. Man kan diskutere spørsmål som:
    * Er forbedringen nødvendig? Passer forbedringen med prosjektets overordnede mål? Vil integrasjon med resten av koden bli komplisert? Bør andre forbedringer prioriteres først?
    * Kan man beskrive med ord hvordan forbedringen kan realiseres? Finnes alternative løsninger, og hvilken løsning er eventuelt best?
    * Hvor mye arbeid kreves? Hvilke deler av den eksisterende koden må endres? Hva kan man hente fra andre prosjekter? Hvem skal ta ansvar for forbedringen?
    * I tilfelle feil i programmet, når og hvordan oppstår feilen? Hvilke steg kan man gjøre for å reprodusere feilen på sin egen maskin? Hva betyr eventuelle feilmeldinger? Kan man identifisere hva som forårsaker feilen?
3. En person tar ansvar for forbedringen, og oppretter til slutt en pull request. En slik pull request har gjerne en *referanse* til et issue, og vice versa. I slike tilfeller kan vi si at en pull request *løser* et issue. 
4. Når en pull request er opprettet, er det her diskusjonen fortsetter. Koden som er foreslått går gjennom review, testing, diskusjoner og eventuelle forbedringer. Dersom alt er vellykket, kan koden til slutt smeltes inn i programmet.

Dersom et issue har gått gjennom alle disse stegene, blir det til slutt lukket. Et issue kan også lukkes hvis man blir enige om at forbedringen ikke skal realiseres (fordi den ikke er relevant eller ikke kan prioriteres). Et issue som hverken har blitt fullført eller avvist, er et *åpent* issue. Hvem som helst kan prøve å løse et åpent issue og deretter legge inn en pull request med den foreslåtte løsningen. 

Som konklusjon kan vi si at *Issues* gir en ryddig måte å planlegge enhver type forbedring i et repository, enten det er snakk om retting av en feil, ny funksjonalitet eller andre forbedringer av koden. Issues gir en oversikt over eksisterende oppgaver i et prosjekt, og legger til rette for samarbeid og kommunikasjon rundt disse. 

Listen over alle tidligere issues og pull requests fungerer som et arkiv over alle avgjørelser som har blitt tatt, og kan være en nyttig referanse i framtiden. 

**Aktivitet 1.** Finn noen prosjekter som interesserer deg ved å søke på *Github*. Trykk deretter på *Issues*, og gå inn på noen issues. Finn ut av følgende:
* Hvilken informasjon må tas med i et issue? Følges alltid en bestemt mal? Varierer dette fra prosjekt til prosjekt? 
* Bruk nedtrekksmenyen *Label* til å finne issues med forskjellige merkelapper. Finn minst et issue som registrerer en feil (*bug*) og et issue som foreslår ny funksjonalitet. Brukes forskjellige maler til å registrere ulike typer issues?
    * Prøv gjerne å finne merkelappen *good first issues*, som betyr at forbedringen er relativt enkel å realisere. Dette er en god måte å finne ut hvor man kan gjøre sitt første bidrag! 
* Hva slags diskusjon finner sted på ulike typer issues?
* Trykk på *closed issues* og gå inn på noen lukkede issues. Gå nederst på siden og finn ut hvorfor de ble lukket. Er noen issues koblet til et pull request?

**Aktivitet 2.** Forsøk å opprette et issue på ditt eget repository. Gå inn på *Issues* og trykk på *New issue*. Følg en mal som du fant i *Aktivitet 1* til å skrive et fiktivt issue (eller et ekte issue, dersom du kommer på en en forbedring du ønsker for programmet ditt).
