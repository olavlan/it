---
title: "Tillegg: maskinlæring"
belongs_to_chain: "Individ, samfunn og systemer"
figures_to_include:
	- "nn.svg"
---

I førre seksjon nemnde me at maskinlæring er ein viktig teknikk i moderne kunstig intelligens. Men kva er eigentleg maskinlæring? Kva meiner me når me seier at tradisjonell programmering er regelbasert, medan KI-algoritmar er datadrivne og sjølvlært? Det skal me sjå nærare på i denne seksjonen.

Sjå for deg ein funksjon med følgjande spesifikasjon:

> **Inndata:** Eit bilete som inneheld ansiktet til anten ein hund eller katt.
> **Ønskte utdata:** *Hund* dersom biletet inneheld ein hund, og *Katt* dersom biletet inneheld ein katt.

Korleis kan ein programmera ein slik funksjon? La oss først definera ein algoritme basert på regelbasert programmering, der me nyttar tradisjonelle teknikkar for biletprosessering. Regelbasert programmering er ein sekvens av klart definerte operasjonar på inndataet:

1. Finn konturar i biletet. Ein kontur er ei mengd av pikslar som representerer omrisset av eit objekt. Ei slik mengd pikslar har omtrent same intensitet og dannar ei lukka kurve. Det finst matematiske formlar som kan brukast til å finna slike mengder med pikslar.
2. Gå gjennom alle konturar i biletet, og rekn ut i kor stor grad konturane har sirkelform. Dette kan også reknast ut med  matematiske formlar.
3. Dersom det finst ein kontur som har sirkelform over ein viss grenseverdi, returner *katt*. Viss ikkje, returner *hund*.

Dette er ein svært forenkla algoritme basert på gjettinga om eit kattehovud er meir sirkelforma enn eit hundehovud. Antakeleg vil algoritmen ha låg presisjon, altså gi feil svar på ein stor del av bileta.

Maskinlæring er ein heilt annan teknikk der me **ikkje** gjer ein sekvens av klart definerte operasjonar. For å utvikla ein maskinlæringsalgoritme må me gjennomføra fire viktige steg: opprette treningsdata, opprette modell, trena opp modellen, og testa og evaluera modellen.

* **Opprette treningsdata**. Først treng me ei viss mengd data som er korrekt merka. I vårt tilfelle treng me ei mengd bilete av kattar og hundar, der kvart bilete er rett merkt med *Katt* eller *Hund*. Denne datamengda blir kalla *treningsdata*.
* **Opprette modell**. For å laga ein maskinlæringsalgoritme, definerer me først ein *modell*. Ein modell er ein matematisk struktur med parametrar som kan endrast.

Ein av dei enklaste modellane me kan definera er ein førstegradsfunksjon med fleire variablar:
$$ f(x_1, x_2, x_3, ...) = k_1 x_1 + k_2 x_2 + k_3 x_3 + ...$$

Her kan til dømes $x_1$ vera lysstyrken til den første pikselen, $x_2$ for den andre pikselen, og så vidare. Koeffisientane $k_1, k_2, ...$ er parametrane til modellen.

Målet vårt er å definera ein slik funksjon, og deretter endra parametrane på ein slik måte at funksjonen blir god til å klassifisera bilete av hundar og kattar. Treningsdataa må brukast for å endra parametrane i gunstig retning.

La oss no sjå på ein meir komplisert modell. Eit populært val av modell er nemleg nevrale nettverk. Du har kanskje høyrt om det? Eit *nevralt nettverk* er ei slags forenkling av korleis cellene i hjernen fungerer. Nettverket består av *nevronar* og *koplingar* mellom nevronar. Den eine sida av nettverket er inndatanevronar, og den andre sida er utdatanevronar. Mellom desse finst indre nevronar. Som ei forenkling kan me seia at kvart inndatanevron svarer til eit piksel i biletet, og dersom nevronet har høg verdi, så betyr det at pikselen har høg lysstyrke.

I vårt døme held det med eitt utdatanevron, som kan ha høg verdi dersom nettverket bereknar at biletet inneheld ein katt, og låg verdi viss biletet inneheld ein hund.

<img src="/media/markdowncontent/assosiated_files/nn.svg">

Korleis kan det nevrale nettverket prosessera eit bilete? Me byrjar med å setja verdiane til inndatanevronane slik at dei svarer til pikslane i biletet. Deretter blir eit signal forplanta gjennom nettverket. Kva verdiar dei indre nevrona får bestemmast ikkje berre av inndatanevronane, men også koplingane mellom nevrona. Sterke koplingar mellom nevronar betyr at høge verdiar blir forplanta lettare.

Det er styrken på koplingane som er parametrane i modellen, og som kan endrast for å gjera nettverket betre til å klassifisera bilete av hundar og kattar. Målet er å finna rett styrke på koplingane, i den forstand at når me startar med eit kattebilete, så vil signala forplanta seg slik at utdatanevronet har høg aktivering, medan når me startar med eit hundebilete, har utdatanevronet låg aktivering (nær null). Dette blir gjort med opptrening.

* **Opptrening.** Når me har definert modellen, i vårt tilfelle eit nevralt nettverk, kan me trena det opp ved å bruka treningsdataa, det vil seia bileta som allereie er korrekt merka.

Me byrjar med setja ein tilfeldig startverdi på alle koplingane, og sender det første biletet i treningsdataa gjennom nettverket. Sidan signalet no vil spreia seg på ein tilfeldig måte, så vil utdatanevronet antakeleg ha ein feil verdi. Det me no må gjera er å endra styrken til koplingane slik at nettverket gir ein litt rettare verdi. Til dømes, viss nettverket gav verdien 0.1 på eit kattebilete, så kan me endra koplingane slik at verdien blir høgare.

Det finst ein matematisk funksjon for å endra koplingane på ein slik måte at kattebiletet får høgare utdataverdi. Me kan til og med la nettverket prøva seg på mange bilete, og deretter endra koplingane slik at nettverket i snitt gir rettare verdiar på alle bileta. Når me har justert koplingane éin gong, kan me la nettverket prøva seg på nytt, og deretter justera ytterlegare. På denne måten kan nettverket bli gradvist meir presist.

Kvifor er eit nevralt nettverk betre enn regelbasert programmering? I staden for å manuelt definera eigenskapar i eit bilete, slik som konturar og grad av sirkelform, så kan eit nevralt nettverk sjølv bestemma kva som er relevante eigenskapar å trekkja ut. Styrken på dei ulike koplingane bestemmer kva som skal trekkjast ut frå pikslane i biletet, og vidare prosessering kan skje i dei indre nevronane. Sidan eit nevralt nettverk har som einaste mål å klassifisera bilete av hundar å kattar, vil han prøva å trekkja ut eigenskapar som er best eigna til å skilja hundar frå kattar. Ofte er det ikkje mogleg å forstå kva eigenskapar eit nevralt nettverk trekkjer ut.

* **Testing og evaluering.** Når me har trena det nevrale nettverket, kan me la det prøva seg på bilete det aldri har sett før, og deretter måla presisjonen for nettverket. Dersom me gir den 1000 nye bilete av hundar og kattar, og han klassifiserer 900 rett, har algoritmen ein presisjon på 90 %.

Dersom nettverket har høg nok presisjon, så kan det brukast til å merka nye bilete. Store databasar med bilete kan dermed merkast automatisk, og det minimerer manuelt arbeid. Rett nok må me tolerera at nokre bilete blir merka feil. I ulike bruksmåtar kan det vera ulike krav til presisjon.

Her har me snakka om nevrale nettverk som ein struktur beståande av nevronar og koplingar. På same måte som vår første døme på modell var ein matematisk formel, så kan eit nevralt nettverk også definerast som ein matematisk formel, rett nok meir komplisert.  Derfor krevst det i prinsippet ikkje mange kodelinjer for å laga ein algoritme basert på eit nevralt nettverk. I praksis bruker ein gjerne ein programmeringspakke, til dømes [scikit-learn](https://github.com/scikit-learn/scikit-learn) for Python, som mellom anna gjer det enkelt å oppretta nevrale nettverk og trena det opp med eigne treningsdata.

Styrken til maskinlæring ligg altså i dets evne til å læra seg relevante mønster i treningsdata, og bruka dette til å gjera prediksjonar på nytt data. Det er i prinsippet ingen grenser for kor komplekse mønster som kan kjennast igjen. Ein kan til dømes trena opp eit nevralt nettverk til å kjenna igjen ulike hunderasar i bilete! Slike bruksmåtar ville vore umogleg med regelbasert programmering.

