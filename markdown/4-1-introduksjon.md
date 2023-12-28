# Datahåndtering

## Begreper

Vi skal nå se på noen viktige begreper knyttet til data og datahåndtering. Siden dette er vanskelige begreper, skal vi ikke forsøke å gi presise definisjoner, men heller gi eksempler som kan være til hjelp. 

**Hva er *informasjon*?** 

Dersom vi står i tett tåke, kan vi ikke si mye om det vi ser rundt oss. Vi kan derfor argumentere for at tåke ikke inneholder noe *informasjon*. Men dersom litt av tåka forsvinner og vi kan se omrisset av et hus, så har vi plutselig struktur i synsinntrykket. 

Hva mener vi med *struktur*? Struktur, eller mønster, er rett og slett noe som ikke er helt tilfeldig. Vannmolekylene i en tåkesky svever kanskje tilfeldig rundt i lufta, men materialet i et hus er langt fra tilfeldig! Et murhus består av leire som har blitt formet som rektangulære klosser og deretter satt oppå hverandre på en bestemt måte; her er det mye struktur og mønster. 

Der det finnes struktur, finnes også informasjon. For eksempel kan vi beskrive hvordan leira er formet som mursteiner med en bestemt lengde, bredde og høyde. Informasjon kan altså sees på som en beskrivelse av struktur og mønstre. 
    
**Hva er *data*?** 

Informasjon kan formidles på forskjellige måter. *Data* er en måte å beskrive struktur gjennom *konkrete verdier*. For eksempel kan vi beskrive et murhus ved å oppgi konkrete størrelsesmål: 


```python
murstein_lengde = 25
murstein_bredde = 10
murstein_hoyde = 10
```

Men en konkret verdi trenger ikke å være et tall; vi kan også oppgi formen på hustak ved å definere forskjellige kategorier:


```python
hus1_tak = "skrått"
hus2_tak = "flatt"
hus3_tak = "skrått"
```

Vi bør likevel huske på at alle data lagres som tall; hver bokstav lagres som et tall i datamaskinen, så ordet "skrått" er egentlig en sekvens av tall, og ordet "flatt" er en annen tallsekvens. Siden alt likevel lagres som tall, kunne vi først laget en liste med kategoriene, og deretter brukt indeksene i lista for å registrere spesifikke hus: 


```python
kategorier_hustak = ["skrått", "flatt"]

hus1_tak = 0
hus2_tak = 1
hus3_tak = 0
```

Ved å definere en slik *assossiasjon* mellom tall og kategorier sparer vi plass i datamaskinens minne, siden vi bare trenger å skrive det fulle navnet på kategorien én gang.

**Hva er *datahåndtering*?** 

Når vi snakker om *datahåndtering*, mener vi alt man kan gjøre med data! Vi kan dele inn datahåndtering i to hovedkategorier:

* Håndtere data i sin originale form: *lagring*, *sikring* og *utveksling* av data
* Omforme data til meningsfull informasjon: *databehandling*

Som en oppsummering av denne seksjonen kan vi tenke oss et system for værvarsling: 

1. I atmosfæren kan det finnes områder med høyere trykk og områder med lavere trykk. Trykket i atmosfæren er altså ikke noe helt tilfeldig, men har *mønster* og *struktur*.
2. Når vi beskriver strukturen i atmosfæren, har vi *informasjon*. Et eksempel på informasjon kan være at "det er høyere trykk i Oslo enn i Bergen i dag". 
3. Vi kan også beskrive atmosfæren med *data*; målestasjoner på forskjellige geografiske punkter kan ha sensorer som måler trykk, fuktighet, temperatur og annet. Siden en måling består av konkrete tallverdier, har vi data. 
4. Måledataene kan i første omgang lagres på målestasjonen, og deretter sendes til et datasenter. Det er et eksempel på *lagring og utveksling* av data. I disse stegene håndterer vi måledataene i sin originale form; slike data kalles gjerne *rådata*, fordi de ikke har gjennomgått noen form for bearbeiding.
5. På datamaskinene kan måledata fra hele landet brukes til å gjøre simuleringer, det vil si å beregne hvordan atmosfæren kommer til å utvikle seg de neste dagene. I dette steget blir måledataene brukt som parametre i funksjoner, og returverdier kommer ut. Returverdiene kan til slutt analyseres og presenteres i form av en værmelding. Alt dette er *databehandling*; vi omformer de originale måledataene til meningsfull og nyttig informasjon. 

## *Oslo bysykkel*

For å vise hvor spennende datahåndtering kan være, skal vi ta utgangspunkt i data fra *Oslo Bysykkel*, som har 259 selvbetjente sykkelstasjoner i Oslo (i April 2023); du kan se alle sykkelstasjonene på [dette kartet](https://oslobysykkel.no/stasjoner). Når en person låser opp en sykkel på en stasjon A, og leverer den på stasjon B, så har det blitt registrert en tur fra A til B. Følgende tur ble registrert den 26. April 2023: 

```json
{
        "started_at": "2023-04-29 12:10:38.207000+00:00",
        "ended_at": "2023-04-29 12:14:34.256000+00:00",
        "duration": 236,
        "start_station_id": "463",
        "start_station_name": "Schous plass trikkestopp",
        "start_station_description": "ved biblioteket",
        "start_station_latitude": 59.9207284,
        "start_station_longitude": 10.7594857,
        "end_station_id": "437",
        "end_station_name": "Sentrum Scene",
        "end_station_description": "ved Arbeidersamfunnets plass",
        "end_station_latitude": 59.91546786564256,
        "end_station_longitude": 10.751140873016311
}
```

Her vises diverse informasjon om turen, slik som:
* Nøyaktig start -og sluttidspunkt
* Turens varighet i sekunder
* Nøyaktig start -og sluttposisjon, gitt som geografiske koordinater

Dataene ovenfor er skrevet i formatet *JSON*, og i neste seksjon skal vi lære reglene for å skrive data i dette formatet. Vi kan *lagre* *JSON*-dataene ved å opprette en fil med filendelsen `.json`, og deretter kan vi *sende* filen til andre datamaskiner, eller bruke programmering til å lese filen og *behandle* dataene. Databehandling er  kanskje ikke så interessant når vi bare har én sykkeltur, men hva om vi har flere tusen registrerte turer? 

På *Oslo bysykkel* sine hjemmesider kan vi gå inn på [historiske data](https://oslobysykkel.no/apne-data/historisk) og hente *JSON*-filer for hver måned, det vil si alle registrerte turer! For eksempel starter *JSON*-filen for April 2023 slik:

```json
{
    "started_at": "2023-04-01 03:23:05.537000+00:00",
    "ended_at": "2023-04-01 03:32:55.489000+00:00",
    "duration": 589,
    "start_station_id": "424",
    "start_station_name": "Birkelunden",
    "start_station_description": "langs Seilduksgata",
    "start_station_latitude": 59.9256113,
    "start_station_longitude": 10.760926,
    "end_station_id": "464",
    "end_station_name": "Sukkerbiten",
    "end_station_description": "ved gangbroen",
    "end_station_latitude": 59.905124380703484,
    "end_station_longitude": 10.753763553726515
},
{
    "started_at": "2023-04-01 03:28:06.449000+00:00",
    "ended_at": "2023-04-01 03:34:52.075000+00:00",
    "duration": 405,
    "start_station_id": "592",
    "start_station_name": "Badebakken",
    "start_station_description": "langs Maridalsveien",
    "start_station_latitude": 59.94558091179507,
    "start_station_longitude": 10.760323881579982,
    "end_station_id": "397",
    "end_station_name": "Storo Storsenter",
    "end_station_description": "langs Vitaminveien",
    "end_station_latitude": 59.94671044754387,
    "end_station_longitude": 10.773805285879131
}
```

Her ser vi de to første sykkelturene som ble registrert denne måneden, og hele filen inneholder over 70.000 turer! I Python kan vi gjøre masse interessant med disse dataene, som for eksempel: 

* Finne gjennomsnittlig eller median reisetid mellom to stasjoner, basert på alle turer som har blitt gjort mellom stasjonene. 
    * Deretter kan man for eksempel sammenligne reisetidene med alternative transportmetoder. For eksempel kan forventet reisetid med offentlig transport hentes fra [*Entur*](https://entur.no/), og reisetider med bil kan hentes fra *Google Maps*. Både *Entur* og *Google* tilbyr et grensesnitt som gjør det mulig å hente slik data med programmering!
* Finne ut hvor ofte hver stasjon brukes, enten som start -eller endestasjon. Resultatene kan deretter presenteres på forskjellige måter; for eksempel kan stasjonene markeres som sirkler på et kart, der størrelsen på sirkelen viser hvor populær stasjonen er. 
* Vi lage et 24-timersdiagram for hver stasjon, som forteller hvilke tidspunkter stasjonen brukes mest. 
* Vi kan kombinere de to punktene ovenfor, og lage en kartanimasjon som viser hvordan populæriteten til stasjonene endrer seg gjennom en dag.


Dette er ment som eksempler på veldig interessante (men også utfordrende) måter å behandle data. I senere seksjoner skal vi smått starte på disse eksemplene, og du vil få en kunnskapsbase som gjør at du selv kan bygge videre på det. 

Først må vi lære hvordan data registreres i formatet *JSON*!


## Introduksjon til *JSON*

*JSON* er et tekstformat for å lagre data. Hva betyr egentlig det? Det er mange måter å registrere data som tekst. Dersom vi ønsket å registrere informasjon om oss selv, kunne vi skrevet følgende i en tekstfil:

```
Ola Nordmann
17 år
Oslo
```

Men dersom vi ønsker å registrere dataene i et spesifikt *tekstformat*, må vi følge *reglene* til formate. Dersom vi ønsker å bruke *JSON*, ville teksten ovenfor ikke vært gyldig, fordi vi ikke følger reglene for *JSON*. Her er en måte å gjøre det på som følger *JSON*-reglene:

```json
{
    "fornavn": "Ola",
    "etternavn": "Nordmann", 
    "alder": 17,
    "bosted": "Oslo"
}
```

Det mest grunnleggende elementet i *JSON* er *attributter*. Et eksempel på en attributt er `"fornavn": "Ola"`, og den består av to deler: 

* `"fornavn"` er *nøkkelen* (engelsk *key*)
* `"Ola"` er *verdien* (engelsk *value*)

En nøkkel **må** være en tekststreng, og alle tekststrenger **må** skrives med anførselstegn. Følgende eksempler er *ikke* gyldige attributter: 

* `1: "Ola"` er *ikke* gyldig fordi nøkkelen ikke kan være et tall
* `fornavn: Ola` er *ikke* gyldig fordi alle tekstrenger må ha anførselstegn (både nøkler og verdier)

Attributten `"alder": 17` er gyldig fordi vi har lov til å bruke tall som verdi. Dersom vi skriver desimaltall, må vi huske å bruke punktum som desimalskilletegn, for eksempel `"høyde": 180.5`. 

Hvordan kan vi registrere en fødselsdato, for eksempel 1. januar 2006? Bør vi bruke tall eller tekststreng? Det mest vanlige er å skrive dato på formatet *åååå-mm-dd*, og siden dette **ikke** er et tall, må vi bruke en tekststreng. Attributten kan derfor skrives som `"fødselsdato": "2006-01-01"`. Her er det svært viktig å bruke anførselstegn; selv om tekststrengen nesten bare inneholder tall, er det likevel ikke et tall! 

For å registrere data om oss selv, opprettet vi altså et attributt for hver verdi vi ønsket å registrere; det er lurt å bruke litt tid på å finne et passende nøkkel. Attributtene plasseres deretter i et *objekt*:

```json
{"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo"}
```

Et objekt består av en kommaseparert liste med attributter, og krøllparentesene `{}` viser hvor objektet starter og slutter. Men hva er egentlig et objekt? Det kan være hva som helst, men innholdet i objektet bør være verdier som "hører sammen" på en eller annen måte. Verdiene "Ola", "Nordmann", 17 og "Oslo" hører sammen fordi de handler om en bestemt person. Dersom vi ønsker å registrere en ny person, bør vi opprette et nytt objekt for denne personen: 

```json
[
    {"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo"},
    {"fornavn": "Kari", "etternavn": "Hansen", "alder": 42, "bosted": "Trondheim"}
]
```

Nå har vi en liste av objekter! For å opprette en liste av objekter, må vi bruke de rette parentesene `[]` for å vise hvor listen starter og slutter, og objektene må separeres med komma. 

Vi har lov til å plassere hva som helst i en liste, men en uskreven regel er at objektene i listen bør være av samme type. Derfor bør vi kun legge til nye personer i listen ovenfor, og ikke andre objekter. Det er også viktig at nye personer registreres på samme måte; for eksempel ville det vært dumt å legge til en ny person på følgende måte:

```json
[
    {"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo"},
    {"fornavn": "Kari", "etternavn": "Hansen", "alder": 42, "bosted": "Trondheim"},
    {"navn": "Per Hansen", "hjemsted": "Tromsø"}
]
```

Her er det to problemer:

- Vi har skrevet hele navnet i én attributt, i stedet for å ha attributter for fornavn og etternavn.  
- Vi har brukt nøkkelen `"hjemsted"` i stedet for `"bosted"`. 

Vi bør bruke de **samme nøklene** for å registrere samme type informasjon:

```json
[
    {"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo"},
    {"fornavn": "Kari", "etternavn": "Hansen", "alder": 42, "bosted": "Trondheim"},
    {"fornavn": "Per", "etternavn": "Hansen", "alder": null, "bosted": "Tromsø"}
]
```

Her har vi også brukt den spesielle verdien `null`, som forteller at alderen til den nye personen er ukjent. 

En *JSON*-fil består gjerne av en liste med objekter, som i eksempelet over. Men det er også lov å definere en liste av *verdier*:  

```json
["fotball", "musikk", "bøker"]
```

En liste kan plasseres i et attributt: 

```json
{
    "fornavn": "Ola", 
    "etternavn": "Nordmann", 
    "alder": 17, 
    "bosted": "Oslo", 
    "interesser": ["fotball", "musikk", "bøker"]
}
```

I neste seksjon skal vi se at vi har full valgfrihet til å plassere lister og objekter inni hverandre!

## Struktur av *JSON*-filer

Generelt kan vi si at en *JSON*-fil er bygd opp av objekter og lister. Forskjellen mellom dem kan oppsummeres slik:

* En liste er omsluttet av de rette parentesene `[]`, mens et objekt er omsluttet av krøllparentesene `{}`.
* En liste inneholder en sekvens av verdier, mens et objekt inneholder en sekvens av attributter.

Tenk deg et vi skal registrere størrelsen til en eske; dette kan være viktig i et system som håndterer pakkepost. Avhengig av hvor mye informasjon vi ønsker å registrere, kan vi enten bruke enten en liste eller et objekt: 

```json
[50, 40, 30]
{"lengde": 50, "bredde": 40, "høyde": 30}
```

Både listen og objektet inneholder verdier, men i et objekt må hver verdi tilknyttes et nøkkel.

I dette eksempelet brukte vi bare tallverdier, men vi har lov til å bruke følgende typer verdier: 

* Tekststreng
* Tall
* Liste
* Objekt
* `null` (indikerer at verdien mangler)
* Boolsk verdi (enten `true` eller `false`)

Her er et objekt som inneholder alle typer verdier: 

```json
{
    "fornavn": "Kari",
    "etternavn": null,
    "alder": 42, 
    "interesser": ["sjakk", "fotografering"],
    "bolig": {
        "type": "leilighet", 
        "størrelse": 100, 
        "sted": "Trondheim"}, 
    "harHusdyr": true
}
```

Å bruke ulike typer verdier er altså vanlig i objekter, mens i en liste bør verdiene være av samme type. Vi kan for eksempel ha en liste av tall, en liste av tekststrenger, en liste av objekter, eller en liste av lister! 

Følgende eksempel viser hvordan lister og objekter kan settes inni hverandre:

```json
{
    "personer": [
        {
            "fornavn": "Ola", 
            "etternavn": "Nordmann", 
            "alder": 17, 
            "bosted": "Oslo",
            "interesser": ["fotball", "musikk", "bøker"]
        },
        {
            "fornavn": "Kari", 
            "etternavn": "Hansen", 
            "alder": 42, 
            "bosted": "Trondheim",
            "interesser": ["sjakk", "fotografering"]
        },
        {
            "fornavn": "Per", 
            "etternavn": "Hansen", 
            "alder": null, 
            "bosted": "Tromsø",
            "interesser": ["matlaging", "skiturer"]
        }
    ]
}
```

I dette eksempelet har vi et objekt som omslutter hele teksten, og i dette objektet finner vi ett attributt med nøkkelen `"personer"`. I dette attributtet finner vi en liste med *personobjekter*, det vil si at hvert objekt inneholder informasjon om en person. 

I *JSON* spiller mellomrom og linjeskift ingen rolle, så vi kunne skrevet all teksten på én linje! Men ved å bruke innrykk og linjeskift gjør vi det lettere å se strukturen av lister og objekter. Det kan være lurt å bruke en teksteditor som hjelper deg å formatere *JSON*-teksten på en ryddig måte. Du kan også åpne *JSON*-filer i nettleseren din: 

* Med en nyere versjon av Firefox vil *JSON*-filer automatisk åpnes i en ryddig og interaktiv framviser.
* Med Google Chrome kan du bruke utvidelsen *JSON Viewer*.
* [JSON Hero](https://jsonhero.io/) er et nettbasert alternativ som kan brukes fra hvilken som helst nettleser. 

**Aktivitetsforslag.**

1. Lag en *JSON*-fil hvor du registrerer data fra ditt eget liv. For eksempel kan filen begynne med grunnleggende informasjon, videre kan du registrere eiendeler; hvis du for eksempel har mange bøker, kan hver bok ha informasjon som tittel, forfatter, sideantall, og så videre.  Du kan også registrere hvilke filmer, serier eller annet du har sett nylig, eller ting du har gjort. Forsøk å organisere *JSON*-filen på en oversiktlig måte ved å bruke lister og objekter. 

2. [Her](https://github.com/jdorfman/awesome-json-datasets/blob/master/README.md) finner du mange eksempler på *JSON*-filer med ekte data. Last ned ett eller flere filer som du synes virker interessante, og studér strukturen til *JSON*-teksten. 

## *JSON* eller *CSV*? 

*JSON*-formatet er veldig fleksibelt og kan brukes til å lagre alle typer data. I senere seksjoner vil du for eksempel se hvordan statistisk data elegant kan lagres i *JSON*.

I enkelte tilfeller kan dataene våre skrives som rader i en tabell, og da kan det være aktuelt å bruke det enklere formatet *CSV*. 

Tenk deg at du har følgende *JSON*-fil:

```json
[
    {
        "fornavn": "Ola", 
        "etternavn": "Nordmann", 
        "alder": 17, 
        "bosted": "Oslo"
    },
    {
        "fornavn": "Kari", 
        "etternavn": "Hansen", 
        "alder": 42, 
        "bosted": "Trondheim"
    },
    {
        "fornavn": "Per", 
        "etternavn": "Hansen", 
        "alder": 64, 
        "bosted": "Tromsø"
    }
]

```
Denne *JSON*-filen har følgende egenskaper: 
* Filen består av én liste av objekter, og ikke noe annet.
* Hvert objekt har nøyaktig de samme datafeltene. 
* I datafeltene finner vi kun strenger og tall, ikke lister eller objekter.

Når en *JSON*-fil er av denne typen, kan vi enkelt registrere dataene på tabellform: 

```csv
"fornavn","etternavn","alder","bosted"
"Ola","Nordmann",17,"Oslo"
"Kari","Hansen",42,"Trondheim"
"Per","Hansen",64,"Tromsø"
```
Dette formatet kalles *CSV* (*Comma-Separated Values*), og har kun noen få enkle regler:
* I den første linjen skriver vi navnet på datafeltene, separert av komma
* Deretter skriver vi hvert objekt på én linje
* Hvert objekt skrives som en liste av verdier, separert av komma
* Rekkefølgen av verdier svarer til rekkefølgen av datafelter

Hvordan kan man vise *CSV*-filer? Siden en *CSV*-fil er en tabell, kan vi bruke et vanlig program for regneark, for eksempel *Microsoft Excel* på Windows, *Numbers* på Mac, eller [*Google Sheets*](https://docs.google.com/spreadsheets/u/0/) i nettleseren. 

Som oppsummering kan vi si at dersom dataene våre har egenskapene listet ovenfor, så er *CSV* en enkel og plassbesparende løsning. Men i alle andre tilfeller er *JSON* å foretrekke, siden det gir fleksibilitet til å strukturere dataene slik vi selv ønsker. 

## Dictionary i Python

Du er antagelig vant til å bruke lister i Python:


```python
my_list = ["Oslo", "Tønsberg", "Mandal", "Hammerfest"]
```

Hvert element i lista har en unik *indeks*: 

```
0: "Oslo"
1: "Tønsberg"
2: "Mandal"
3: "Hammerfest"
```

Disse indeksene gjør at vi kan finne igjen spesifikke elementer i lista: 


```python
a = my_list[0]
b = my_list[2]

print(a)
print(b)
```

    Oslo
    Mandal


Vi kan si at 0 er *nøkkelen* som gir oss det første elementet i lista, altså "Oslo". I en liste må vi bruke heltallene $0, 1, 2, 3, ...$ som nøkler. Men hva om vi ønsker å bruke andre nøkler, som for eksempel:

```
"hovedstad": "Oslo"
"eldst": "Tønsberg"
"sørligst": "Mandal"
"nordligst": "Hammerfest"
```

Vi kan gjøre dette ved å bruke en *dictionary*. For å opprette en dictionary bruker vi krøllparentesene `{}`, og hver verdi må tilknyttes en nøkkel:


```python
my_dict = {"hovedstad": "Oslo", "eldst": "Tønsberg", "sørligst": "Mandal", "nordligst": "Hammerfest"}
```

Nå kan vi hente verdier ved å bruke våre egendefinerte nøkler: 


```python
a = my_dict["hovedstad"]
b = my_dict["sørligst"]

print(a)
print(b)
```

    Oslo
    Mandal


La oss se på et annet eksempel. I Python kan elementene i en liste være hva som helst, også nye lister:


```python
person = ["Kari", None, 42, ["sjakk", "fotografering"], ["leilighet", 100, "Trondheim"], True]
```

Denne listen er ment å gi informasjon om en person, men det er uklart hva de ulike verdiene betyr. I tillegg må vi bruke tallindekser for å hente ut spesifikke verdier:


```python
bosted = person[4][2]
print(bosted)
```

    Trondheim


Her er det mye mer hensiktsmessig å bruke en dictionary, fordi vi kan legge inn verdiene med nøkler: 


```python
person = {"fornavn": "Kari", "alder": 42}
```

Igjen kan vi tenke på nøklene "fornavn" og "alder" som egendefinerte indekser. I en liste ville indeksene vært 0 og 1, mens i en dictionary kan vi bruke valgfrie tekststrenger. Deretter kan vi "slå opp" på disse strengene for å hente verdiene vi ønsker. En dictionary er altså et slags oppslagsverk, akkurat som navnet antyder.

For å legge inn flere verdier i en dictionary trenger vi bare å opprette nye nøkler: 


```python
person["interesser"] = ["sjakk", "fotografering"]
person["harHusdyr"] = True
print(person)
```

    {'fornavn': 'Kari', 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'harHusdyr': True}


Vi kan legge inn hva som helst, til og med en ny dictionary:


```python
person["bolig"] = {"type": "leilighet", "størrelse": 100, "sted": "Trondheim"}
print(person)
```

    {'fornavn': 'Kari', 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'harHusdyr': True, 'bolig': {'type': 'leilighet', 'størrelse': 100, 'sted': 'Trondheim'}}


For å hente verdien "Trondheim", må vi først gå inn på nøkkelen "bolig", og deretter på nøkkelen "sted":


```python
print(person["bolig"]["sted"])
```

    Trondheim


Det er ikke noe i veien for å opprette en liste der hvert element er en dictionary:


```python
person1 = {"navn": "Ola Nordmann", "alder": 17}
person2 = {"navn": "Kari Hansen", "alder": 42}
person3 = {"navn": "Per Hansen", "alder": 64}

people = [person1, person2, person3]
```

For å hente spesifikke verdier kan vi bruke en blanding av tallindekser og nøkler: 


```python
name = people[2]["navn"]
print(name)
```

    Per Hansen


Vi kan også gå gjennom lista med en løkke:


```python
for person in people:
    print(person["navn"])
```

    Ola Nordmann
    Kari Hansen
    Per Hansen


Hva hadde skjedd hvis en dictionary manglet nøkkelen "navn"? Da ville vi fått en feilmelding! Derfor må vi være sikre på at de samme nøklene finnes i hver dictionary. Sagt på en annen måte bør lista inneholde objekter av samme type. I vårt eksempel har vi en liste av personobjekter. 

For å oppsummere kan vi si at data bør legges i en dictionary når vi ønsker å slå opp spesifikke verdier. En liste er kun egnet dersom hvert element er av samme type og vi skal gjøre den samme operasjonen på hvert element (ved å bruke en løkke). 

Vi har også sett at en liste kan inneholde dictionary-elementer, og en dictionary kan inneholde lister!

**Aktivitetsforslag.** Ta utgangspunkt i *Aktivitetsforslag 1* eller *2* fra seksjonen *Struktur av JSON-filer*. Legg alle eller deler av dataene i en dictionary (eventuelt en liste der hvert element er en dictionary). Sørg for at dataene er strukturert på samme måte, med de samme nøklene. Forsøk deretter å hente noen spesifikke verdier, og eksperimenter også med løkker dersom du har lister. 

## Innlasting av *JSON*-filer i Python

Tenk deg at du har *JSON*-filen `person.json` med følgende innhold: 

```json
{
    "fornavn": "Kari",
    "etternavn": null,
    "alder": 42, 
    "interesser": ["sjakk", "fotografering"],
    "bolig": {
        "type": "leilighet", 
        "størrelse": 100, 
        "sted": "Trondheim"}, 
    "harHusdyr": true
}
```

Hvordan kan vi legge disse verdiene i en variabel i Python? Dersom du har lest forrige seksjon, ser du kanskje at et *JSON*-objekt i praksis er det samme som en *dictionary* i Python? Vi ønsker altså at dataene ovenfor skal legges i en dictionary, og at vi deretter kan bruke nøklene til å hente spesifikke verdier.

For å importere en *JSON*-fil kan vi bruke følgende kode:


```python
import json
my_file = open("person.json")
my_string = my_file.read()
my_dict = json.loads(my_string)

print(my_dict)
```

    {'fornavn': 'Kari', 'etternavn': None, 'alder': 42, 'interesser': ['sjakk', 'fotografering'], 'bolig': {'type': 'leilighet', 'størrelse': 100, 'sted': 'Trondheim'}, 'harHusdyr': True}


*Funksjonen `json.loads` tar en tekststreng som parameter og forsøker å tolke denne som en dictionary.*

Nå har vi lagt dataene i en dictionary som har akkurat samme struktur som *JSON*-objektet. Vi kan nå gjøre endre noen spesifikke verdier: 


```python
old_age = my_dict["alder"] 
new_age = old_age + 10
my_dict["alder"] = new_age
my_dict["interesser"].append("fuglekikking")

print(my_dict)
```

    {'fornavn': 'Kari', 'etternavn': None, 'alder': 52, 'interesser': ['sjakk', 'fotografering', 'fuglekikking'], 'bolig': {'type': 'leilighet', 'størrelse': 100, 'sted': 'Trondheim'}, 'harHusdyr': True}


Husk at disse endringene kun finnes i variabelen `my_dict`, som er midlertidig lagret i datamaskinens minne når vi kjører programmet. For å lagre dataene permanent, kan vi legge dem i en *JSON*-fil. I starten av seksjonen importerte vi fra *JSON* til dictionary, og nå skal vi gå den andre veien. Vi begynner med å konvertere fra dictionary til en tekststreng:


```python
my_new_string = json.dumps(my_dict, indent=4)
print(my_new_string)
```

    {
        "fornavn": "Kari",
        "etternavn": null,
        "alder": 52,
        "interesser": [
            "sjakk",
            "fotografering",
            "fuglekikking"
        ],
        "bolig": {
            "type": "leilighet",
            "st\u00f8rrelse": 100,
            "sted": "Trondheim"
        },
        "harHusdyr": true
    }


*Merk hvordan funksjonen `json.dumps` sørger for pen formatering når vi bruker tilleggsparameteren `indent=4`. Dette er også nyttig dersom vi jobber med en stor dictionary og ønsker å få en bedre oversikt over strukturen.*

Nå kan vi legge tekststrengen i en *JSON*-fil:


```python
new_file = open('person_new.json', 'w+')
new_file.write(my_new_string)
new_file.close()
```

For å oppsummere, så har vi importert filen `person.json`, gjort noen endringer, og lagret de nye dataene under filnavnet `person_new.json`. Vi kunne også ha overskrevet den gamle filen med de nye dataene. 

**Aktivitetsforslag.** Ta utgangspunkt i *JSON*-filen du opprettet i *Aktivitetsforslag 1* eller *2* fra seksjonen *Struktur av JSON-filer*. Last inn filene i Python, og forsøk deretter å gjøre noen endringer på dataene. Lagre til slutt de oppdaterte datene i en ny *JSON*-fil (eller overskriv den gamle filen). 
