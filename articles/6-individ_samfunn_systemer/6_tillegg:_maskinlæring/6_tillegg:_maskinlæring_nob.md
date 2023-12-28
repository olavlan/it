---
title: "Tillegg: maskinlæring"
belongs_to_chain: "Individ, samfunn og systemer"
figures_to_include:
	- "nn.svg"
---

I forrige seksjon nevnte vi at maskinlæring er en viktig teknikk i moderne kunstig intelligens. Men hva er egentlig maskinlæring? Hva mener vi når vi sier at tradisjonell programmering er regelbasert, mens KI-algoritmer er datadrevet og selvlært? Det skal vi se nærmere på i denne seksjonen. 

Se for deg en funksjon med følgende spesifikasjon:

> **Inndata:** Et bilde som inneholder ansiktet til enten en hund eller katt.   
> **Ønsket utdata:** *Hund* dersom bildet inneholder en hund, og *Katt* dersom bildet inneholder en katt.

Hvordan kan man programmere en slik funksjon? La oss først definere en algoritme basert på regelbasert programmering, der vi benytter tradisjonelle teknikker for bildeprosessering. Regelbasert programmering er en sekvens av klart definerte operasjoner på inndataen: 

1. Finn konturer i bildet. En kontur er en mengde av piksler som representerer omrisset av et objekt. En slik mengde piksler har omtrent samme intensitet og danner en lukket kurve. Det finnes matematiske formler som kan brukes til å finne slike mengder med piksler. 
2. Gå gjennom alle konturer i bildet, og regn ut i hvor stor grad konturene har sirkelform. Dette kan også regnes ut med  matematiske formler. 
3. Dersom det finnes en kontur som har sirkelform over en viss grenseverdi, returner *katt*. Hvis ikke, returner *hund*. 

Dette er en svært forenklet algoritme basert på antagelsen om et kattehode er mer sirkelformet enn et hundehode. Antagelig vil algoritmen ha lav presisjon, altså gi feil svar på en stor andel av bildene.

Maskinlæring er en helt annen teknikk der vi **ikke** gjør en sekvens av klart definerte operasjoner. For å utvikle en maskinlæringsalgoritme må vi gjennomføre fire viktige steg: opprette treningsdata, opprette modell, trene opp modellen, og teste og evaluere modellen. 

* **Opprette treningsdata**. Først trenger vi en viss mengde data som er korrekt merket. I vårt tilfelle trenger vi en mengde bilder av katter og hunder, der hvert bilde er riktig merket med *Katt* eller *Hund*. Denne datamengden kalles *treningsdata*.
* **Opprette modell**. For å lage en maskinlæringsalgoritme, definerer vi først en *modell*. En modell er en matematisk struktur med parametre som kan endres. 

En av de enkleste modellene vi kan definere er en førstegradsfunksjon med flere variabler: 
$$ f(x_1, x_2, x_3, ...) = k_1 x_1 + k_2 x_2 + k_3 x_3 + ...$$

Her kan for eksempel $x_1$ være lysstyrken til den første pikselen, $x_2$ for den andre pikselen, og så videre. Koeffisientene $k_1, k_2, ...$ er parametrene til modellen. 

Målet vårt er å definere en slik funksjon, og deretter endre parametrene på en slik måte at funksjonen blir god til å klassifisere bilder av hunder og katter. Treningsdataene må brukes for å endre parametrene i gunstig retning.

La oss nå se på en mer komplisert modell. Et populært valg av modell er nemlig nevrale nettverk. Du har kanskje hørt om det? Et *nevralt nettverk* er en slags forenkling av hvordan cellene i hjernen fungerer. Nettverket består av *nevroner* og *koblinger* mellom nevroner. Den ene siden av nettverket er inndatanevroner, og den andre siden er utdatanevroner. Mellom disse finnes indre nevroner. Som en forenkling kan vi si at hvert inndatanevron svarer til et piksel i bildet, og dersom nevronet har høy verdi, så betyr det at pikselen har høy lysstyrke. 

I vårt eksempel holder det med ett utdatanevron, som kan ha høy verdi dersom nettverket beregner at bildet inneholder en katt, og lav verdi hvis bildet inneholder en hund. 

<img src="/media/markdowncontent/assosiated_files/nn.svg">

Hvordan kan det nevrale nettverket prosessere et bilde? Vi begynner med å sette verdiene til inndatanevronene slik at de svarer til pikslene i bildet. Deretter forplantes et signal gjennom nettverket. Hvilke verdier de indre nevronene får bestemmes ikke bare av inndatanevronene, men også koblingene mellom nevronene. Sterke koblinger mellom nevroner betyr at høye verdier forplantes lettere. 

Det er styrken på koblingene som er parametrene i modellen, og som kan endres for å gjøre nettverket bedre til å klassifisere bilder av hunder og katter. Målet er å finne riktig styrke på koblingene, i den forstand at når vi starter med et kattebilde, så vil signalene forplante seg slik at utdatanevronet har høy aktivering, mens når vi starter med et hundebilde, har utdatanevronet lav aktivering (nærme null). Dette gjøres med opptrening. 

* **Opptrening.** Når vi har definert modellen, i vårt tilfelle et nevralt nettverk, kan vi trene det opp ved å bruke treningsdataene, det vil si bildene som allerede er korrekt merket. 

Vi begynner med sette en tilfeldig startverdi på alle koblingene, og sender det første bildet i treningsdataene gjennom nettverket. Siden signalet nå vil spre seg på en tilfeldig måte, så vil utdatanevronet antagelig ha en feil verdi. Det vi nå må gjøre er å endre styrken til koblingene slik at nettverket gir en litt riktigere verdi. For eksempel, hvis nettverket ga verdien 0.1 på et kattebilde, så kan vi endre koblingene slik at verdien blir høyere. 

Det finnes en matematisk funksjon for å endre koblingene på en slik måte at kattebildet får høyere utdataverdi. Vi kan til og med la nettverket prøve seg på mange bilder, og deretter endre koblingene slik at nettverket i snitt gir riktigere verdier på alle bildene. Når vi har justert koblingene én gang, kan vi la nettverket prøve seg på nytt, og deretter justere ytterligere. På denne måten kan nettverket bli gradvist mer presist.

Hvorfor er et nevralt nettverk bedre enn regelbasert programmering? I stedet for å manuelt definere egenskaper i et bilde, slik som konturer og grad av sirkelform, så kan et nevralt nettverk selv bestemme hva som er relevante egenskaper å trekke ut. Styrken på de ulike koblingene bestemmer hva som skal trekkes ut fra pikslene i bildet, og videre prosessering kan skje i de indre nevronene. Siden et nevralt nettverk har som eneste mål å klassifisere bilder av hunder å katter, vil den forsøke å trekke ut egenskaper som er best egnet til å skille hunder fra katter. Ofte er det ikke mulig å forstå hvilke egenskaper et nevralt nettverk trekker ut. 

* **Testing og evaluering.** Når vi har trent det nevrale nettverket, kan vi la det prøve seg på bilder det aldri har sett før, og deretter måle nettverkets presisjon. Dersom vi gir den 1000 nye bilder av hunder og katter, og den klassifiserer 900 riktig, har algoritmen en presisjon på 90 %.

Dersom nettverket har høy nok presisjon, så kan det brukes til å merke nye bilder. Store databaser med bilder kan dermed merkes automatisk, og det minimerer manuelt arbeid. Riktignok må vi tolerere at noen bilder blir merket feil. I ulike anvendelser kan det være ulike krav til presisjon. 

Her har vi snakket om nevrale nettverk som en struktur bestående av nevroner og koblinger. På samme måte som vår første eksempel på modell var en matematisk formel, så kan et nevralt nettverk også defineres som en matematisk formel, riktignok mer komplisert.  Derfor kreves det i prinsippet ikke mange kodelinjer for å lage en algoritme basert på et nevralt nettverk. I praksis bruker man gjerne en programmeringspakke, for eksempel [scikit-learn](https://github.com/scikit-learn/scikit-learn) for Python, som blant annet gjør det enkelt å opprette nevrale nettverk og trene det opp med egne treningsdata. 

Styrken til maskinlæring ligger altså i dets evne til å lære seg relevante mønstre i treningsdata, og bruke dette til å gjøre prediksjoner på ny data. Det er i prinsippet ingen grenser for hvor komplekse mønstre som kan gjenkjennes. Man kan for eksempel trene opp et nevralt nettverk til å gjenkjenne forskjellige hunderaser i bilder! Slike anvendelser ville vært umulig med regelbasert programmering. 

