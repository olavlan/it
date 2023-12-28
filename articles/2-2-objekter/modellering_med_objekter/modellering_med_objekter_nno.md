---
title: "Modellering med objekt"
belongs_to_chain: "Hva er objekter?"
figures_to_include:
	- "modell_boker_personer.svg"
---

Sjå for deg at du har ei stor boksamling, og du liker å tilrå og låna bort bøker til familie og venner. Du ønskjer no å laga eit program som kan hjelpa deg. Programmet skal halda oversikt over bøkene i samlinga og registrera utlån til personar. Du ser for deg at programmet også kan gjera meir komplekse ting, som å gjera søk etter ledige bøker, henta informasjon om bøkene på internett, og kanskje til og med gi tilrådingar basert på interesser. Det me har skrive her er ein *kravspesifikasjon* - ei skildring av ønskte funksjonar til programmet. Den kan vera kort som her, eller meir detaljert.

Me har altså ein kravspesifikasjon for eit bokprogram. Sidan dette berre er tekst, bør me strukturera informasjonen før me byrjar å programmera. Det første me bør spørja oss er kva objekt som finst i kravspesifikasjonen. I dette tilfellet er hovudobjekta bøker og personar. Me kan nå laga eit enkelt diagram:

<img src="/media/markdowncontent/assosiated_files/modell_boker_personer.svg" width="500">

Me har teikna tre bokobjekt og tre personobjekt, for å visa at det finst fleire av kvar type. Me har også teikna ei kopling som viser at ein person kan låna ei bok.  Dette er ein modell, altså ei forenkling av røyndommen. Her ønskjer me berre å visa kva objekt som er relevante og korleis dei er relaterte til kvarandre.

Korleis veit me kva objekt som er relevante? Her finst det ikkje eit eintydig svar, og det er ofte fleire gode måtar å modellera ein situasjon. Men som ein generell regel, så identifiserer me dei objekta som har relevante eigenskapar og handlingar. Eigenskapar gir informasjon om objektet, og handlingar er ting me kan gjera med objektet. No kan me grunngi at bøker og personar er relevante objekt for programmet vårt:

- Ei bok har eigenskapar, til dømes tittel, forfattar og lånestatus (utlånt eller ledig).
- Ein kan gjera handlingar med ei bok, til dømes “Lån ut” og “Levér inn”.
- Ein person har eigenskapar, til dømes namn og interesser.
- Ein kan gjera handlingar med ein person, til dømes “Anbefal bok”.

Alle desse eigenskapane og handlingane er relevante for bokprogrammet vårt.

