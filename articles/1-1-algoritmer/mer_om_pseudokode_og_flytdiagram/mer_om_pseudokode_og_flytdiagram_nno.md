---
title: "Meir om pseudokode og flytdiagram"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
	- "algoritmer_flytdiagram_for.svg"
	- "algoritmer_flytdiagram_if.svg"
---

I denne seksjonen viser me korleis ein presenterer **for**-løkker og større **if**-**else**-setningar med både pseudokode og flytdiagram.

Ein **for**-løkke kan skrivast med pseudokode på følgjande måte:

> **for** $i$ **from** $1$ **to** $10$
&emsp; **display** $i$

For å teikna eit flytdiagram for denne løkka kan me først forma om det til ein **while**-løkke! Prøv gjerne å gjera dette sjølv!

Iterasjonsvariabelen $i$ skal starta på $1$ og gå til $10$. Me kan oppnå dette på følgjande måte:

>**set** $i$ **to** $1$
**while** $i$ **smaller than or equal to**  $10$
&emsp;**display** $i$
&emsp;**set** $i$ **to** $i + 1$

No kan me teikna løkka på same måte som før:

<img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram_for.svg">

I dette flytdiagrammet har me ikkje inndata eller utdata, så me bruker ein **startboks** og ein **stoppboks**. Desse blir teikna som runde eller ovale boksar.

Samanlikn gjerne løkka med den me hadde i førre seksjon. Legg spesielt merke til at me alltid oppdaterer iterasjonsvariabelen på slutten av løkka. Elles ville me enda opp med ei uendeleg løkke!

No ser me på korleis ein kan skriva større **if**-**else**-setningar med pseudokode. Me tek utgangspunkt i eit døme skrive i Python:


```python
def livsfase(alder): 
    if alder <= 12:
        return "barn"
    elif alder > 12 and alder < 18:
        return "ungdom"
    else:
        return "voksen"
```

Me kan presentera algoritmen med pseudokode på følgjande måte:

>**Algoritme** *Livsfase*
**Inndata:** Eit positivt heiltal $a$
**Utdata:** Livsfasen $l$ til ein person med alder $a$
>
>**if** $a$ **lessar than or equal to** $12$
&emsp;**set** $l$ **to** *barn*
**else if** $a$ **greater than** $12$ **and lessar than**   $18$
&emsp;**set** $l$ **to** *ungdom*
**else**
&emsp;**set** $l$ **to** *voksen*
**endif**
**return** $l$

Til slutt kan me presentera algoritmen med eit flytdiagram:

>**Algoritme** *Livsfase*
>
><img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram_if.svg">

Merk at viss den første testen gir positivt svar, hoppar me over dei neste testane. Det er berre når ein test gir negativt svar at me held fram til den neste testen. Ved å følgja same mønster som over, kan du teikna vilkårleg store **if**-**else**-setningar.

**Aktivitetsforslag:** Gå inn på eit program du nyleg har skrive og vel nokre kodelinjer som inneheld løkker og vilkår. Form om koden til både pseudokode og flytdiagram.
