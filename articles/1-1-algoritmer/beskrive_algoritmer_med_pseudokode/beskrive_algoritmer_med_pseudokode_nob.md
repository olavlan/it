---
title: "Beskrive algoritmer med pseudokode"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
---

En vanlig måte å presentere algoritmer på er med *pseudokode*.
Når vi skriver pseudokode, bruker vi ikke hele setninger, men skriver kommandoer ved hjelp av variabler og nøkkelord.
Disse kommandoene er likevel bare skrevet for å leses av mennesker, og kan ikke kjøres på en datamaskin.

Som et eksempel på pseudokode ser vi på det første steget i algoritmen *Finn største tall*: 

> Sett $s$ til å være det første tallet i lista $L$.

Med Python kunne vi programmert dette med kodelinja:

```
s = L[0]
```

Hvordan skriver vi dette steget med pseudokode? For å gi en verdi til en variabel, er det vanlig å bruke nøkkelordene **set** og **to**, på følgende måte: 

>**set** $s$ **to** $L[0]$   

Hva er poenget med dette? Hvorfor ikke bruke hele setninger eller ferdig programkode? 

* Pseudokode er mer presist enn hele setninger, og kan dermed lettere oversettes til programkode.
* Pseudokode er mer lesbart enn programkode, fordi hver linje kan leses som en setning. Videre trenger man ikke å kunne et spesifikt programmeringsspråk for å lese pseudokode. I stedet kan pseudokoden oversettes til et **valgfritt** programmeringsspråk. 

La oss nå se på hvordan vi kan presentere hele algoritmen *Finn største tall* med pseudokode:

>**Algoritme** *Finn største tall*    
**Inndata:** En liste $L$ med $n$ desimaltall    
**Utdata:** Det største tallet $s$ i lista $L$
>
>**set**  $s$  **to**  $L[0]$   
**set**  $i$  **to**  $1$   
**while**  $i$  **smaller than**  $n$   
&emsp;**if**  $L[i]$  **greater than**  $s$   
&emsp;&emsp;**set**  $s$  **to**  $L[i]$    
&emsp;**endif**   
&emsp;**set**  $i$  **to**  $i + 1$   
**endwhile**     
**return**  $s$   

Nå kan algoritmen lett oversettes til en Python-funksjon: 


```python
def find_largest_number(L,n):
    s = L[0]
    i = 1
    while i < n:
        if L[i] > s:
            s = L[i]
        i = i + 1
    return s
```

Å oversette en algoritme fra pseudokode til programkode kalles å *implementere* algoritmen. Her har vi brukt Python til å implementere algoritmen *Finn største tall*. Sammenlign gjerne pseudokoden med Python-koden. Synes du pseudokoden er lettere å lese? 

Det finnes ingen universelle regler for hvordan pseudokode skal skrives, men vi forsøker å skrive det på en måte som kan forstås av alle som programmerer, uansett hvilket programmeringsspråk man bruker. Da er det nyttig å bruke selvforklarende nøkkelord i stedet for symboler. For eksempel brukes gjerne nøkkelord som **while**, **if** og **greater than**. 

Merk også at vi bruker **endwhile** for å markere hvor **while**-blokken slutter. Antagelig har du ikke brukt denne skrivemåten i noe programmeringsspråk. I  Java brukes for eksempel krøllparentesene {} for å angi hvor en blokk starter og slutter, mens i Python brukes innrykk. Men uansett om man er vant med Java eller Python, vil man kunne forstå pseudokoden!

Hovedforskjellen mellom pseudokode og programkode er altså: 

* I pseudokode bruker vi selvforklarende nøkkelord i stedet for spesifikke symboler og regler.

*Du har kanskje lagt merke til at pseudokoden i eksempelet også har innrykk? Det er en måte å gjøre pseudokoden lettere å lese, men det er ikke nødvendig! Vi bruker jo nøkkelord som **endwhile** og **endif** for å markere hvor blokkene slutter, så i prinsippet kan alle linjer være uten innrykk.*

**Aktivitetsforslag:** Ta utgangspunkt i *Aktivitetsforslag 2* fra forrige seksjon. Presenter algoritmen med pseudokode. 

