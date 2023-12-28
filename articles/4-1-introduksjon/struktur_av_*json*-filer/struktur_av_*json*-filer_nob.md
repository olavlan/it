---
title: "Struktur av *JSON*-filer"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

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

