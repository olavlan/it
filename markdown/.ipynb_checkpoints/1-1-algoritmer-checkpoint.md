# Introduksjon og måter å presentere algoritmer

## Hva er en algoritme? 

Sagt på en enkel måte, er en algoritme en oppskrift på hvordan noe skal gjøres.

Mer presist: En algoritme er en fullstendig og nøyaktig beskrivelse av fremgangsmåten for å løse en oppgave. Algoritmen angir de enkelte skrittene i oppgaveløsningen og rekkefølgen av dem ved ord, matematisk symbolikk og/eller skjematisk fremstilling av arbeidsgangen.

En oppskrift på en matrett er et eksempel på en algoritme. Du følger oppskriften trinn for trinn til matretten er ferdig. Du benytter kunnskapen, det vil si oppskriften – algoritmen – for å løse den oppgaven du står overfor. Til slutt står du igjen med en ferdig matrett. 

Når du bruker offentlig transport søker du gjerne opp en reisevei på en app. Appen gir deg en oppskrift - en algoritme - på hvordan du skal komme deg til ønsket destinasjon. Du følger oppskriften trinn for trinn til du har kommet frem.

Vi kan prøve å sette opp en algoritme for hvordan man vasker klær:

1. Legg klærne i vaskemaskinen
2. Sett temperatur som passer til klærne
3. Hell i vaskepulver
4. Start maskinen
5. Når maskinen er ferdig, heng klærne til tørk
6. Når klærne er tørre, legg dem i skapet

Denne beskrivelsen er egentlig ikke fullstendig nok. En algoritme skal være så fullstendig og nøyaktig at en som aldri har gjort det før, og som ikke har noe kreativitet eller evne til problemløsning, skal klare det uten hjelp. For hvordan skal klærne legges i skapet? Her må vi ha betingelser. Om det er en skjorte, skal den henges opp. Om det er en T-skjorte, skal den brettes og legges sammen med de andre T-skjortene. Og så videre. 

Dette eksemplet viser at selv enkle hverdagsoppgaver kan være nokså kompliserte, og at vi mennesker kan veldig mange algoritmer uten at vi tenker over det. Vi utfører disse i vårt dagligliv for å oppnå oppgavene vi står ovenfor. Men når man prøver å skrive dem ned blir det fort komplisert.

**Aktivitetsforslag:** Skriv ned en algoritme for noe du gjør regelmessig. Når skrevet algoritmen, svar på følgende:
* I hvor stor grad kreves kreativitet og problemløsning for å gjennomføre stegene?
* Kan du gjøre algoritmer mer presis og fullstendig, slik at dette ikke kreves? 

## Problemer som kan løses med algoritmer

Hvilke type problemer kan løses med en algoritme? La oss tenke på følgende problem: 

> Reparere sykkelen

Dette problemet er ikke tydelig definert. For hvilken sykkel er det snakk om? Hva er galt med sykkelen? Og når kan vi regne sykkelen som "reparert"? 

En måte å være presise på, er å definere utgangspunktet og ønsket resultat:

> **Problem** *Reparere sykkel*   
**Utgangspunkt:** En sykkel $S$ med punktert hjul.    
**Ønsket resultat:** At sykkelen $S$ ikke har noen punkterte hjul. 

Her har vi definert problemet på en måte som ikke kan misforstås: 

* Vi har gitt navn til objektet som problemet handler om, slik at vi kan referere entydig til objektet. Det er vanlig å bruke store bokstaver som navn på objekter. 
* Istedenfor å definere hva verbet "reparere" betyr, har vi gitt en presis beskrivelse av hva som er ønsket sluttresultat. 

Merk at denne definisjonen ikke sier noe om hvordan problemet kan løses. For å løse et problem må vi lage en algoritme som kan gjøre om startsituasjonen til det ønskede resultatet.

Når vi skriver en slik algoritme, må vi huske at $S$ kan være en hvilken som helst sykkel. Et steg i algoritmen kan for eksempel være "ta av det punkterte hjulet på sykkelen $S$". Her er det viktig at steget fungerer på alle sykler, ikke bare en spesifikk sykkel!

Det kan finnes mange algoritmer for å løse et bestemt problem. For å løse problemet *Reparere sykkel* kan én algoritme være å lappe dekket, mens en annen algoritme kan være å skifte dekket. 

Som et annet eksempel kan vi gi en definisjon av problemet "å vaske klær":

> **Problem** *Vaske klær*    
**Utgangspunkt:** En mengde klær $K$ og et skap $S$.   
**Ønsket resultat:** At klærne $K$ er rene, tørre, brettet og lagt i skapet $S$.

Merk at dette problemet har flere relevante objekter, og vi har gitt navn til alle. 

Her burde man kanskje ha definert hva som kreves for å kalle et klesplagg "rent", men siden problemet skal løses av mennesker, kan vi tillate oss å ikke definere alle ord. Vi må derimot være helt presise når vi definerer problemer som skal løses av en datamaskin, som er tema for neste seksjon!

**Aktivitetsforslag:** Tenk over en oppgave du gjør regelmessig, for eksempel å lage matpakke eller skifte sengetøy. Hvilket problem står du ovenfor før du tar fatt på oppgaven? Skriv en presis definisjon av problemet, altså hva som er utgangspunktet og hva som er ønsket resultat. Forsøk å gi navn til de relevante objektene i problemet. 

## Datamaskinproblemer

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

## Beskrive algoritmer med ord

Vi skal nå beskrive en algoritme for å finne det største tallet i en liste $L$. La oss se på et konkret eksempel, nemlig lista $[3.14, \ 1, \ 4.7, \ 0, \ 2]$. Lista har fem tall, og vi trenger en algoritme som finner det høyeste tallet.

Som mennesker ser vi umiddelbart at $4.7$ er det høyeste tallet i lista, men hvordan kan vi komme fram til dette på en strukturert måte som alltid fungerer? Vi kan gå gjennom lista, fra det første til det siste tallet, mens vi underveis holder styr på det største tallet vi har funnet. Følgende tabell viser hvordan denne metoden fungerer: 

| Neste element i lista | 3.14 | 1    | 4.7 | 0   | 2   |
|-----------------------|------|------|-----|-----|-----|
| Hittil høyeste tall   | 3.14 | 3.14 | 4.7 | 4.7 | 4.7 |

I hvert steg sammenligner vi det neste tallet i lista med det hittil største tallet vi har funnet. La oss presentere denne algoritmen:

> **Algoritme** *Finn største tall*    
**Inndata:** En liste $L$ av desimaltall    
**Utdata:** Det største tallet $s$ i lista $L$
> 
> 1. Sett $s$ til å være det første tallet i lista $L$.
> 2. Sammenlign $s$ med det neste tallet i $L$. Dersom det neste tallet er større, sett $s$ til denne verdien. 
> 3. Dersom $L$ har flere elementer, gjenta steg 2.
> 4. Returner $s$. 

Legg merke til at vi har tatt med følgende informasjon om algoritmen:

* Vi har gitt algoritmen et navn, nemlig *Finn største tall*
* Vi har definert inndata og utdata for algoritmen
* Til slutt har vi skrevet stegene for algoritmen

Dette er en oversiktlig måte å presentere en algoritme på. 

Legg også merke til hvordan vi bruker variabelen $s$ til å holde styr på hva som er det hittil høyeste tallet i lista. La oss bruke algoritmen på lista $[1,2,3,2,1,4,3,5]$. Følgende tabell viser hvordan $s$ oppdateres etter hvert som vi går gjennom lista: 

|  Neste tall i lista   | 1 | 2 | 3 | 2 | 1 | 4 | 3 | 5 |
|-----|---|---|---|---|---|---|---|---|
| $s$ | 1 | 2 | 3 | 3 | 3 | 4 | 4 | 5 |

**Aktivitetsforslag 1:** Utfør algoritmen *Finn største tall* på listene som er generert nedenfor. Du skal altså tenke over hva som skjer ved hvert steg, og skrive ned hvordan variabelen $s$ endrer seg underveis. Hvilken verdi returneres av algoritmen?


```python
from random import randint

for i in range(3):
    random_list = [randint(0,10) for i in range(10)]
    print(random_list)
```

    [6, 2, 4, 0, 7, 2, 8, 7, 3, 7]
    [10, 7, 5, 8, 5, 7, 7, 6, 3, 2]
    [4, 4, 10, 1, 1, 1, 5, 0, 0, 9]


**Aktivitetsforslag 2:** Gå inn på et program du nylig har kodet. Finn en funksjon med minst en parameter og returverdi (dersom du ikke har en slik funksjon, forsøk å sette noe av koden din inn i en funksjon). Hvilket problem løser funksjonen? Presenter algoritmen som løser problemet. Du skal altså skrive med ord hvilke steg koden din utfører.

## Beskrive algoritmer med pseudokode

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

## Beskrive algoritmer med flytdiagram

Vi har allerede sett på flytdiagrammer i kapittelet *Konsepter i objektorientert programmering*. Nå skal vi se på hvordan vi kan presentere algoritmer med flytdiagram. 

Når vi skal tegne et flytdiagram, plasserer vi stegene i bokser, og bruker piler til å vise *flyten* mellom stegene, altså hvordan man går fra et steg til det neste. Vi kan godt velge om vi vil bruke ord, pseudokode eller programkode i boksene. 

Hvordan kan vi oversette algoritmen *Finn største tall* til et flytdiagram? Det er ofte lurt å ta utgangspunkt i pseudokoden, fordi vi da kan oversette hver linje til en boks. La oss begynne med de to første linjene: 

>**set** $s$ **to** $L[0]$   
**set** $i$ **to** $1$

Hver av disse linjene er en *operasjon* eller en *prosess*, og disse skal plasseres i **prosessbokser**. Vi tegner disse som rektangulære bokser:

<img src="../fig2/algoritmer_flytdiagram1.svg">

I dette tilfellet har vi valgt å plassere begge operasjonene i én felles boks, men de kunne også vært i hver sin boks. 

Den neste linjen i pseudokoden er:

>**while** $i$ **smaller than**  $n $

Her må vi ha en forgrening i flytdiagrammet! Dersom $i$ er mindre enn $n$ skal vi gå inn i en løkke, og når $i$ ikke er mindre enn $n$, skal vi gå ut av løkken:

<img src="../fig2/algoritmer_flytdiagram2.svg">

For å teste om noe er sant har vi brukt en **valgboks**, som tegnes med diamantform. Siden testen ble gjort av en **while**-setning, skal det være to piler som går ut av boksen; den ene pilen skal lede til en løkke og den andre pilen skal lede videre i diagrammet. 

Det neste vi må gjøre er å lage boksene som skal være inni løkka. Pseudokoden er:

>&emsp;**if** $L[i]$ **greater than** $s$   
&emsp;&emsp;**set** $s$ **to** $L[i]$    
&emsp;**endif**   
&emsp;**set** $i$ **to** $i + 1$

I løkka skal vi altså gjøre en ny test, nemlig å sjekke om $L[i]$ er større enn $s$. Igjen tegner vi testen med en valgboks, og en pil for hvert av utfallene:

<img src="../fig2/algoritmer_flytdiagram3.svg">

Dersom testen har positivt svar, skal vi altså oppdatere variabelen $s$, og deretter gå til det neste steget. Dersom testen har negativt svar, skal vi gå rett til det neste steget. 

Den siste operasjonen i løkka er å øke iterasjonsvariabelen $i$. Vi må alltid huske denne operasjonen når vi tegner løkker; som vi skal se i neste seksjon, gjelder dette også **for**-løkker.

De to siste linjene i pseudokoden er:

>**endwhile**     
**return** $s$ 

Dette forteller hva vi skal gjøre når vi kommer ut av **while**-løkka. Den siste linja forteller egentlig hva som er utdata for algoritmen. Inndata og utdata for en algoritme settes i **databokser**, som tegnes med parallellogrammer. Databoksene er det som gjenstår for å fullføre flytdiagrammet:  

>**Algoritme** *Finn største tall*
>
><img src="../fig2/algoritmer_flytdiagram.svg">

For å utføre algoritmen starter vi på boksen *Inndata* og følger pilene helt til vi kommer til boksen *Utdata*. I oppgaven nedenfor kan du selv gå gjennom flytdiagrammet med noen tilfeldig genererte lister.

**Aktivitetsforslag 1:** Utfør algoritmen *Finn største tall* på listene som er generert nedenfor. Du skal utføre algoritmen ved å gå gjennom flytdiagrammet. I hver valgboks må du avgjøre gren du skal følge videre i diagrammet. Du bør skrive ned hvilken verdi variablene $i$ og $s$ har til enhver tid. 


```python
from random import randint

for i in range(3):
    random_list = [randint(0,10) for i in range(10)]
    print(random_list)
```

    [6, 9, 3, 1, 5, 8, 9, 3, 4, 6]
    [4, 4, 1, 2, 5, 5, 10, 3, 8, 5]
    [8, 7, 1, 9, 3, 5, 7, 4, 7, 3]


**Aktivitetsforslag 2:** Ta utgangspunkt i *Aktivitetsforslag 2* fra seksjonen *Beskrive algoritmer med ord*. Presenter algoritmen med flytdiagram.  

## Mer om pseudokode og flytdiagram

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

<img src="../fig2/algoritmer_flytdiagram_for.svg">

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
><img src="../fig2/algoritmer_flytdiagram_if.svg">

Merk at hvis den første testen gir positivt svar, hopper vi over de neste testene. Det er kun når en test gir negativt svar at vi fortsetter til den neste testen. Ved å følge samme mønster som over, kan du tegne vilkårlig store **if**-**else**-setninger. 

**Aktivitetsforslag:** Gå inn på et program du nylig har skrevet og velg noen kodelinjer som inneholder løkker og betingelser. Omform koden til både pseudokode og flytdiagram.  
