---
title: "Det prosedyreorienterte paradigmet"
belongs_to_chain: "Når og hvorfor brukes objektorientert programmering?"
figures_to_include:
---

I forrige seksjon så vi et program som regner ut avstand mellom punkter. Du så kanskje at vi gjorde samme utregning to ganger? Matematiske utregninger plasseres gjerne i funksjoner:

```py
def avstand(a, b):
    return ((a[0]-b[0])**2+(a[1]-b[1])**2)**0.5

avstand_p_q = avstand(p, q)
avstand_q_o = avstand(q, o)
```
Vi har nå tatt i bruk prosedyreorientert programmering! Det handler rett og slett om å bruke prosedyrer, også kalt funksjoner. Mange vil si at funksjoner er den mest grunnleggende strukturen i matematikk. Derfor er prosedyreorientert programmering det naturlige valget når vi skal gjøre matematiske beregninger. 

Med prosedyreorientert programmering ønsker vi å separere funksjoner og data, slik at funksjonene kan ta imot data fra svært ulike kilder. Matematiske funksjoner er jo nettopp slik - ikke begrenset til et spesifikt formål, men nyttige i mange ulike situasjoner. For eksempel kan avstandfunksjonen være like aktuell for behandling av kartdata som for diagnostisering av sykdom (punkter kan også være *datapunkter*, som for eksempel kan inneholde verdier av blodprøver). 

