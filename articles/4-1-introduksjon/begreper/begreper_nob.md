---
title: "Begreper"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

Vi skal nå se på noen viktige begreper knyttet til data og datahåndtering. Siden dette er vanskelige begreper, skal vi ikke forsøke å gi presise definisjoner, men heller gi eksempler som kan være til hjelp. 

**Hva er *informasjon*?** 

Dersom vi står i tett tåke, kan vi ikke si mye om det vi ser rundt oss. Vi kan derfor argumentere for at tåke ikke inneholder noe *informasjon*. Men dersom litt av tåka forsvinner og vi kan se omrisset av et hus, så har vi plutselig struktur i synsinntrykket. 

Hva mener vi med *struktur*? Struktur, eller mønster, er rett og slett noe som ikke er helt tilfeldig. Vannmolekylene i en tåkesky svever kanskje tilfeldig rundt i lufta, men materialet i et hus er langt fra tilfeldig! Et murhus består av leire som har blitt formet som rektangulære klosser og deretter satt oppå hverandre på en bestemt måte; her er det mye struktur og mønster. 

Der det finnes struktur, finnes også informasjon. For eksempel kan vi beskrive hvordan leira er formet som mursteiner med en bestemt lengde, bredde og høyde. Informasjon kan altså sees på som en beskrivelse av struktur og mønstre. 
    
**Hva er *data*?** 

Informasjon kan formidles på forskjellige måter. *Data* er en måte å beskrive struktur gjennom *konkrete verdier*. For eksempel kan vi beskrive et murhus ved å oppgi konkrete størrelsesmål: 


```python
murstein_lengde = 25
murstein_bredde = 10
murstein_hoyde = 10
```

Men en konkret verdi trenger ikke å være et tall; vi kan også oppgi formen på hustak ved å definere forskjellige kategorier:


```python
hus1_tak = "skrått"
hus2_tak = "flatt"
hus3_tak = "skrått"
```

Vi bør likevel huske på at alle data lagres som tall; hver bokstav lagres som et tall i datamaskinen, så ordet "skrått" er egentlig en sekvens av tall, og ordet "flatt" er en annen tallsekvens. Siden alt likevel lagres som tall, kunne vi først laget en liste med kategoriene, og deretter brukt indeksene i lista for å registrere spesifikke hus: 


```python
kategorier_hustak = ["skrått", "flatt"]

hus1_tak = 0
hus2_tak = 1
hus3_tak = 0
```

Ved å definere en slik *assossiasjon* mellom tall og kategorier sparer vi plass i datamaskinens minne, siden vi bare trenger å skrive det fulle navnet på kategorien én gang.

**Hva er *datahåndtering*?** 

Når vi snakker om *datahåndtering*, mener vi alt man kan gjøre med data! Vi kan dele inn datahåndtering i to hovedkategorier:

* Håndtere data i sin originale form: *lagring*, *sikring* og *utveksling* av data
* Omforme data til meningsfull informasjon: *databehandling*

Som en oppsummering av denne seksjonen kan vi tenke oss et system for værvarsling: 

1. I atmosfæren kan det finnes områder med høyere trykk og områder med lavere trykk. Trykket i atmosfæren er altså ikke noe helt tilfeldig, men har *mønster* og *struktur*.
2. Når vi beskriver strukturen i atmosfæren, har vi *informasjon*. Et eksempel på informasjon kan være at "det er høyere trykk i Oslo enn i Bergen i dag". 
3. Vi kan også beskrive atmosfæren med *data*; målestasjoner på forskjellige geografiske punkter kan ha sensorer som måler trykk, fuktighet, temperatur og annet. Siden en måling består av konkrete tallverdier, har vi data. 
4. Måledataene kan i første omgang lagres på målestasjonen, og deretter sendes til et datasenter. Det er et eksempel på *lagring og utveksling* av data. I disse stegene håndterer vi måledataene i sin originale form; slike data kalles gjerne *rådata*, fordi de ikke har gjennomgått noen form for bearbeiding.
5. På datamaskinene kan måledata fra hele landet brukes til å gjøre simuleringer, det vil si å beregne hvordan atmosfæren kommer til å utvikle seg de neste dagene. I dette steget blir måledataene brukt som parametre i funksjoner, og returverdier kommer ut. Returverdiene kan til slutt analyseres og presenteres i form av en værmelding. Alt dette er *databehandling*; vi omformer de originale måledataene til meningsfull og nyttig informasjon. 

