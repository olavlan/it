---
title: "Beskriva algoritmar med ord"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
---

Me skal no beskriva ein algoritme for å finna det største talet i ei liste $L$. La oss sjå på eit konkret døme, nemleg lista $[3.14, \ 1, \ 4.7, \ 0, \ 2]$. Lista har fem tal, og me treng ein algoritme som finn det høgaste talet.

Som menneske ser me omgåande at $4.7$ er det høgaste talet i lista, men korleis kan me komma fram til dette på ein strukturert måte som alltid fungerer? Me kan gå gjennom lista, frå det første til det siste talet, medan me undervegs held #styr på det største talet me har funne. Følgjande tabell viser korleis denne metoden fungerer:

| Neste element i lista | 3.14 | 1    | 4.7 | 0   | 2   |
|-----------------------|------|------|-----|-----|-----|
| Hittil høgaste tal   | 3.14 | 3.14 | 4.7 | 4.7 | 4.7 |

I kvart steg samanliknar me det neste talet i lista med det hittil største talet me har funne. La oss presentera denne algoritmen:

> **Algoritme** *Finn største tal*
**Inndata:** Ei liste $L$ av desimaltal
**Utdata:** Det største talet $s$ i lista $L$
> 
> 1. Sett $s$ til å vera det første talet i lista $L$.
> 2. Samanlikn $s$ med det neste talet i $L$. Dersom det neste talet er større, sett $s$ til denne verdien.
> 3. Dersom $L$ har fleire element, gjenta steg 2
> 4. Returner $s$.

Legg merke til at me har teke med følgjande informasjon om algoritmen:

* Me har gitt algoritmen eit namn, nemleg *Finn største tal*
* Me har definert inndata og utdata for algoritmen
* Til slutt har me skrive stega for algoritmen

Dette er ein oversiktleg måte å presentera ein algoritme på.

Legg også merke til korleis me bruker variabelen $s$ til å halda #styr på kva som er det hittil høgaste talet i lista. La oss bruka algoritmen på lista $[1,2,3,2,1,4,3,5]$. Følgjande tabell viser korleis $s$ blir etter kvart oppdatert som me går gjennom lista:

|  Neste tal i lista   | 1 | 2 | 3 | 2 | 1 | 4 | 3 | 5 |
|-----|---|---|---|---|---|---|---|---|
| $s$ | 1 | 2 | 3 | 3 | 3 | 4 | 4 | 5 |

**Aktivitetsforslag 1:** Utfør algoritmen *Finn største tal* på listene som er genererte nedanfor. Du skal altså tenkja over kva som skjer ved kvart steg, og skriva ned korleis variabelen $s$ endrar seg undervegs. Kva verdi blir returnert av algoritmen?


```python
from random import randint

for i in range(3):
    random_list = [randint(0,10) for i in range(10)]
    print(random_list)
```

    [6, 2, 4, 0, 7, 2, 8, 7, 3, 7]
    [10, 7, 5, 8, 5, 7, 7, 6, 3, 2]
    [4, 4, 10, 1, 1, 1, 5, 0, 0, 9]


**Aktivitetsforslag 2:** Gå inn på eit program du nyleg har koda. Finn ein funksjon med minst ein parameter og returverdi (dersom du ikkje har ein slik funksjon, forsøk å setja noko av koden din inn i ein funksjon). Kva problem løyser funksjonen? Presenter algoritmen som løyser problemet. Du skal altså skriva med ord kva steg koden din utfører.

