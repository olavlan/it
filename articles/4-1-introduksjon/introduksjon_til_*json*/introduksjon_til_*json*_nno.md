---
title: "Introduksjon til *JSON*"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

*JSON* er eit tekstformat for å lagra data. Kva betyr eigentleg det? Det er mange måtar å registrera data som tekst. Dersom me ønskte å registrera informasjon om oss sjølv, kunne me skrive følgjande i ei tekstfil:

```
Ola Nordmann
17 år
Oslo
```

Men dersom me ønskjer å registrera dataa i eit spesifikt *tekstformat*, må me følgja *reglane* til formate. Dersom me ønskjer å bruka *JSON*, ville teksten ovanfor ikkje vore gyldig, fordi me ikkje følgjer reglane for *JSON*. Her er ein måte å gjera det på som følgjer *JSON*-reglane:

```json
{
    "fornavn": "Ola",
    "etternavn": "Nordmann", 
    "alder": 17,
    "bosted": "Oslo"
}
```

Det mest grunnleggjande elementet i *JSON* er *attributt*. Eit døme på eit attributt er `"fornavn": "Ola"`, og han består av to delar:

* `"fornavn"` er *nøkkelen* (engelsk *key*)
* `"Ola"` er *verdien* (engelsk *value*)

Ein nøkkel **må** vera ein tekststreng, og alle tekststrenger **må** skrivast med hermeteikn. Følgjande døme er *ikkje* gyldige attributt:

* `1: "Ola"` er *ikkje* gyldig fordi nøkkelen ikkje kan vera eit tal
* `fornavn: Ola` er *ikkje* gyldig fordi alle tekstrenger må ha hermeteikn (både nøklar og verdiar)

Attributten `"alder": 17` er gyldig fordi me har lov til å bruka tal som verdi. Dersom me skriv desimaltal, må me hugsa å bruka punktum som desimalskiljeteikn, til dømes `"høyde": 180.5`.

Korleis kan me registrera ein fødselsdato, til dømes 1. januar 2006? Bør me bruka tal eller tekststreng? Det mest vanlege er å skriva dato på formatet *åååå-mm-dd*, og sidan dette **ikkje** er eit tal, må me bruka ein tekststreng. Attributten kan derfor skrivast som `"fødselsdato": "2006-01-01"`. Her er det svært viktig å bruka hermeteikn; sjølv om tekststrengen nesten berre inneheld tal, er det likevel ikkje eit tal!

For å registrera data om oss sjølv, oppretta me altså eit attributt for kvar verdi me ønskte å registrera; det er lurt å bruka litt tid på å finna eit passande nøkkel. Attributta blir deretter plasserte i eit *objekt*:

```json
{"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo"}
```

Eit objekt består av ei kommaseparert liste med attributt, og krøllparentesane `{}` viser kvar objektet startar og sluttar. Men kva er eigentleg eit objekt? Det kan vera kva som helst, men innhaldet i objektet bør vera verdiar som "høyrer saman" på ein eller annan måte. Verdiene "Ola", "Nordmann", 17 og "Oslo" høyrer saman fordi dei handlar om ein bestemd person. Dersom me ønskjer å registrera ein ny person, bør me oppretta eit nytt objekt for denne personen:

```json
[
    {"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo"},
    {"fornavn": "Kari", "etternavn": "Hansen", "alder": 42, "bosted": "Trondheim"}
]
```

No har me ei liste av objekt! For å oppretta ei liste av objekt, må me bruka dei rette parentesane `[]` for å visa kvar lista startar og sluttar, og objekta må separerast med komma.

Me har lov til å plassera kva som helst i ei liste, men ein uskriven regel er at objekta i lista bør vera av same type. Derfor bør me berre leggja til nye personar i lista ovanfor, og ikkje andre objekt. Det er også viktig at nye personar blir registrerte på same måte; til dømes ville det vore dumt å leggja til ein ny person på følgjande måte:

```json
[
    {"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo"},
    {"fornavn": "Kari", "etternavn": "Hansen", "alder": 42, "bosted": "Trondheim"},
    {"navn": "Per Hansen", "hjemsted": "Tromsø"}
]
```

Her er det to problem:

- Me har skrive heile namnet i eitt attributt, i staden for å ha attributt for førenamn og etternamn.
- Me har brukt nøkkelen `"hjemsted"` i staden for `"bosted"`.

Me bør bruka dei **same nøklane** for å registrera same type informasjon:

```json
[
    {"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo"},
    {"fornavn": "Kari", "etternavn": "Hansen", "alder": 42, "bosted": "Trondheim"},
    {"fornavn": "Per", "etternavn": "Hansen", "alder": null, "bosted": "Tromsø"}
]
```

Her har me også brukt den spesielle verdien `null`, som fortel at alderen til den nye personen er ukjend.

Ein *JSON*-fil består gjerne av ei liste med objekt, som i dømet over. Men det er også lov å definera ei liste av *verdiar*:

```json
["fotball", "musikk", "bøker"]
```

Ei liste kan plasserast i eit attributt:

```json
{
    "fornavn": "Ola", 
    "etternavn": "Nordmann", 
    "alder": 17, 
    "bosted": "Oslo", 
    "interesser": ["fotball", "musikk", "bøker"]
}
```

I neste seksjon skal me sjå at me har full valfridom til å plassera lister og objekt inni kvarandre!

