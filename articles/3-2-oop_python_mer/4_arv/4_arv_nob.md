---
title: "Arv"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
	- "inheritance.svg"
---

Fra seksjonene om arv fra kapittelet *Konsepter i objektorientert programmering* kom vi fram til følgende klassediagram: 

<img src="/media/markdowncontent/assosiated_files/inheritance.svg" width="400">

*Dette klassediagrammet er oversatt til engelsk og litt modifisert. Vi hadde klassen `Utlånsobjekt`, som vi har oversatt til `Loanable`. Vi kan tenke på dette som en kortversjon av *"Loanable object"*. I slike navn er det vanlig å utelate ordet *object* i klassenavnet.*

Klassene `Book` og `Movie` skal arve datafeltene og metodene til klassen `Loanable`. Hvordan får vi til dette i Python? 

Superklassen `Loanable` arver ikke fra noen klasser, så denne kan programmeres på vanlig måte:


```python
class Loanable:
    def register_loan(self, person):
        print("Loan registered: ", title, " -> ", person)

    def register_delivery(self):
        print("Delivery registered: ", title)
```

*På dette stadiet er det ikke viktig at vi har fungerende kode, så vi kan begynne med å printe ut noen enkle meldinger.*

Hvordan kan vi nå endre klassen `Book` slik at den arver fra `Loanable`? La oss ta utgangspunkt i en enkel versjon av bokklassen: 


```python
class Book:
    def __init__(self, title, author, number_of_pages):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
```

Nå kan vi endre den første linjen til `class Book(Loanable)`. Det forteller at klassen `Book` skal arve fra klassen `Loanable`. Merk at superklassen må være definert først!


```python
class Book(Loanable):
    def __init__(self, title, author, number_of_pages):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
```

Vi kan nå opprette et bokobjekt på vanlig måte:


```python
my_book = Book("Sofies verden", "Jostein Gaarder", 512)
```

Siden `Book` arver alle metodene til `Loanable`, kan et bokobjekt utføre disse metodene: 


```python
my_book.register_loan("Per Hansen")
```

    Loan registered:  Sofies verden  ->  Per Hansen


Når du programmerer klassen `Book`, så har du også tilgang til alle datafelter og metoder fra superklassen. Disse kan brukes som byggeblokker til nye metoder: 


```python
class Book(Loanable):
    def renew(self, person):
        self.register_delivery()
        self.register_loan(person)
```

Metodene `register_delivery()` og `register_loan()` er ikke noe vi henter utenfra. Tvert imot er de en del av bokklassen! Klassen `Book` består nemlig av alle metodene vi har definert i klasseblokken, **pluss** alle metodene som kommer fra superklassene til `Book`.

