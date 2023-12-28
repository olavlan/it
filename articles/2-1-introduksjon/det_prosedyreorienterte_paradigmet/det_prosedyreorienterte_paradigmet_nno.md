---
title: "Det prosedyreorienterte paradigmet"
belongs_to_chain: "Når og hvorfor brukes objektorientert programmering?"
figures_to_include:
---

I førre seksjon såg me eit program som reknar ut avstand mellom punkt. Du så kanskje at me gjorde same utrekning to gonger? Matematiske utrekningar blir gjerne plasserte i funksjonar:

```py
def avstand(a, b):
    return ((a[0]-b[0])**2+(a[1]-b[1])**2)**0.5

avstand_p_q = avstand(p, q)
avstand_q_o = avstand(q, o)
```
Me har no teke i bruk prosedyreorientert programmering! Det handlar rett og slett om å bruka prosedyrar, også kalla funksjonar. Mange vil seia at funksjonar er den mest grunnleggjande strukturen i matematikk. Derfor er prosedyreorientert programmering det naturlege valet når me skal gjera matematiske berekningar.

Med prosedyreorientert programmering ønskjer me å separera funksjonar og data, slik at funksjonane kan ta imot data frå svært ulike kjelder. Matematiske funksjonar er jo nettopp slik - ikkje avgrensa til eit spesifikt formål, men nyttige i mange ulike situasjonar. Til dømes kan avstandsfunksjonen vera like aktuell for behandling av kartdata som for diagnostisering av sjukdom (punkt kan også vera *datapunkt*, som til dømes kan innehalda verdiar av blodprøver).

