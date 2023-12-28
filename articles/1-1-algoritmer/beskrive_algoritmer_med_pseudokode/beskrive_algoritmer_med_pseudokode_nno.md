---
title: "Beskriva algoritmar med pseudokode"
belongs_to_chain: "Introduksjon og måter å presentere algoritmer"
figures_to_include:
---

Ein vanleg måte å presentera algoritmar på er med *pseudokode*.
Når me skriv pseudokode, bruker me ikkje heile setningar, men skriv kommandoar ved hjelp av variablar og nøkkelord.
Desse kommandoane er likevel berre skrive for å lesast av menneske, og kan ikkje køyrast på ei datamaskin.

Som eit døme på pseudokode ser me på det første steget i algoritmen *Finn største tal*:

> Sett $s$ til å vera det første talet i lista $L$.

Med Python kunne me programmert dette med kodelinja:

```
s = L[0]
```

Korleis skriv me dette steget med pseudokode? For å gi ein verdi til ein variabel, er det vanleg å bruka nøkkelorda **set** og **to**, på følgjande måte:

>**set** $s$ **to** $L[0]$

Kva er poenget med dette? Kvifor ikkje bruka heile setningar eller ferdig programkode?

* Pseudokode er meir presist enn heile setningar, og kan dermed lettare omsetjast til programkode.
* Pseudokode er meir lesbart enn programkode, fordi kvar linje kan lesast som ei setning. Vidare treng ein ikkje å kunna eit spesifikt programmeringsspråk for å lesa pseudokode. I staden kan pseudokoden omsetjast til eit **valfritt** programmeringsspråk.

La oss no sjå på korleis me kan presentera heile algoritmen *Finn største tal* med pseudokode:

>**Algoritme** *Finn største tal*
**Inndata:** Ei liste $L$ med $n$ desimaltal
**Utdata:** Det største talet $s$ i lista $L$
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

No kan algoritmen lett omsetjast til ein Python-funksjon:


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

Å omsetja ein algoritme frå pseudokode til programkode blir kalla å *implementera* algoritmen. Her har me brukt Python til å implementera algoritmen *Finn største tal*. Samanlikn gjerne pseudokoden med Python-koden. Synest du pseudokoden er lettare å lesa?

Det finst ingen universelle reglar for korleis pseudokode skal skrivast, men me prøver å skriva det på ein måte som kan forståast av alle som programmerer, uansett kva programmeringsspråk ein bruker. Då er det nyttig å bruka sjølvforklarande nøkkelord i staden for symbol. Til dømes blir gjerne brukt nøkkelord som **while**, **if** og **greater than**.

Merk også at me bruker **endwhile** for å markera kor **while**-blokka sluttar. Antakeleg har du ikkje brukt denne skrivemåten i noko programmeringsspråk. I  Java blir til dømes brukt krøllparentesane {} for å angi kvar ei blokk startar og sluttar, medan i Python blir innrykk brukt. Men anten ein er vant med Java eller Python, vil ein kunna forstå pseudokoden!

Hovudforskjellen mellom pseudokode og programkode er altså:

* I pseudokode bruker me sjølvforklarande nøkkelord i staden for spesifikke symbol og reglar.

*Du har kanskje lagt merke til at pseudokoden i dømet også har innrykk? Det er ein måte å gjera pseudokoden lettare å lesa, men det er ikkje nødvendig! Me bruker jo nøkkelord som **endwhile** og **endif** for å markera kvar blokkene sluttar, så i prinsippet kan alle linjer vera utan innrykk.*

**Aktivitetsforslag:** Ta utgangspunkt i *Aktivitetsforslag 2* frå førre seksjon. Presenter algoritmen med pseudokode.

