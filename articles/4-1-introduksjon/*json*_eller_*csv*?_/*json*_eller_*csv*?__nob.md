---
title: "*JSON* eller *CSV*? "
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

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

