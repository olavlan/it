---
title: "Dokumentasjon"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
---

Målet i denne seksjonen er å gjøre det lettere for brukerne av bokklassen å se hvilke metoder som er offentlige og hvordan de brukes. Til dette formålet kan vi skrive en dokumentasjon, og den kan skrives direkte i kodefilen!

Du vet kanskje hvordan man skriver kommentarer i Python? Kommentarer er tekst som ikke er kode, og som ikke regnes med når vi kjører kodefilen. Det finnes to måter å skrive kommentarer i Python:


```python
# Dette er en kommentar på én linje

""" Dette er en kommentar
som går over
flere linjer.
"""
```




    ' Dette er en kommentar\nsom går over\nflere linjer.\n'



Det er kommentarene som går over flere linjer vi skal bruke når vi skriver dokumentasjon for en klasse. 

I stedet for å forklare hver del i detalj, går vi rett på sak og viser en full dokumentasjon av bokklassen. For presentasjonen sin del har vi utelatt koden i dette eksempelet (vi har skrevet `pass` der vi ellers ville hatt kode). Det er lurt å skrive dokumentasjonen på engelsk, slik at klassen blir mest mulig tilgjengelig (det kan hende at vi ønsker å publisere klassen senere):


```python
class Book: 
    """Class used to represent a physical book

    Public methods
    -------
    Book(title, author, number_of_pages)
        Creates a new book object from given data

    Book(isbn)
        Creates a new book object from ISBN

    set_title(title)
        Sets a new title for the book

    get_title()
        Returns the title of the book

    calculate_average()
        Returns a score between 0 and 10 based on reviews from different sources 
    """
    
    def __init__(self, title=None, author=None, number_of_pages=None, isbn=None):
        """
        Creates a new book object

        If the parameter isbn is passed, attempts to find the book data in a database.
        Otherwise uses the other parameters.

        Parameters
        ----------
        title : str, optional
            The full title of the book (default is None)
        author : str, optional
            The full name of the author, on the form "[First name] [Surname]" (default is None)
        number_of_pages : int, optional
            The number of pages in the book (default is None)
        isbn : int, optional
            The ISBN of the book (default is None)
        """
        pass

    def set_title(self, title):
        """
        Sets a new title for the book

        Parameters
        ----------
        title : str, optional
            The new title of the book

        Returns
        -------
        None
        """
        
        pass

    def get_title(self):
        """
        Returns the title of the book 

        Returns
        -------
        string
            The title of the book
        """
        pass

    def calculate_average_score(self):
        """
        Returns a score between 0 and 10
        
        The score is based on reviews from the following sources:
        * Reviews from borrowers of the book
        * Online user reviews: Bokelskere, Goodreads
        * Online critics

        Returns
        -------
        float
            A decimal number between 0 and 10 if at least one review is found.
            Otherwise -1 (if no reviews are found).   
        """
        
        pass
```

**Forklaring.** Vi dokumenterer både klassen i seg selv og alle metodene. Dokumentasjon av klassen skal komme rett etter `class Book:`, altså i starten av klasseblokken. Tilsvarende skal dokumentasjon av en metode komme i starten av metodeblokken.

Vi strukturerer dokumentasjonen slik: 
1. Den første linjen skal med en kort setning forklare hva klassen eller metoden gjør.
2. På de neste linjene kan man, hvis ønskelig, skrive en lengre forklaring av klassen eller metoden.
3. Deretter kommer det an på om man dokumenterer en klasse eller metode:
    * **Klasse:** Under overskriften *Public methods* lister vi opp alle de offentlige metodene. Under hver metode skriver vi en kort forklaring av hva metoden gjør. Dersom en metode kan brukes på forskjellige måter (med valgfrie parametre), lister vi alle måtene den kan brukes.
    * **Metoder:** Under overskriften *Parameters* lister vi alle parametre (dersom metoden har parametre). For hver parameter skriver vi navn og datatype, og på neste linje en kort beskrivelse av hva parameteren skal inneholde. Under overskriften *Returns* gir vi en tilsvarende beskrivelse av returverdien (dersom metoden har returverdi).

Husk å inkludere et ekstra linjeskift mellom hver av punktene 1-3. 

Hva er poenget med å skrive dokumentasjonen på akkurat denne måten? Ved å følge denne standarden, vil alle som er kjent med Python-programmering forstå dokumentasjonen! En annen fordel er at når noen importerer klassen din, kan de enkelt hente dokumentasjon for klasser og metoder:


```python
my_book = Book()
help(my_book.calculate_average_score)
```

    Help on method calculate_average_score in module __main__:
    
    calculate_average_score() method of __main__.Book instance
        Returns a score between 0 and 10
        
        The score is based on reviews from the following sources:
        * Reviews from borrowers of the book
        * Online user reviews: Bokelskere, Goodreads
        * Online critics
        
        Returns
        -------
        float
            A decimal number between 0 and 10 if at least one review is found.
            Otherwise -1 (if no reviews are found).
    


For å hente dokumentasjonen til hele klassen, brukes kommandoen `help(my_book)` eller `help(Book)`.

