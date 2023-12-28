---
title: "Setja inn fleire konstruktørar"
belongs_to_chain: "Klasser og objekter i Python"
figures_to_include:
	- "python_class_book_two_constructors.svg"
---

Me skal no visa korleis me kan leggja til ein ekstra konstruktør. Dømet vårt er ein konstruktør som berre treng bokas ISBN:

<img src="/media/markdowncontent/assosiated_files/python_class_book_two_constructors.svg" width="25%">

Tenk deg at du har boka *Sofies verd*, og på baksida ser du at bokas ISBN er *9788203245114*. Det hadde vore veldig nyttig å kunna registrera boka med kommandoen `Book("9788203245114")`. Problemet er at me allereie har ein konstruktør for klassen `Book`, og Python lèt oss ikkje definera to konstruktørar! Løysinga er å sørgja for at den eine konstruktøren kan brukast på fleire måtar, ved å bruka *namngitte parametrar* (*keyword arguments* på engelsk). For å forstå kva dette er kan me samanlikna følgjande kodelinjer:


```python
b1 = Book("Sofies verden", "Jostein Gaarder", 512)
b2 = Book(author="Jostein Gaarder", number_of_pages=512, title="Sofies verden")
```

I den første linja opprettar me eit bokobjekt på den vanlege måten. I den andre linja opprettar me eit objekt med akkurat dei same verdiane, men her spesifiserer me namnet til parameteren før me skriv verdien. Ein fordel med dette er at me ikkje treng å hugsa rekkjefølgja til parametrane (men me må hugsa namna). Ein annan fordel er at me har høve til å droppa nokre parametrar. Då må me først sørgja for at parametrane har *standardverdiar*:


```python
class Book:
    def __init__(self, title="", author="", number_of_pages=0):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
```

No kan me seia at metoden har *valfrie parametrar*, sidan me kan la vera å fylla ut nokre parametrar. Til dømes kan me oppretta eit objekt med kommandoen `Book("Sofies verden", number_of_pages=512)`. Her skriv me den første parameteren på vanleg måte, men i staden for å skriva den andre parameteren, så namngir me den tredje parameteren. Altså har me hoppa over den andre parameteren (`author`), og denne får derfor standardverdien, som i dette tilfellet er den tomme tekststrengen `""`.

Kvifor er valfrie parametrar nyttige for oss? Fordi me no kan me leggja til dei valfrie parameteren `isbn`!


```python
class Book:
    def __init__(self, title="", author="", number_of_pages=0, isbn = ""):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
```

Sidan alle parametrane er valfrie, kan me hoppa over dei tre første parametrane, slik at me berre skriv ISBN! Med andre ord kan me oppretta eit bokobjekt med kommandoen `Book(isbn="9788203245114")`.

Men for at metoden faktisk skal fungera slik me ønskjer, må han sjekka kva parametrar som har vorte fylt ut. Meir spesifikt må me stilla følgjande spørsmål:

- Har parameteren `isbn` vorte fylt ut?
* Viss ja, så bruker me `isbn` til å finna boka i ein database, og hentar dei ønskte verdiane frå databasen.
+ Viss nei, så bruker me dei tre første parametrane i staden.

Når me skal "stilla eit spørsmål" for å avgjera kva kode som skal avgjerast, bruker me ein `if`-`else`-blokk:


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

Prøv gjerne å forstå korleis spørsmålet me stilte ovanfor har vorte til ein `if`-`else`-blokk i koden. Her følgjer ei forklaring:

1. Kodelinja `if len(isbn) > 0` testar om `isbn`-parameteren har vorte fylt ut. Viss testen gir svaret "ja", så blir denne kodeblokka utført.
2. Viss testen gir svaret "nei", så utførast `else`-blokka i staden.
3. Sidan konstruktøren berre skal ha ansvar for å oppretta datafelta, har me  laga ein delmetode som har ansvar for å henta informasjon frå ein bokdatabase.

*Merk at me ikkje har skrive funksjonell kode i delmetoden `get_information_from_database`. Dette kan me gjerne venta med til den grunnleggjande strukturen med alle klassar og metodar er på plass. Førebels kan me la delmetoden returnera nokre standardverdiar.*

*Det er også viktig å forstå korleis me kallar på delmetoden. Me kan ikkje skriva `get_information_from_database(isbn)`, for då vil Python klaga på at me berre har gitt éin parameter! I staden må me skriva `self.get_information_from_database(isbn)`, slik at objektet sjølv blir gitt som den første parameteren, og `isbn` som den andre parameteren!*

Me har no éin konstruktør som kan brukast på to ulike måtar:


```python
b1 = Book("Sofies verden", "Jostein Gaarder", 512)
b2 = Book(isbn="9788203245114")
```

