---
title: "Sette inn flere konstruktører"
belongs_to_chain: "Klasser og objekter i Python"
figures_to_include:
	- "python_class_book_two_constructors.svg"
---

Vi skal nå vise hvordan vi kan legge til en ekstra konstruktør. Eksempelet vårt er en konstruktør som bare trenger bokas ISBN:

<img src="/media/markdowncontent/assosiated_files/python_class_book_two_constructors.svg" width="25%">

Tenk deg at du har boka *Sofies verden*, og på baksiden ser du at bokas ISBN er *9788203245114*. Det hadde vært veldig nyttig å kunne registrere boka med kommandoen `Book("9788203245114")`. Problemet er at vi allerede har en konstruktør for klassen `Book`, og Python lar oss ikke definere to konstruktører! Løsningen er å sørge for at den ene konstruktøren kan brukes på flere måter, ved å bruke *navngitte parametre* (*keyword arguments* på engelsk). For å forstå hva dette er kan vi sammenligne følgende kodelinjer:


```python
b1 = Book("Sofies verden", "Jostein Gaarder", 512)
b2 = Book(author="Jostein Gaarder", number_of_pages=512, title="Sofies verden")
```

I den første linjen oppretter vi et bokobjekt på den vanlige måten. I den andre linjen oppretter vi et objekt med akkurat de samme verdiene, men her spesifiserer vi navnet til parameteren før vi skriver verdien. En fordel med dette er at vi ikke trenger å huske rekkefølgen til parametrene (men vi må huske navnene). En annen fordel er at vi har mulighet til å droppe noen parametre. Da må vi først sørge for at parametrene har *standardverdier*:


```python
class Book:
    def __init__(self, title="", author="", number_of_pages=0):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
```

Nå kan vi si at metoden har *valgfrie parametre*, siden vi kan la være å fylle ut noen parametre. For eksempel kan vi opprette et objekt med kommandoen `Book("Sofies verden", number_of_pages=512)`. Her skriver vi den første parameteren på vanlig måte, men i stedet for å skrive den andre parameteren, så navngir vi den tredje parameteren. Altså har vi hoppet over den andre parameteren (`author`), og denne får derfor standardverdien, som i dette tilfellet er den tomme tekststrengen `""`.

Hvorfor er valgfrie parametre nyttige for oss? Fordi vi nå kan vi legge til de valgfrie parameteren `isbn`!


```python
class Book:
    def __init__(self, title="", author="", number_of_pages=0, isbn = ""):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
```

Siden alle parametrene er valgfrie, kan vi hoppe over de tre første parametrene, slik at vi kun skriver ISBN! Med andre ord kan vi opprette et bokobjekt med kommandoen `Book(isbn="9788203245114")`. 

Men for at metoden faktisk skal fungere slik vi ønsker, må den sjekke hvilke parametre som har blitt fylt ut. Mer spesifikt må vi stille følgende spørsmål:

- Har parameteren `isbn` blitt fylt ut? 
    * Hvis ja, så bruker vi `isbn` til å finne boka i en database, og henter de ønskede verdiene fra databasen.
    + Hvis nei, så bruker vi de tre første parametrene i stedet.

Når vi skal "stille et spørsmål" for å avgjøre hvilken kode som skal avgjøres, bruker vi en `if`-`else`-blokk:


```python
class Book:
    def __init__(self, title="", author="", number_of_pages=0, isbn = ""):
        if len(isbn)>0: 
            self.title, self.author, self.number_of_pages = self.get_information_from_database(isbn)
        else:
            self.title = title
            self.author = author
            self.number_of_pages = number_of_pages
            
    def get_information_from_database(self, isbn):
        return "", "", 0
```

Prøv gjerne å forstå hvordan spørsmålet vi stilte ovenfor har blitt til en `if`-`else`-blokk i koden. Her følger en forklaring: 

1. Kodelinjen `if len(isbn) > 0` tester om `isbn`-parameteren har blitt fylt ut. Hvis testen gir svaret "ja", så utføres denne kodeblokken. 
2. Hvis testen gir svaret "nei", så utføres `else`-blokken i stedet. 
3. Siden konstruktøren bare skal ha ansvar for å opprette datafeltene, har vi  laget en delmetode som har ansvar for å hente informasjon fra en bokdatabase. 

*Merk at vi ikke har skrevet funksjonell kode i delmetoden `get_information_from_database`. Dette kan vi gjerne vente med til den grunnleggende strukturen med alle klasser og metoder er på plass. Foreløpig kan vi la delmetoden returnere noen standardverdier.*

*Det er også viktig å forstå hvordan vi kaller på delmetoden. Vi kan ikke skrive `get_information_from_database(isbn)`, for da vil Python klage på at vi bare har gitt én parameter! I stedet må vi skrive `self.get_information_from_database(isbn)`, slik at objektet selv gis som den første parameteren, og `isbn` som den andre parameteren!*

Vi har nå én konstruktør som kan brukes på to forskjellige måter:


```python
b1 = Book("Sofies verden", "Jostein Gaarder", 512)
b2 = Book(isbn="9788203245114")
```

