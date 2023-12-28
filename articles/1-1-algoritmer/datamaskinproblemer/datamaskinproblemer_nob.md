---
title: "Datamaskinproblemer"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
---

Vi har sett på problemer som kan løses av menneskelige algoritmer, men hva kjennetegner et problem som kan løses av en dataalgoritme? Når vi definerer slike problemer, så må objektene være data! Det gir jo mening, for en datamaskin kan bare gjøre operasjoner på data, ikke fysiske objekter. Vi kan for eksempel definere et problem der objektene er tall: 

> **Problem** *Legge sammen to tall*    
**Inndata:** To desimaltall $A$ og $B$.    
**Ønsket utdata:** Desimaltallet $A+B$.

For datamaskinproblemer bruker vi begrepene *inndata* og *utdata* i stedet for "utgangspunkt" og "resultat". På engelsk brukes begrepene *input* og *output*. 

Det høres kanskje ut som en stor begrensning at objektene må være data, men husk at data kan være veldig mye forskjellig, som vist i følgende problem:

> **Problem** *Rotere bilde*    
**Inndata:** Et bilde $B$.    
**Ønsket utdata:** Bildet $B$ rotert 90 grader med klokka.

Hvordan lagres et bilde i datamaskinens minne? Det kan du lese mer om i kapittelet *Datahåndtering*. Når vi definerer problemer og utvikler algoritmer, er vi ikke alltid interessert i hvordan et objekt lagres på datamaskinen, vi må bare vite at det **kan** lagres som data. 

Til slutt skal vi se på et kjent datamaskinproblem, som vi skal komme tilbake til flere ganger gjennom kapittelet. 

Tenk deg at du har definert en liste av tall i Python: 


```python
L = [3.14, 1, 4.7, 0, 2]
```

Python har en funksjon for å finne det største elementet i lista: 


```python
M = max(L)
print(M)
```

    4.7


Funksjonen `max` er altså innebygd i Python, og løser følgende problem: 

> **Problem** *Finne største tall i en liste*   
**Inndata:** En liste $L$ av desimaltall.    
**Utdata:** Det største tallet $s$ i lista $L$.

**Aktivitetsforslag:** Gå inn på et program du nylig har kodet. Finn en funksjon med minst en parameter og returverdi (dersom du ikke har en slik funksjon, forsøk å sette noe av koden din inn i en funksjon). Hvilket problem løser funksjonen? Skriv en presis definisjon av problemet. 

