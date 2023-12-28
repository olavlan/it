---
title: "Struktur av *JSON*-filer"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

Generelt kan me seia at ein *JSON*-fil er bygd opp av objekt og lister. Forskjellen mellom dei kan samanfattast slik:

* Ei liste er omgitt av dei rette parentesane `[]`, medan eit objekt er omgitt av krøllparentesane `{}`.
* Ei liste inneheld ein sekvens av verdiar, medan eit objekt inneheld ein sekvens av attributt.

Tenk deg eit me skal registrera storleiken til ei eske; dette kan vera viktig i eit system som handterer pakkepost. Avhengig av kor mykje informasjon me ønskjer å registrera, kan me anten bruka anten ei liste eller eit objekt:

```json
[50, 40, 30]
{"lengde": 50, "bredde": 40, "høyde": 30}
```

Både lista og objektet inneheld verdiar, men i eit objekt må kvar verdi knytast til eit nøkkel.

I dette dømet brukte me berre talverdiar, men me har lov til å bruka følgjande typar verdiar:

* Tekststreng
* Tal
* Liste
* Objekt
* `null` (indikerer at verdien manglar)
* Boolsk verdi (anten-eller `true`  `false`)

Her er eit objekt som inneheld alle typar verdiar:

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

Å bruka ulike typar verdiar er altså vanleg i objekt, medan i ei liste bør verdiane vera av same type. Me kan til dømes ha ei liste av tal, ei liste av tekststrenger, ei liste av objekt, eller ei liste av lister!

Følgjande døme viser korleis lister og objekt kan setjast inni kvarandre:

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

I dette dømet har me eit objekt som omgir heile teksten, og i dette objektet finn me eitt attributt med nøkkelen `"personer"`. I dette attributtet finn me ei liste med *personobjekt*, det vil seia at kvart objekt inneheld informasjon om ein person.

I *JSON* speler mellomrom og linjeskift inga rolle, så me kunne skrive all teksten på éi linje! Men ved å bruka innrykk og linjeskift gjer me det lettare å sjå strukturen av lister og objekt. Det kan vera lurt å bruka ein teksteditor som hjelper deg å formatera *JSON*-teksten på ein ryddig måte. Du kan også opna *JSON*-filer i nettlesaren din:

* Med ein nyare versjon av Firefox vil *JSON*-filer automatisk blir opna i ein ryddig og interaktiv framvisar.
* Med Google Chrome kan du bruka utvidinga *JSON Viewer*.
* [JSON Hero](https://jsonhero.io/) er eit nettbasert alternativ som kan brukast frå kva som helst nettlesar.

**Aktivitetsforslag.**

1. Lag ein *JSON*-fil der du registrerer data frå ditt eige liv. Til dømes kan fila byrja med grunnleggjande informasjon, vidare kan du registrera eigedelar; viss du til dømes har mange bøker, kan kvar bok ha informasjon som tittel, forfattar, sidetal, og så vidare.  Du kan også registrera kva filmar, seriar eller anna du har sett nyleg, eller ting du har gjort. Forsøk å organisera *JSON*-fila på ein oversiktleg måte ved å bruka lister og objekt.

2. [Her](https://github.com/jdorfman/awesome-json-datasets/blob/master/readme.md) finn du mange døme på *JSON*-filer med ekte data. Last ned eitt eller fleire filer som du synest verkar interessante, og studér strukturen til *JSON*-teksten.

