---
title: "Introduksjon til *JSON*"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

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

