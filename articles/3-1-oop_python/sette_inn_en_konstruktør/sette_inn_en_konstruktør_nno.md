---
title: "Setja inn ein konstruktør"
belongs_to_chain: "Klasser og objekter i Python"
figures_to_include:
	- "python_class_book_constructor.svg"
	- "python_class_person.svg"
---


Tenk deg at me skal registrera boka *Sofies verd* i systemet. Førebels har me vist korleis me kan gjera dette i to steg:

1. Me oppretta eit *tomt* bokobjekt med kommandoen `book1 = Book()`. Me seier at objektet er tomt fordi datafelta ikkje har spesifikke verdiar - objektet har berre fått standardverdiane me definerte i klassen.
2. Deretter sette me inn rette verdiar ved å skriva:


```python
book1.title = "Sofies verden"
book1.author = "Jostein Gaarder"
book1.number_of_pages = 512
```

I staden for å gå gjennom desse stega, hadde det vore praktisk å kunna bruka kommandoen`Book("Sofies verden", "Jostein Gaarder", 512)` for å oppretta objektet. Kva slags metode treng me for dette? Ein konstruktør!

Me har sett korleis me legg til ein konstruktør i klassediagrammet:

<img src="/media/markdowncontent/assosiated_files/python_class_book_constructor.svg" width="25%">

Ein konstruktør bestemmer kva som skal gjerast med eit nyoppretta objekt. Konstruktøren vår skal oppretta datafelta `title`, `author` og `number_of_pages` i det nye objektet, og fylla desse med parametersverdiane. Korleis lagar me ein konstruktør som gjer dette i Python?

Når me opprettar ein klasse i Python, får klassen automatisk ein metode som blir kalla  `__init__()` (merk at det er to understrekar på kvar side).  Denne er i utgangspunktet skjult for oss, men i Python kan me alltid endra på ein metode ved å skriva han opp på nytt:


```python
class Book:
    def __init__(self):
        print("You have just created the object ", self)

Book()
```

You have just created the object  <__main__.Book object at 0x7f3c6c43fd00>





<__main__.Book at 0x7f3c6c43fd00>



Her laga me altså ein konstruktør som skriv ut ei melding. Men kva er det eigentleg som skjer? Kvifor skreiv me ikkje `__init__()` for å kalla på metoden?

* Når Python ser kommandoen `Book()`, så vil han automatisk køyra funksjonen `__init()__` frå klassen `Book`. Det er altså `__init()__` som er konstruktøren, men for å bruka konstruktøren, må me skriva `Book()`.

No kan me sørgja for at konstruktøren gjer det me ønskjer, nemleg å oppretta datafelt og fylla dei med ønskte verdiar:


```python
class Book:
    def __init__(self, title, author, number_of_pages):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages

book4 = Book("Sofies verden", "Jostein Gaarder", 512)
print(book4.title)
```

Sofies verd


Her kunne me oppretta eit bokobjekt på akkurat den måten me ønskte!

I koden til konstruktøren er det viktig å forstå at `self.title` og `title` er to ulike variablar:

* `self.title ` er ein variabel som blir sett inn i det nye objektet
* `title` er ein variabel som kjem frå parameteren
* Når me skriv `self.title = title`, så opprettar me altså eit datafelt i objektet, og fyller han med verdien frå parameteren `title`.

Dei fleste konstruktørar har denne grunnleggjande strukturen, så no er det enkelt å laga konstruktørar for andre klassar i boksystemet vårt, til dømes klassen `Person`:

<img src="/media/markdowncontent/assosiated_files/python_class_person.svg" width="150">

Ein første versjon av klassen `Person` kan innehalda ein konstruktør. Det er nok til å oppretta personobjekt på ein enkel måte:


```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person1 = Person("Per Hansen", 70)
print(person1.name)
```

Per Hansen


