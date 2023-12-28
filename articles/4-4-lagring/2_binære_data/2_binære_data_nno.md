---
title: "Binære data"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I førre kapittel såg me at eit lite alfabet ikkje set nokon avgrensingar for kva me kan uttrykkja. No skal me sjå på det minste moglege alfabetet me kan bruka, nemleg eit alfabet med berre to teikn! Det er vanleg å bruka *0* og *1* som symbol for eit slikt alfabet:

```
0, 1
```

Nokon strengjar me kan laga med dette alfabetet er *00*, *01*, *10*, *11* og *000*. At me har valt *0* og *1* som teikn betyr ikkje at me skal tenkja på dei som tal. Strengen *1000* betyr **ikkje** tusen, men har i staden den betydninga me vel å gi det. Til dømes kan det bety ein bokstav i det norske alfabetet, eller ein farge.

Med dette alfabetet kan me lagra all digital informasjon, det vil seia all informasjon som kan skrivast som ein sekvens av teikn. Me kan til dømes sjå på ein DNA-sekvens:

```
ATGCAAGCTAATGGGTTCCAGTAA
```

Korleis lagrar me denne informasjonen ved å berre bruka *0* og *1*? Me kan gi ein kode til kvart av teikna *A*, *T*, *C*, *G*:

| Tegn | Kode |
|------|------------|
| A    | 00         |
| C    | 01         |
| G    | 10         |
| T    | 11         |

Kan du bruka denne koden til å omsetja DNA-sekvensen?

Resultatet blir:

```
0011100100001001110000111010111101010010110000
```

Med berre to teikn kan me altså lagra ein DNA-sekvens, og data som er lagra på denne måten blir kalla *binære data*. Strengene me kan laga med alfabetet, som til dømes *00*, *111*, *0101*, blir kalla  *bitstrenger*. Me kan bruka eininga *bit* til å angi mengda data i ein bitstreng. Talet på bit er rett og slett talet på teikn, så *00* består av to bitar, *111* av tre bitar, *0101* av fire bitar, og så vidare.

Kva er poenget med å lagra informasjon som binære data?

Tenk deg at du har fire lyspærer og ønskjer å bruka dei til å lagra bitstrengen *0101*. Då kan du slå på den andre og fjerde lyspæra, og la den første og tredje vera avslått. Altså kan me tenkja at *1* betyr pålått, og *0* betyr avslått.

Litt forenkla kan me seia at ei datamaskin er bygd opp av bitte små elektroniske krinsar som anten kan vera på eller av. Dette kan me utnytta til å lagra binære data! Me kan seia at binære data er det naturlege språket til datamaskina.

**Aktivitetsforslag 1:** Dei binære strengene av lengd 2 er *00*, *01*, *10* og *11*. Kan du skriva opp alle binære strenger av lengd 3? Kva med lengd 4? Og lengd 5? Skriv talet på binære strenger du finn i tabellen under.

| Lengde | Mengd strengjar |
|--------|-----------------|
| 2      | 4               |
| 3      |                 |
| 4      |                 |
| 5      |                 |

Kor mange binære strenger trur du det finst av lengd 6?

**Aktivitetsforslag 2.** Gjer først *Aktivitetsforslag 1*. Tenk deg no at du skal laga ein binær kode for alle norske bokstavar, mellomrom, komma og punktum. Kor mange binære kodar treng du?

For at du skal ha nok binære kodar, må dei ha ei viss lengd. Kor lange må dei vera?

Lag ein binær kode for alle bokstavar, og dessutan mellomrom, komma og punktum. Omset deretter følgjande setning til binær kode:

*Informatikk er gøy.*

