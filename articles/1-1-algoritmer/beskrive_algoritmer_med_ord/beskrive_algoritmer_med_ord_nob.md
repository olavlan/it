---
title: "Beskrive algoritmer med ord"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
---

Vi skal nå beskrive en algoritme for å finne det største tallet i en liste $L$. La oss se på et konkret eksempel, nemlig lista $[3.14, \ 1, \ 4.7, \ 0, \ 2]$. Lista har fem tall, og vi trenger en algoritme som finner det høyeste tallet.

Som mennesker ser vi umiddelbart at $4.7$ er det høyeste tallet i lista, men hvordan kan vi komme fram til dette på en strukturert måte som alltid fungerer? Vi kan gå gjennom lista, fra det første til det siste tallet, mens vi underveis holder styr på det største tallet vi har funnet. Følgende tabell viser hvordan denne metoden fungerer: 

| Neste element i lista | 3.14 | 1    | 4.7 | 0   | 2   |
|-----------------------|------|------|-----|-----|-----|
| Hittil høyeste tall   | 3.14 | 3.14 | 4.7 | 4.7 | 4.7 |

I hvert steg sammenligner vi det neste tallet i lista med det hittil største tallet vi har funnet. La oss presentere denne algoritmen:

> **Algoritme** *Finn største tall*    
**Inndata:** En liste $L$ av desimaltall    
**Utdata:** Det største tallet $s$ i lista $L$
> 
> 1. Sett $s$ til å være det første tallet i lista $L$.
> 2. Sammenlign $s$ med det neste tallet i $L$. Dersom det neste tallet er større, sett $s$ til denne verdien. 
> 3. Dersom $L$ har flere elementer, gjenta steg 2.
> 4. Returner $s$. 

Legg merke til at vi har tatt med følgende informasjon om algoritmen:

* Vi har gitt algoritmen et navn, nemlig *Finn største tall*
* Vi har definert inndata og utdata for algoritmen
* Til slutt har vi skrevet stegene for algoritmen

Dette er en oversiktlig måte å presentere en algoritme på. 

Legg også merke til hvordan vi bruker variabelen $s$ til å holde styr på hva som er det hittil høyeste tallet i lista. La oss bruke algoritmen på lista $[1,2,3,2,1,4,3,5]$. Følgende tabell viser hvordan $s$ oppdateres etter hvert som vi går gjennom lista: 

|  Neste tall i lista   | 1 | 2 | 3 | 2 | 1 | 4 | 3 | 5 |
|-----|---|---|---|---|---|---|---|---|
| $s$ | 1 | 2 | 3 | 3 | 3 | 4 | 4 | 5 |

**Aktivitetsforslag 1:** Utfør algoritmen *Finn største tall* på listene som er generert nedenfor. Du skal altså tenke over hva som skjer ved hvert steg, og skrive ned hvordan variabelen $s$ endrer seg underveis. Hvilken verdi returneres av algoritmen?


```python
from random import randint

for i in range(3):
    random_list = [randint(0,10) for i in range(10)]
    print(random_list)
```

    [6, 2, 4, 0, 7, 2, 8, 7, 3, 7]
    [10, 7, 5, 8, 5, 7, 7, 6, 3, 2]
    [4, 4, 10, 1, 1, 1, 5, 0, 0, 9]


**Aktivitetsforslag 2:** Gå inn på et program du nylig har kodet. Finn en funksjon med minst en parameter og returverdi (dersom du ikke har en slik funksjon, forsøk å sette noe av koden din inn i en funksjon). Hvilket problem løser funksjonen? Presenter algoritmen som løser problemet. Du skal altså skrive med ord hvilke steg koden din utfører.

