---
title: "*JSON* eller *CSV*?"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

*JSON*-formatet er veldig fleksibelt og kan brukast til å lagra alle typar data. I seinare seksjonar vil du til dømes sjå korleis statistisk data elegant kan lagrast i *JSON*.

I enkelte tilfelle kan dataa våre skrivast som radar i ein tabell, og då kan det vera aktuelt å bruka det enklare formatet *CSV*.

Tenk deg at du har følgjande *JSON*-fil:

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
Denne *JSON*-fila har følgjande eigenskapar:
* Fila består av éi liste av objekt, og ikkje noko anna.
* Kvart objekt har nøyaktig dei same datafelta.
* I datafelta finn me berre strenger og tal, ikkje lister eller objekt.

Når ein *JSON*-fil er av denne typen, kan me enkelt registrera dataa på tabellform:

```csv
"fornavn","etternavn","alder","bosted"
"Ola","Nordmann",17,"Oslo"
"Kari","Hansen",42,"Trondheim"
"Per","Hansen",64,"Tromsø"
```
Dette formatet blir kalla *CSV* (*Comma-Separated Values*), og har berre nokre få enkle reglar:
* I den første linja skriv me namnet på datafelta, separert av komma
* Deretter skriv me kvart objekt på éi linje
* Kvart objekt blir skrive som ei liste av verdiar, separert av komma
* Rekkjefølgja av verdiar svarer til rekkjefølgja av datafelt

Korleis kan ein visa *CSV*-filer? Sidan ein *CSV*-fil er ein tabell, kan me bruka eit vanleg program for rekneark, til dømes *Microsoft Excel* på Windows, *Numbers* på Mac, eller [*Google Sheets*](https://docs.google.com/spreadsheets/u/0/) i nettlesaren.

Som oppsummering kan me seia at dersom dataa våre har eigenskapane lista ovanfor, så er *CSV* ei enkel og plassbesparande løysing. Men i alle andre tilfelle er *JSON* å føretrekkja, sidan det gir fleksibilitet til å strukturera dataa slik me sjølv ønskjer.

