---
title: "Mer om pseudokode og flytdiagram"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
	- "algoritmer_flytdiagram_for.svg"
	- "algoritmer_flytdiagram_if.svg"
---

I denne seksjonen viser vi hvordan man presenterer **for**-løkker og større **if**-**else**-setninger med både pseudokode og flytdiagram.  

En **for**-løkke kan skrives med pseudokode på følgende måte: 

> **for** $i$ **from** $1$ **to** $10$   
&emsp; **display** $i$   

For å tegne et flytdiagram for denne løkken kan vi først omforme det til en **while**-løkke! Prøv gjerne å gjøre dette selv! 

Iterasjonsvariabelen $i$ skal starte på $1$ og gå til $10$. Vi kan oppnå dette på følgende måte:  

>**set** $i$ **to** $1$    
**while** $i$ **smaller than or equal to**  $10$  
&emsp;**display** $i$    
&emsp;**set** $i$ **to** $i + 1$  

Nå kan vi tegne løkken på samme måte som tidligere: 

<img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram_for.svg">

I dette flytdiagrammet har vi ikke inndata eller utdata, så vi bruker en **startboks** og en **stoppboks**. Disse tegnes som runde eller ovale bokser. 

Sammenlign gjerne løkken med den vi hadde i forrige seksjon. Legg spesielt merke til at vi alltid oppdaterer iterasjonsvariabelen på slutten av løkken. Ellers ville vi endt opp med en uendelig løkke! 

Nå ser vi på hvordan man kan skrive større **if**-**else**-setninger med pseudokode. Vi tar utgangspunkt i et eksempel skrevet i Python:


```python
def livsfase(alder): 
    if alder <= 12:
        return "barn"
    elif alder > 12 and alder < 18:
        return "ungdom"
    else:
        return "voksen"
```

Vi kan presentere algoritmen med pseudokode på følgende måte: 

>**Algoritme** *Livsfase*    
**Inndata:** Et positivt heltall $a$   
**Utdata:** Livsfasen $l$ til en person med alder $a$
>
>**if** $a$ **lesser than or equal to** $12$     
&emsp;**set** $l$ **to** *barn*   
**else if** $a$ **greater than** $12$ **and lesser than**   $18$   
&emsp;**set** $l$ **to** *ungdom*   
**else**  
&emsp;**set** $l$ **to** *voksen*   
**endif**         
**return** $l$  

Til slutt kan vi presentere algoritmen med et flytdiagram:

>**Algoritme** *Livsfase*
>
><img src="/media/markdowncontent/assosiated_files/algoritmer_flytdiagram_if.svg">

Merk at hvis den første testen gir positivt svar, hopper vi over de neste testene. Det er kun når en test gir negativt svar at vi fortsetter til den neste testen. Ved å følge samme mønster som over, kan du tegne vilkårlig store **if**-**else**-setninger. 

**Aktivitetsforslag:** Gå inn på et program du nylig har skrevet og velg noen kodelinjer som inneholder løkker og betingelser. Omform koden til både pseudokode og flytdiagram.  
