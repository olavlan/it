---
title: "Sette inn en konstruktør"
belongs_to_chain: "Klasser og objekter i Python"
figures_to_include:
	- "python_class_book_constructor.svg"
	- "python_class_person.svg"
---


Tenk deg at vi skal registrere boka *Sofies verden* i systemet. Foreløpig har vi vist hvordan vi kan gjøre dette i to steg: 

1. Vi opprettet et *tomt* bokobjekt med kommandoen `book1 = Book()`. Vi sier at objektet er tomt fordi datafeltene ikke har spesifikke verdier - objektet har bare fått standardverdiene vi definerte i klassen. 
2. Deretter satte vi inn riktige verdier ved å skrive:


```python
book1.title = "Sofies verden"
book1.author = "Jostein Gaarder"
book1.number_of_pages = 512
```

I stedet for å gå gjennom disse stegene, hadde det vært praktisk å kunne bruke kommandoen`Book("Sofies verden", "Jostein Gaarder", 512)` for å opprette objektet. Hva slags metode trenger vi for dette? En konstruktør!

Vi har sett hvordan vi legger til en konstruktør i klassediagrammet:

<img src="/media/markdowncontent/assosiated_files/python_class_book_constructor.svg" width="25%">

En konstruktør bestemmer hva som skal gjøres med et nyopprettet objekt. Vår konstruktør skal opprette datafeltene `title`, `author` og `number_of_pages` i det nye objektet, og fylle disse med parameterverdiene. Hvordan lager vi en konstruktør som gjør dette i Python? 

Når vi oppretter en klasse i Python, får klassen automatisk en metode som kalles  `__init__()` (merk at det er to understreker på hver side).  Denne er i utgangspunktet skjult for oss, men i Python kan vi alltid endre på en metode ved å skrive den opp på nytt:


```python
class Book:
    def __init__(self):
        print("You have just created the object ", self)

Book()
```

    You have just created the object  <__main__.Book object at 0x7f3c6c43fd00>





    <__main__.Book at 0x7f3c6c43fd00>



Her laget vi altså en konstruktør som skriver ut en melding. Men hva er det egentlig som skjer? Hvorfor skrev vi ikke `__init__()` for å kalle på metoden?

* Når Python ser kommandoen `Book()`, så vil den automatisk kjøre funksjonen `__init()__` fra klassen `Book`. Det er altså `__init()__` som er konstruktøren, men for å bruke konstruktøren, må vi skrive `Book()`.

Nå kan vi sørge for at konstruktøren gjør det vi ønsker, nemlig å opprette datafelter og fylle dem med ønskede verdier:


```python
class Book:
    def __init__(self, title, author, number_of_pages):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages

book4 = Book("Sofies verden", "Jostein Gaarder", 512)
print(book4.title)
```

    Sofies verden


Her kunne vi opprette et bokobjekt på akkurat den måten vi ønsket!

I koden til konstruktøren er det viktig å forstå at `self.title` og `title` er to forskjellige variabler:

* `self.title ` er en variabel som settes inn i det nye objektet
* `title` er en variabel som kommer fra parameteren
* Når vi skriver `self.title = title`, så oppretter vi altså et datafelt i objektet, og fyller den med verdien fra parameteren `title`.

De fleste konstruktører har denne grunnleggende strukturen, så nå er det enkelt å lage konstruktører for andre klasser i boksystemet vårt, for eksempel klassen `Person`:

<img src="/media/markdowncontent/assosiated_files/python_class_person.svg" width="150">

En første versjon av klassen `Person` kan inneholde en konstruktør. Det er nok til å opprette personobjekter på en enkel måte:


```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person1 = Person("Per Hansen", 70)
print(person1.name)
```

    Per Hansen


