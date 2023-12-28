---
title: "Lagring av tall"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

Hvordan kan tall lagres på datamaskinen, altså ved å bare bruke *0* og *1*? Vi kan bruke det *binære tallsystemet*, også kalt *totallsystemet*.

Til vanlig bruker vi *titallsystemet*. Det betyr at når vi skriver et tall, for eksempel 1506, så betyr det

$$1560 = (1 \cdot \textcolor{green}{1000}) +   (5 \cdot \textcolor{green}{100})  +   (0 \cdot \textcolor{green}{10})   +   (6 \cdot \textcolor{green}{1}). $$

Tallet 1560 skal altså tolkes ved å gange hvert siffer med en potens av 10 og deretter summere leddene. I totallssystemet gjør vi akkuratdet samme, men med potenser av 2! Vi begynner derfor med å skrive opp potensene av 2: 

$2^0 = \textcolor{green}{1}$   
$2^1 = \textcolor{green}{2}$   
$2^2 = \textcolor{green}{4}$   
$2^3 = \textcolor{green}{8}$   
$2^4 = \textcolor{green}{16}$   
$2^5 = \textcolor{green}{32}$   
$2^6 = \textcolor{green}{64}$   
$2^7 = \textcolor{green}{128}$

For å skrive et tall i det binære tallsystemet, må alle sifrene være enten 0 eller 1. Et eksempel på et gyldig binært tall er 1011. Hvordan tolker vi dette tallet? Det er fire sifre, så vi trenger de fire første potensene av 2:

$$1101 \rightarrow (1 \cdot \textcolor{green}{8})  +  (1 \cdot \textcolor{green}{4})  +  (0 \cdot \textcolor{green}{2})  +  (1 \cdot \textcolor{green}{1}) = 8 + 4 + 1 = 13$$

Tallet tretten skrives altså som $1101$ i totallssystemet. Her er to andre eksempler: 

$10100 \ \ \rightarrow \quad \quad \quad \quad \ (1 \cdot \textcolor{green}{16} ) + ( 0\cdot \textcolor{green}{8} ) + ( 1\cdot \textcolor{green}{4} ) + ( 0\cdot \textcolor{green}{2} ) + ( 0\cdot \textcolor{green}{1}) = 16 + 4 \quad \ \   = 20$    
$101010 \rightarrow (1\cdot \textcolor{green}{32} ) + ( 0\cdot \textcolor{green}{16} ) + (1 \cdot \textcolor{green}{8} ) + ( 0\cdot \textcolor{green}{4} ) + ( 1 \cdot \textcolor{green}{2} ) + ( 0 \cdot \textcolor{green}{1}) = 32 + 8 + 2 = 42$   

Altså kan tallet tjue skrives som binærtallet $10100$, og førtito kan skrives som $101010$. Vi har lov til å legge på nuller i starten, så  $00010100$ er fortsatt lik 42. Nå kan vi for eksempel skrive alle tall fra 0 til 255:

$0000 0000 \rightarrow 0$   
$0000 0001 \rightarrow (1 \cdot \textcolor{green}{1}) = 1$   
$0000 0010 \rightarrow (1 \cdot \textcolor{green}{2} ) + ( 0 \cdot \textcolor{green}{1}) = 2$   
$\quad \quad \vdots$   
$1111 1111 \rightarrow (1 \cdot \textcolor{green}{128} ) + ( 1 \cdot \textcolor{green}{64} ) + ( 1 \cdot \textcolor{green}{32} ) + ( 1\cdot \textcolor{green}{16} ) + (1 \cdot \textcolor{green}{8} ) + ( 1\cdot \textcolor{green}{4} ) + ( 1 \cdot \textcolor{green}{2} ) + ( 1 \cdot \textcolor{green}{1}) = 255$

Siden $1111 1111$ er det høyeste tallet vi kan skrive med åtte bits, trenger vi en ekstra bit for å skrive det neste tallet, som er 256:

$1 0000 0000 \rightarrow (256 \cdot \textcolor{green}{1}) = 256$

Ser du mønsteret? Med åtte bits bruker vi potensene 1, 2, 4, 8, 16, 32, 64 og 128. Da kan vi skrive alle tall opp til den neste potensen, som er 256. 

Antall tall vi kan skrive med åtte bits er altså $2^8 = 256$. På samme måte kan vi komme fram til at antall tall vi kan skrive med ni bits er $2^9 = 512$. Du har kanskje hørt at moderne datamaskiner har 64-bits prosessorer? Det betyr blant annet at tall lagres med 64 bits. Antall tall vi kan skrive med 64 bits er $2^{64}\approx 1.8\cdot 10^{19}$!

**Finne binærformen til et tall.** Hvordan kan vi skrive et vilkårlig tall i det binære tallsystemet? Vi skal nå vise stegene for å skrive tallet 84 i det binære tallsystemet. 

Vi skriver  opp potensene av 2, helt fram til det første tallet som er høyere enn 84:
$$1, 2, 4, 8, 16, 32, 64, 128 \quad \vert \quad 84$$
Vi skal nå plukke ut potenser av 2 som til sammen blir 84. 
Til høyre skriver vi hvor mye vi mangler. 
Foreløpig har vi ikke tatt med noen potenser, så vi mangler 84. 
Først tar vi med det høyest mulige tallet, som er 64. Etter å ha tatt med 64, mangler vi 20 for å komme til 84:
$$1, 2, 4, 8, 16, 32, \cancel{64}, 128 \quad \vert \quad \cancel{84} \ {20}$$
Hva er det høyeste mulige tallet vi kan ta med nå? Vi kan ta med 16, og da mangler vi bare 4:
$$1, 2, 4, 8, \cancel{16}, 32, \cancel{64}, 128 \quad \vert \quad \cancel{84} \ \cancel{20} \ 4$$
Nå kan vi ta med 4, og da mangler vi ingenting!
$$1, 2, \cancel{4}, 8, \cancel{16}, 32, \cancel{64}, 128 \quad \vert \quad \cancel{84} \ \cancel{20} \ \cancel{4} \ 0$$
Siden det står 0 på høyere side, har vi nå funnet tallene som til sammen blir 84! La oss skrive opp potensene i motsatt rekkefølge og markere tallene vi har tatt med i grønt: 
$$\textcolor{green}{64}, 32, \textcolor{green}{16}, 8, \textcolor{green}{4}, 2, 1$$
Nå kan vi oversette dette til en bitstreng! Tallene i grønt skrives som 1, og de andre tallene skrives som 0:
$$\textcolor{green}{1}0\textcolor{green}{1}0\textcolor{green}{1}00$$
Kan du dobbeltsjekke at $1010100$ blir 84, ved å gå den andre veien?

I denne seksjonen har vi vist hvordan man oversetter mellom titallssystemet og totallssystemet. Det er lurt å vite hvordan disse utregningene gjøres, men i de neste seksjonene kan du gjerne bruke en kalkulator, som for eksempel [Bin2Dec](https://eliasbiondo.github.io/bin2dec/).

**Aktivitetsforslag.**
1. Tell fra 0 til 15 med det binære tallsystemet. Skriv alle binærtallene med fire siffer.
2. Hvor mange tall kan du skrive med ti bits?
3. Hvor mange bits trenger du for å skrive tallet 2000?
4. Gjør oppgavene som er generert under. Du skal gjøre utregningene for hånd, men etterpå kan du sjekke svarene dine med [Bin2Dec](https://eliasbiondo.github.io/bin2dec/).


```python
from random import randint
print("a. Oversett følgende binærtall:")
for i in range(5):
    s = ""
    for i in range(8): 
        s += str(randint(0,1))
    print(s)
print()
print("b. Skriv følgende tall som binærtall:") 
for i in range(5):
    print(str(randint(0,255)))
```

    a. Oversett følgende binærtall:
    00001000
    01001000
    10100110
    01010000
    00110001
    
    b. Skriv følgende tall som binærtall:
    133
    204
    200
    128
    64


