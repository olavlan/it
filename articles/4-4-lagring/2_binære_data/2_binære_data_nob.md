---
title: "Binære data"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I forrige kapittel så vi at et lite alfabet ikke setter noen begrensninger for hva vi kan uttrykke. Nå skal vi se på det minste mulige alfabetet vi kan bruke, nemlig et alfabet med bare to tegn! Det er vanlig å bruke *0* og *1* som symboler for et slikt alfabet: 

```
0, 1
```

Noen strenger vi kan lage med dette alfabetet er *00*, *01*, *10*, *11* og *000*. At vi har valgt *0* og *1* som tegn betyr ikke at vi skal tenke på dem som tall. Strengen *1000* betyr **ikke** tusen, men har i stedet den betydning vi velger å gi det. For eksempel kan det bety en bokstav i det norske alfabetet, eller en farge. 

Med dette alfabetet kan vi lagre all digital informasjon, det vil si all informasjon som kan skrives som en sekvens av tegn. Vi kan for eksempel se på en DNA-sekvens: 

```
ATGCAAGCTAATGGGTTCCAGTAA
```

Hvordan lagrer vi denne informasjonen ved å bare bruke *0* og *1*? Vi kan gi en kode til hvert av tegnene *A*, *T*, *C*, *G*: 

| Tegn | Kode |
|------|------------|
| A    | 00         |
| C    | 01         |
| G    | 10         |
| T    | 11         |

Kan du bruke denne koden til å oversette DNA-sekvensen? 

Resultatet blir: 

```
0011100100001001110000111010111101010010110000
```

Med kun to tegn kan vi altså lagre en DNA-sekvens, og data som er lagret på denne måten kalles *binære data*. Strengene vi kan lage med alfabetet, som for eksempel *00*, *111*, *0101*, kalles  *bitstrenger*. Vi kan bruke enheten *bit* til å angi mengden data i en bitstreng. Antall bit er rett og slett antall tegn, så *00* består av to bits, *111* av tre bits, *0101* av fire bits, og så videre. 

Hva er poenget med å lagre informasjon som binære data? 

Tenk deg at du har fire lyspærer og ønsker å bruke dem til å lagre bitstrengen *0101*. Da kan du slå på den andre og fjerde lyspæren, og la den første og tredje være avslått. Altså kan vi tenke at *1* betyr påslått, og *0* betyr avslått. 

Litt forenklet kan vi si at en datamaskin er bygget opp av bittesmå elektroniske kretser som enten kan være på eller av. Dette kan vi utnytte til å lagre binære data! Vi kan si at binære data er datamaskinens naturlige språk. 

**Aktivitetsforslag 1:** De binære strengene av lengde 2 er *00*, *01*, *10* og *11*. Kan du skrive opp alle binære strenger av lengde 3? Hva med lengde 4? Og lengde 5? Skriv antall binære strenger du finner i tabellen under.

| Lengde | Antall strenger |
|--------|-----------------|
| 2      | 4               |
| 3      |                 |
| 4      |                 |
| 5      |                 |

Hvor mange binære strenger tror du det finnes av lengde 6? 

**Aktivitetsforslag 2.** Gjør først *Aktivitetsforslag 1*. Tenk deg nå at du skal lage en binær kode for alle norske bokstaver, mellomrom, komma og punktum. Hvor mange binære koder trenger du?

For at du skal ha nok binære koder, må de ha en viss lengde. Hvor lange må de være? 

Lag en binær kode for alle bokstaver, samt mellomrom, komma og punktum. Oversett deretter følgende setning til binær kode: 

*Informatikk er gøy.*

