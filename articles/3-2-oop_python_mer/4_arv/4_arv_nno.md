---
title: "Arv"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
	- "inheritance.svg"
---

Frå seksjonane om arv frå kapittelet *Konsepter i objektorientert programmering* kom me fram til følgjande klassediagram:

<img src="/media/markdowncontent/assosiated_files/inheritance.svg" width="400">

*Dette klassediagrammet er omsett til engelsk og litt modifisert. Me hadde klassen `Utlånsobjekt`, som me har omsett til `Loanable`. Me kan tenkja på dette som ein kortversjon av *"Loanable object"*. I slike namn er det vanleg å utelata ordet *object* i klassenamnet.*

Klassane `Book` og `Movie` skal arva datafelta og metodane til klassen `Loanable`. Korleis får me til dette i Python?

Superklassen `Loanable` arvar ikkje frå nokon klassar, så denne kan programmerast på vanleg måte:


```python
class Loanable:
    def register_loan(self, person):
        print("Loan registered: ", title, " -> ", person)

    def register_delivery(self):
        print("Delivery registered: ", title)
```

*På dette stadiet er det ikkje viktig at me har fungerande kode, så me kan byrja med å skriva ut nokre enkle meldingar.*

Korleis kan me no endra klassen `Book` slik at han arvar frå `Loanable`? La oss ta utgangspunkt i ein enkel versjon av bokklassen:


```python
class Book:
    def __init__(self, title, author, number_of_pages):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
```

No kan me endra den første linja til `class Book(Loanable)`. Det fortel at klassen `Book` skal arva frå klassen `Loanable`. Merk at superklassen må vera definert først!


```python
class Book(Loanable):
    def __init__(self, title, author, number_of_pages):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
```

Me kan no oppretta eit bokobjekt på vanleg måte:


```python
my_book = Book("Sofies verden", "Jostein Gaarder", 512)
```

Sidan `Book` arvar alle metodane til `Loanable`, kan eit bokobjekt utføra desse metodane:


```python
my_book.register_loan("Per Hansen")
```

Loan registered:  Sofies verd  ->  Per Hansen


Når du programmerer klassen `Book`, så har du også tilgang til alle datafelt og metodar frå superklassen. Desse kan brukast som byggjeblokker til nye metodar:


```python
class Book(Loanable):
    def renew(self, person):
        self.register_delivery()
        self.register_loan(person)
```

Metodane `register_delivery()` og `register_loan()` er ikkje noko me hentar utanfrå. Tvert imot er dei ein del av bokklassen! Klassen `Book` består nemleg av alle metodane me har definert i klasseblokka, **pluss** alle metodane som kjem frå superklassane til `Book`.

