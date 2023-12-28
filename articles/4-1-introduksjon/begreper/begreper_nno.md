---
title: "Omgrep"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

Me skal no sjå på nokre viktige omgrep knytt til data og datahandtering. Sidan dette er vanskelege omgrep, skal me ikkje prøva å gi presise definisjonar, men heller gi døme som kan vera til hjelp.

**Kva er *informasjon*?**

Dersom me står i tett tåke, kan me ikkje seia mykje om det me ser rundt oss. Me kan derfor argumentera for at tåke ikkje inneheld noko *informasjon*. Men dersom litt av tåka forsvinn og me kan sjå omrisset av eit hus, så har me plutseleg struktur i synsinntrykket.

Kva meiner me med *struktur*? Struktur, eller mønster, er rett og slett noko som ikkje er heilt tilfeldig. Vassmolekyla i ei tåkesky svevar kanskje tilfeldig rundt i lufta, men materialet i eit hus er langt frå tilfeldig! Eit murhus består av leire som har vorte forma som rektangulære klossar og deretter sett oppå kvarandre på ein bestemd måte; her er det mykje struktur og mønster.

Der det finst struktur, finst også informasjon. Til dømes kan me beskriva korleis leira er forma som mursteinar med ei bestemd lengd, breidd og høgd. Informasjon kan altså sjåast på som ei skildring av struktur og mønstra.
    
**Kva er *data*?**

Informasjon kan formidlast på ulike måtar. *Data* er ein måte å beskriva struktur gjennom *konkrete verdiar*. Til dømes kan me beskriva eit murhus ved å oppgi konkrete storleiksmål:


```python
murstein_lengde = 25
murstein_bredde = 10
murstein_hoyde = 10
```

Men ein konkret verdi treng ikkje å vera eit tal; me kan også oppgi forma på hustak ved å definera ulike kategoriar:


```python
hus1_tak = "skrått"
hus2_tak = "flatt"
hus3_tak = "skrått"
```

Me bør likevel hugsa på at alle data blir lagra som tal; kvar bokstav blir lagra som eit tal i datamaskina, så ordet "skrått" er eigentleg ein sekvens av tal, og ordet "flatt" er ein annan talsekvens. Sidan alt likevel blir lagra som tal, kunne me først laga ei liste med kategoriane, og deretter brukt indeksane i lista for å registrera spesifikke hus:


```python
kategorier_hustak = ["skrått", "flatt"]

hus1_tak = 0
hus2_tak = 1
hus3_tak = 0
```

Ved å definera ein slik *assossiasjon* mellom tal og kategoriar sparer me plass i minnet til datamaskina, sidan me berre treng å skriva det fulle namnet på kategorien éin gong.

**Kva er *datahandtering*?**

Når me snakkar om *datahandtering*, meiner me alt ein kan gjera med data! Me kan dela inn datahandtering i to hovudkategoriar:

* Handtera data i si originale form: *lagring*, *sikring* og *utveksling* av data
* Forma om data til meiningsfull informasjon: *databehandling*

Som ei oppsummering av denne seksjonen kan me tenkja oss eit system for vêrvarsling:

1. I atmosfæren kan det finnast område med høgare trykk og område med lågare trykk. Trykket i atmosfæren er altså ikkje noko heilt tilfeldig, men har *mønster* og *struktur*.
2. Når me beskriv strukturen i atmosfæren, har me *informasjon*. Eit døme på informasjon kan vera at "det er høgare trykk i Oslo enn i Bergen i dag".
3. Me kan også beskriva atmosfæren med *data*; målestasjonar på ulike geografiske punkt kan ha sensorar som måler trykk, fukt, temperatur og anna. Sidan ei måling består av konkrete talverdiar, har me data.
4. Måledataa kan i første omgang lagrast på målestasjonen, og deretter blir sende til eit datasenter. Det er eit døme på *lagring og utveksling* av data. I desse stega handterer me måledataa i si originale form; slike data blir gjerne kalla *rådata*, fordi dei ikkje har gått gjennom noka form for bearbeiding.
5. På datamaskinene kan måledata frå heile landet blir brukt til å gjera simuleringar, det vil seia å berekna korleis atmosfæren kjem til å utvikla seg dei neste dagane. I dette steget blir måledataa brukte som parametrar i funksjonar, og returverdiar kjem ut. Returverdiane kan til slutt analyserast og blir presenterte i form av ei vêrmelding. Alt dette er *databehandling*; me formar om dei originale måledataa til meiningsfull og nyttig informasjon.

