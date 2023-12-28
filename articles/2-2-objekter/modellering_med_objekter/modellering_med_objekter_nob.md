---
title: "Modellering med objekter"
belongs_to_chain: "Hva er objekter?"
figures_to_include:
	- "modell_boker_personer.svg"
---

Se for deg at du har en stor boksamling, og du liker å anbefale og låne bort bøker til familie og venner. Du ønsker nå å lage et program som kan hjelpe deg. Programmet skal holde oversikt over bøkene i samlingen og registrere utlån til personer. Du ser for deg at programmet også kan gjøre mer komplekse ting, som å gjøre søk etter ledige bøker, hente informasjon om bøkene på internett, og kanskje til og med gi anbefalinger basert på interesser. Det vi har skrevet her er en *kravspesifikasjon* - en beskrivelse av ønskede funksjoner til programmet. Den kan være kort som her, eller mer detaljert. 

Vi har altså en kravspesifikasjon for et bokprogram. Siden dette bare er tekst, bør vi strukturere informasjonen før vi begynner å programmere. Det første vi bør spørre oss er hvilke objekter som finnes i kravspesifikasjonen. I dette tilfellet er hovedobjektene bøker og personer. Vi kan nå lage et enkelt diagram:

<img src="/media/markdowncontent/assosiated_files/modell_boker_personer.svg" width="500">

Vi har tegnet tre bokobjekter og tre personobjekter, for å vise at det finnes flere av hver type. Vi har også tegnet en kobling som viser at en person kan låne en bok.  Dette er en modell, altså en forenkling av virkeligheten. Her ønsker vi kun å vise hvilke objekter som er relevante og hvordan de er relaterte til hverandre. 

Hvordan vet vi hvilke objekter som er relevante? Her finnes det ikke et entydig svar, og det er ofte flere gode måter å modellere en situasjon. Men som en generell regel, så identifiserer vi de objektene som har relevante egenskaper og handlinger. Egenskaper gir informasjon om objektet, og handlinger er ting vi kan gjøre med objektet. Nå kan vi begrunne at bøker og personer er relevante objekter for programmet vårt:

- En bok har egenskaper, for eksempel tittel, forfatter og lånestatus (utlånt eller ledig).
- Man kan gjøre handlinger med en bok, for eksempel “Lån ut” og “Levér inn”. 
- En person har egenskaper, for eksempel navn og interesser. 
- Man kan gjøre handlinger med en person, for eksempel “Anbefal bok”.

Alle disse egenskapene og handlingene er relevante for bokprogrammet vårt.

