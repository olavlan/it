---
title: "Lagring av tal"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

Korleis kan tal lagrast på datamaskina, altså ved å berre bruka *0* og *1*? Me kan bruka det *binære talsystemet*, også  *kalla *totalsystemet*.

Til vanleg bruker me *titalssystemet*. Det betyr at når me skriv eit tal, til dømes 1506, så betyr det

$$1560 = (1 \cdot \textcolor{green}{1000}) +   (5 \cdot \textcolor{green}{100})  +   (0 \cdot \textcolor{green}{10})   +   (6 \cdot \textcolor{green}{1}). $$

Talet 1560 skal altså tolkast ved å ganga kvart siffer med ein potens av 10 og deretter summera ledda. I totalsystemet gjer me akkuratdet same, men med potensar av 2! Me byrjar derfor med å skriva opp potensane av 2:

$2^0 = \textcolor{green}{1}$   
$2^1 = \textcolor{green}{2}$   
$2^2 = \textcolor{green}{4}$   
$2^3 = \textcolor{green}{8}$   
$2^4 = \textcolor{green}{16}$   
$2^5 = \textcolor{green}{32}$   
$2^6 = \textcolor{green}{64}$   
$2^7 = \textcolor{green}{128}$

For å skriva eit tal i det binære talsystemet, må alle siffera vera anten 0 eller 1. Eit døme på eit gyldig binært tal er 1011. Korleis tolkar me dette talet? Det er fire siffer, så me treng dei fire første potensane av 2:

$$1101 \rightarrow (1 \cdot \textcolor{green}{8})  +  (1 \cdot \textcolor{green}{4})  +  (0 \cdot \textcolor{green}{2})  +  (1 \cdot \textcolor{green}{1}) = 8 + 4 + 1 = 13$$

Talet tretten blir altså skrivne som $1101$ i totalsystemet. Her er to andre døme:

$10100 \ \ \rightarrow \quad \quad \quad \quad \ (1 \cdot \textcolor{green}{16} ) + ( 0\cdot \textcolor{green}{8} ) + ( 1\cdot \textcolor{green}{4} ) + ( 0\cdot \textcolor{green}{2} ) + ( 0\cdot \textcolor{green}{1}) = 16 + 4 \quad \ \   = 20$
$101010 \rightarrow (1\cdot \textcolor{green}{32} ) + ( 0\cdot \textcolor{green}{16} ) + (1 \cdot \textcolor{green}{8} ) + ( 0\cdot \textcolor{green}{4} ) + ( 1 \cdot \textcolor{green}{2} ) + ( 0 \cdot \textcolor{green}{1}) = 32 + 8 + 2 = 42$

Altså kan talet tjue skrivast som binærtallet $10100$, og førtito kan skrivast som $101010$. Me har lov til å leggja på null i starten, så  $00010100$ er framleis lik 42. No kan me til dømes skriva alle tal frå 0 til 255:

$0000 0000 \rightarrow 0$
$0000 0001 \rightarrow (1 \cdot \textcolor{green}{1}) = 1$
$0000 0010 \rightarrow (1 \cdot \textcolor{green}{2} ) + ( 0 \cdot \textcolor{green}{1}) = 2$
$\quad \quad \vdots$
$1111 1111 \rightarrow (1 \cdot \textcolor{green}{128} ) + ( 1 \cdot \textcolor{green}{64} ) + ( 1 \cdot \textcolor{green}{32} ) + ( 1\cdot \textcolor{green}{16} ) + (1 \cdot \textcolor{green}{8} ) + ( 1\cdot \textcolor{green}{4} ) + ( 1 \cdot \textcolor{green}{2} ) + ( 1 \cdot \textcolor{green}{1}) = 255$

Sidan $1111 1111$ er det høgaste talet me kan skriva med åtte bitar, treng me ein ekstra bit for å skriva det neste talet, som er 256:

$1 0000 0000 \rightarrow (256 \cdot \textcolor{green}{1}) = 256$

Ser du mønsteret? Med åtte bitar bruker me potensane 1, 2, 4, 8, 16, 32, 64 og 128. Då kan me skriva alle tal opp til den neste potensen, som er 256

Talet på tal me kan skriva med åtte bitar er altså $2^8 = 256$. På same måte kan me komma fram til at talet på tal me kan skriva med ni bitar er $2^9 = 512$. Du har kanskje høyrt at moderne datamaskiner har 64-bits prosessorar? Det betyr mellom anna at tal blir lagra med 64 bitar. Talet på tal me kan skriva med 64 bitar er $2^{64}\approx 1.8\cdot 10^{19}$!

**Finne binærformen til eit tal.** Korleis kan me skriva eit vilkårleg tal i det binære talsystemet? Me skal no visa stega for å skriva talet 84 i det binære talsystemet.

Me skriv opp   potensane av 2, heilt fram til det første talet som er høgare enn 84:
$$1, 2, 4, 8, 16, 32, 64, 128 \quad \vert \quad 84$$
Me skal no plukka ut potensar av 2 som til saman blir 84
Til høgre skriv me kor mykje me manglar.
Førebels har me ikkje teke med nokon potensar, så me manglar 84
Først tek me med det høgast moglege talet, som er 64. Etter å ha teke med 64, manglar me 20 for å komma til 84:
$$1, 2, 4, 8, 16, 32, \cancel{64}, 128 \quad \vert \quad \cancel{84} \ {20}$$
Kva er det høgaste moglege talet me kan ta med no? Me kan ta med 16, og då manglar me berre 4:
$$1, 2, 4, 8, \cancel{16}, 32, \cancel{64}, 128 \quad \vert \quad \cancel{84} \ \cancel{20} \ 4$$
No kan me ta med 4, og då manglar me ingenting!
$$1, 2, \cancel{4}, 8, \cancel{16}, 32, \cancel{64}, 128 \quad \vert \quad \cancel{84} \ \cancel{20} \ \cancel{4} \ 0$$
Sidan det står 0 på høgare side, har me no funne tala som til saman blir 84! La oss skriva opp potensane i motsett rekkjefølgje og markera tala me har teke med i grønt:
$$\textcolor{green}{64}, 32, \textcolor{green}{16}, 8, \textcolor{green}{4}, 2, 1$$
No kan me omsetja dette til ein bitstreng! Tala i grønt blir skrivne som 1, og dei andre tala blir skrivne som 0:
$$\textcolor{green}{1}0\textcolor{green}{1}0\textcolor{green}{1}00$$
Kan du dobbeltsjekka at $1010100$ blir 84, ved å gå den andre vegen?

I denne seksjonen har me vist korleis ein omset mellom titalssystemet og totalsystemet. Det er lurt å vita korleis desse utrekningane blir gjorde, men i dei neste seksjonane kan du gjerne bruka ein kalkulator, som til dømes [Bin2Dec](https://eliasbiondo.github.io/bin2dec/).

**Aktivitetsforslag.**
1. Tell frå 0 til 15 med det binære talsystemet. Skriv alle binærtallene med fire siffer.
2. Kor mange tal kan du skriva med ti bitar?
3. Kor mange bitar treng du for å skriva talet 2000?
4. Gjer oppgåvene som er genererte under. Du skal gjera utrekningane for hand, men etterpå kan du sjekka svara dine med [Bin2Dec](https://eliasbiondo.github.io/bin2dec/).


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

a. Oversett følgjande binærtall:
    00001000
    01001000
    10100110
    01010000
    00110001
    
b. Skriv følgjande tal som binærtall:
    133
    204
    200
    128
    64


