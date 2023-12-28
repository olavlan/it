---
title: "Lagring av tegn med UTF-8"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I dag har datamaskinene blitt mye kraftigere, noe som tillater oss å bruke lengre bitkoder, og dermed ha mange flere tegn. *ASCII* har derfor blitt erstattet av en ny standard som heter *UTF-8*. Hvor mange tegn finnes i den nye standarden? I 2023 hadde omtrent 150.000 tegn fått sin *UTF-8*-kode. men hvert år utvides standarden med nye tegn, og det finnes nok bitkoder til over 1 million tegn!

Egentlig finnes flere lignende standarder (*UTF-8*, *UTF-16* og *UTF-32*) som har samlebetegnelsen *Unicode* (navnet kommer fra *universal encoding*). Forskjellen på de ulike versjonene er lengden på bitkodene. Med *UTF-8* blir et tegn kodet som en *bytesekvens*. En *byte* består av åtte bit, så et eksempel på en bytesekvens er:

```11100010 10000010 10101100```

Størrelsen på denne bitstrengen er altså tre bytes. I *UTF-16* brukes ikke bytes, men blokker på 16 bits. 

Grunnen til *UTF-8* er den mest populære standarden, er at alle de 128 *ASCII*-tegnene kan lagres med bare én byte! Det betyr at alle de latinske bokstavene og de vanligste spesialtegnene kan lagres med samme korte bitkode som *ASCII* bruker.

Teksten du nå leser er antagelig kodet med *UTF-8*, og nesten alle tegnene vi bruker her trenger bare én byte! Dersom teksten hadde blitt skrevet på et språk som bruker et annet alfabet, ville kanskje *UTF-16* vært mer plassbesparende. 

Måten *UTF-8* gir bitkoder til tegn fungerer litt annerledes enn *ASCII*. Som eksempler skal vi bruke bokstaven *s* og eurotegnet *€*.

**Steg 1.** Alle tegn i *Unicode* får tildelt et unikt tall mellom 0 og 1.114.111. Tegnene *s* og *€* har fått følgende tall: 

*s*: 115   
*€*: 8364   

Vi sier at 101 er *kodepunktet* til *s* (*code point* på engelsk). De vanligste tegnene har gjerne lavere kodepunkter, så det er naturlig at *€* har et høyere kodepunkt enn *s*. 

**Steg 2.** Nå må vi avgjøre hvor mange bytes vi trenger for å skrive tegnet. Det kan vi finne ut med følgende tabell:

| Kodepunkt | Antall bytes |
|-----------|--------------|
| 0 - 127        | 1           |
| 128 - 2047         | 2           |
| 2048 - 65.535         | 3           |
| 65.536 - 1.114.111        | 4           |

Hvor mange bytes trenger vi for å skrive *s*, og hvor mange trenger vi for å skrive *€*?

Siden teksten du nå leser er skrevet med *UTF-8*, betyr det den lagret som en sekvens av bytes. Men hvordan kan datamaskinen vite om det neste tegnet er skrevet med én byte eller tre bytes?

* Dersom en byte starter med $\textcolor{green}{0}$, så har vi kommet til et tegn som er skrevet med én byte. 
* Dersom en byte starter med $\textcolor{green}{110}$, så har vi kommet til et tegn som er skrevet med to bytes. 

Nå skjønner du sikkert hva det betyr dersom en byte starter med $\textcolor{green}{110}$ eller $\textcolor{green}{1110}$? 

Den siste regelen er: 

* Dersom en byte starter med $\textcolor{green}{10}$, så er det ikke et nytt tegn, men fortsettelsen av bitkoden til det forrige tegnet.

**Steg 3.** Nå kan vi lage en tabell med all informasjon vi har så langt:

| Tegn | Kodepunkt | Antall bytes  | *UTF-8*-kode |
|-----------|--------------|---|---|
| *s*        | 115           | 1  |  $\textcolor{green}{0}xxxxxxx$ |
| *€*         | 8364           |  3 | $\textcolor{green}{1110}xxxx \ \textcolor{green}{10}xxxxxx \ \textcolor{green}{10}xxxxxx$ |

Vi har altså brukt reglene ovenfor til å fylle ut så mye av *UTF-8*-koden som mulig. Hva skal vi fylle inn i stedet for $x$-ene? Vi skal rett og slett skrive kodepunktet til tegnet, oversatt til det binære tallsystemet!

Kodepunktet til *s* er 115, som i det binære tallsystemet er $1110011$. Dermed blir *UTF-8*-koden $\textcolor{green}{0}1110011$. 

Kodepunktet til *€* er 8364, som i det binære tallsystemet er $0010 \ 000010 \ 101100$. Dermed blir *UTF-8*-koden $\textcolor{green}{1110}0010 \ \textcolor{green}{10}000010 \ \textcolor{green}{10}101100$. Merk hvordan vi har fordelt det binære tallet i tre deler, og at vi måtte legge til to nuller i starten for å fylle opp alle $x$-ene. 

Selv om du ikke vil få bruk for å oversette tegn til *UTF-8*-koder, er det nyttig å kjenne til systemet. Som en oppsummering kan vi si at alle tegn har et kodepunkt, altså et tall mellom 0 og 1.114.111. Dette kodepunktet kan oversettes til en *UTF-8*-kode bestående av 1-4 bytes. Tegn med lave kodepunkt kan skrives med færre bytes. 

*Når man søker opp hva et tegn er i Unicode, er svaret man får noe slikt som U+20AC. Dette er egentlig bare kodepunktet til tegnet, men skrevet på en spesiell måte:* 
1. *U+ er bare for å markere at det er Unicode som er brukt.*
2. *Hvert tall kan oversettes til det binære tallsystemet. Bokstavene A-F er tallene 10-15, som også kan oversettes til det binære tallsystemet:*
    * *2: 0010*
    * *0: 0000*
    * *A: 1010*
    * *C: 1100*
3. *Til slutt plasseres disse i sekvens: 0010 0000 1010 1100. Dette er tallet 8364 skrevet i det binære tallsystemet. Dermed kan vi konkludere med at U+20AC er tegnet med kodepunkt 8364, altså €.*

**Aktivitetsforslag 1:** Gå inn på [UTF-8 Tool](https://www.cogsci.ed.ac.uk/~richard/utf-8.cgi?mode=char) og søk på de dansk-norske bokstavene *æ*, *ø* og *å*. Hva er kodepunktet til bokstavene? Du finner kodepunktet i feltet *Decimal code point*. Kan du finne *UTF-8-koden* til disse bokstavene ved å følge stegene beskrevet i denne seksjonen? 

**Aktivitetsforslag 2.** Gå inn på [UTF-8 Tool](https://www.cogsci.ed.ac.uk/~richard/utf-8.cgi?mode=decimal) og søk på forskjellige kodepunkter, både veldig lave og veldig høye tall (det høyeste er omtrent 150.000 i 2023). Forsøk gjerne mange tall mellom 0 og 2000, som er de mest vanlige tegnene. Kan du finne ulike grupper av tegn? 
