---
title: "Dokumentasjon"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
---

Målet i denne seksjonen er å gjera det lettare for brukarane av bokklassen å sjå kva metodar som er offentlege og korleis dei blir brukte. Til dette formålet kan me skriva ein dokumentasjon, og han kan skrivast direkte i kodefila!

Du veit kanskje korleis ein skriv kommentarar i Python? Kommentarar er tekst som ikkje er kode, og som ikkje blir rekna med når me køyrer kodefila. Det finst to måtar å skriva kommentarar i Python:


```python
# Dette er en kommentar på én linje

""" Dette er en kommentar
som går over
flere linjer.
"""
```




' Dette er ein kommentar\nsom går over\nflere linjer.\n'



Det er kommentarane som går over fleire linjer me skal bruka når me skriv dokumentasjon for ein klasse.

I staden for å forklara kvar del i detalj, går me rett på sak og viser ein full dokumentasjon av bokklassen. For presentasjonen sin del har me utelate koden i dette dømet (me har skrive `pass` der me elles ville hatt kode). Det er lurt å skriva dokumentasjonen på engelsk, slik at klassen blir mest mogleg tilgjengeleg (det kan hende at me ønskjer å publisera klassen seinare):


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

**Forklaring.** Me dokumenterer både klassen i seg sjølv og alle metodane. Dokumentasjon av klassen skal komma rett etter `class Book:`, altså i starten av klasseblokka. Tilsvarande skal dokumentasjon av ein metode komma i starten av metodeblokka.

Me strukturerer dokumentasjonen slik:
1. Den første linja skal med ei kort setning forklara kva klassen eller metoden gjer.
2. På dei neste linjene kan ein, viss ønskjeleg, skriva ei lengre forklaring av klassen eller metoden.
3. Deretter kjem det an på om ein dokumenterer ein klasse eller metode:
* **Klasse:** Under overskrifta *Public methods* lister me opp alle dei offentlege metodane. Under kvar metode skriv me ei kort forklaring av kva metoden gjer. Dersom ein metode kan brukast på ulike måtar (med valfrie parametrar), listar me alle måtane han kan brukast.
* **Metodar:** Under overskrifta *Parameters* listar me alle parametrar (dersom metoden har parametrar). For kvar parameter skriv me namn og datatype, og på neste linje ei kort skildring av kva parameteren skal innehalda. Under overskrifta *Returns* gir me ei tilsvarande skildring av returverdien (dersom metoden har returverdi).

Hugs å inkludera eit ekstra linjeskift mellom kvart av punkta 1-3.

Kva er poenget med å skriva dokumentasjonen på akkurat denne måten? Ved å følgja denne standarden, vil alle som er kjende med Python-programmering forstå dokumentasjonen! Ein annan fordel er at når nokon importerer klassen din, kan dei enkelt henta dokumentasjon for klassar og metodar:


```python
my_book = Book()
help(my_book.calculate_average_score)
```

Help on method calculate_average_skår in module __main__:
    
calculate_average_skår() method of __main__.Book instance
Returns a skår between 0 and 10
        
The skår is based on reviews from the following sources:
* Reviews from borrowers of the book
* Online user reviews: Bokelskarar, Goodreads
* Online critics
        
Returns
        -------
float
A decimal number between 0 and 10 if at least one review is found.
Otherwise -1 (if no reviews are found).
    


For å henta dokumentasjonen til heile klassen, blir kommandoen brukt `help(my_book)` eller `help(Book)`.

