---
title: "Get-metoder"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
---

Hva med når brukeren bare ønsker å hente et datafelt? For eksempel ønsker man kanskje å vite tittelen til en bok. Til dette formålet legger vi til en *get*-metode (også kalt *getter*, fra engelsk *to get*):


```python
class Book:
    def set_title(self, title):
        if type(title) == str:
            self._title = title
            
    def get_title(self):
        return self._title
```

Vi kan bruke denne forenklede klassen til å opprette et bokobjekt, endre tittelen, og til slutt hente tittelen:


```python
my_book = Book()
my_book.set_title("Sofies verden")
title = my_book.get_title()
print(title)
```

    Sofies verden


Husk at *Sofies verden* er en streng som ligger i minnet, og at variabelen `title` nå inneholder adressen til denne strengen. Men å ha tilgang til adressen gjør oss ikke i stand til å endre strengen! Dette er gode nyheter, for hvis ikke ville vi ha mislyktes i å beskytte datafeltet.

Hvorfor kan ikke strengen endres? I Python finnes to typer objekter: 

* Ikke-muterbare objekter (*immutable objects*): I denne kategorien finnes strenger, heltall, desimaltall, boolske verdier og tupler. Det finnes ingen måter å endre slike objekter, det er bare mulig å opprette nye.
* Muterbare objekter (*mutable objects*): Alle andre objekter kan endres. Et eksempel er en liste, fordi vi kan endre verdien på en bestemt indeks. Et annet eksempel er et objekt fra vår egen klasse, fordi vi kan endre verdien på et bestemt datafelt.

Vi kan vise denne forskjellen med følgende kode: 


```python
mutable = ["Hei"]
immutable = "Hei"

test1 = mutable
test2 = immutable

test1[0] = "Hade"
print(mutable)
```

    ['Hade']


Her har vi opprettet et ikke-muterbart og et muterbart objekt. Minneadressene til disse objektene kopieres deretter til `test1` og `test2`.
* Vi kan bruke `test1` til å endre `mutable`, fordi variablene peker til det samme, muterbare objektet.
* Vi kan ikke bruke `test2` til å endre `immutable` (dersom vi skriver `test2 = "Hade"`, oppnår vi bare at `test` peker til et nytt objekt, mens `immutable` fortsetter å peke til det gamle objektet). 

Som konklusjon kan vi si at det er trygt å lage følgende gettere:


```python
class Book:
    def get_title(self):
        return self._title

    def get_author(self):
        return self._author

    def get_number_of_pages(self):
        return self._number_of_pages
```

Siden vi returnerer ikke-muterbare objekter (strenger og heltall), kan disse ikke endres av brukeren. Altså er datafeltene beskyttet. 

Men hva om vi ønsker å ha en *get*-metode for datafeltet `_borrower_reviews`? Vi kan jo ikke returnere dette objektet, for det er jo en liste og dermed muterbart! Den eneste måten å beskytte objektet er å returnere en kopi!


```python
class Book:
    def get_borrower_reviews(self):
        return copy(self.borrower_reviews)
```

Funksjonen `copy` er innebygd i Python, og er viktig å bruke når vi ønsker å returnere verdiene i et objekt, men beskytte selve objektet fra å bli endret. Merk at hvis vi skal returnere et objekt som inneholder indre objekter (for eksempel en liste av bokobjekter), må vi bruke funksjonen `deepcopy`, som også oppretter kopier av alle de indre objektene. 

