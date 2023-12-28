---
title: "Datamaskinproblem"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
---

Me har sett på problem som kan løysast av menneskelege algoritmar, men kva kjenneteiknar eit problem som kan løysast av ein dataalgoritme? Når me definerer slike problem, så må objekta vera data! Det gir jo meining, for ei datamaskin kan berre gjera operasjonar på data, ikkje fysiske objekt. Me kan til dømes definera eit problem der objekta er tal:

> **Problem** *Leggja saman to tal*
**Inndata:** To desimaltal $A$ og $B$.
**Ønskte utdata:** Desimaltalet $A+B$.

For datamaskinproblem bruker me omgrepa *inndata* og *utdata* i staden for "utgangspunkt" og "resultat". På engelsk blir omgrepa brukte *input* og *output*.

Det høyrest kanskje ut som ei stor avgrensing at objekta må vera data, men hugs at data kan vera veldig mykje ulik, som vist i følgjande problem:

> **Problem** *Rotere bilete*
**Inndata:** Eit bilete $B$.
**Ønskte utdata:** Biletet $B$ rotert 90 grader med klokka.

Korleis blir eit bilete lagra i minnet til datamaskina? Det kan du lesa meir om i kapittelet *Datahåndtering*. Når me definerer problem og utviklar algoritmar, er me ikkje alltid interessert i korleis eit objekt blir lagra på datamaskina, me må berre vita at det **kan** lagrast som data.

Til slutt skal me sjå på eit kjent datamaskinproblem, som me skal komma tilbake til fleire gonger gjennom kapittelet.

Tenk deg at du har definert ei liste av tal i Python:


```python
L = [3.14, 1, 4.7, 0, 2]
```

Python har ein funksjon for å finna det største elementet i lista:


```python
M = max(L)
print(M)
```

    4.7


Funksjonen `max` er altså innebygd i Python, og løyser følgjande problem:

> **Problem** *Finne største tal i ei liste*
**Inndata:** Ei liste $L$ av desimaltal.
**Utdata:** Det største talet $s$ i lista $L$.

**Aktivitetsforslag:** Gå inn på eit program du nyleg har koda. Finn ein funksjon med minst ein parameter og returverdi (dersom du ikkje har ein slik funksjon, forsøk å setja noko av koden din inn i ein funksjon). Kva problem løyser funksjonen? Skriv ein presis definisjon av problemet.

