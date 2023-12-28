---
title: "Get-metodar"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
---

Kva med når brukaren berre ønskjer å henta eit datafelt? Til dømes ønskjer ein kanskje å vita tittelen til ei bok. Til dette formålet legg me til ein *get*-metode (også kalla *getter*, frå engelsk *to get*):


```python
class Book:
    def set_title(self, title):
        if type(title) == str:
            self._title = title
            
    def get_title(self):
        return self._title
```

Me kan bruka denne forenkla klassen til å oppretta eit bokobjekt, endra tittelen, og til slutt henta tittelen:


```python
my_book = Book()
my_book.set_title("Sofies verden")
title = my_book.get_title()
print(title)
```

Sofies verd


Hugs at *Sofies verd* er ein streng som ligg i minnet, og at variabelen `title` no inneheld adressa til denne strengen. Men å ha tilgang til adressa gjer oss ikkje i stand til å endra strengen! Dette er gode nyheiter, for viss ikkje ville me ha mislykkast i å verna datafeltet.

Kvifor kan ikkje strengen endrast? I Python finst to typar objekt:

* Ikke-muterbare objekt (*immutable objects*): I denne kategorien finst strenger, heiltal, desimaltal, boolske verdiar og tupler. Det finst ingen måtar å endra slike objekt, det er berre mogleg å oppretta nye.
* Muterbare objekt (*mutable objects*): Alle andre objekt kan endrast. Eit døme er ei liste, fordi me kan endra verdien på ein bestemd indeks. Eit anna døme er eit objekt frå vår eigen klasse, fordi me kan endra verdien på eit bestemt datafelt.

Me kan visa denne forskjellen med følgjande kode:


```python
mutable = ["Hei"]
immutable = "Hei"

test1 = mutable
test2 = immutable

test1[0] = "Hade"
print(mutable)
```

['Hade']


Her har me oppretta eit ikke-muterbart og eit muterbart objekt. Minneadressene til desse objekta blir deretter kopierte til `test1` og `test2`.
* Me kan bruka `test1` til å endra `mutable`, fordi variablane peikar til det same, muterbare objektet.
* Me kan ikkje bruka `test2` til å endra `immutable` (dersom me skriv `test2 = "Hade"`, oppnår me berre at `test` peikar til eit nytt objekt, medan `immutable` held fram med å peika til det gamle objektet).

Som konklusjon kan me seia at det er trygt å laga følgjande gettere:


```python
class Book:
    def get_title(self):
        return self._title

    def get_author(self):
        return self._author

    def get_number_of_pages(self):
        return self._number_of_pages
```

Sidan me returnerer ikke-muterbare objekt (strenger og heiltal), kan desse ikkje blir endra av brukaren. Altså er datafelta verna.

Men kva om me ønskjer å ha ein *get*-metode for datafeltet `_borrower_reviews`? Me kan jo ikkje returnera dette objektet, for det er jo ei liste og dermed muterbart! Den einaste måten å verna objektet er å returnera ein kopi!


```python
class Book:
    def get_borrower_reviews(self):
        return copy(self.borrower_reviews)
```

Funksjonen `copy` er innebygd i Python, og er viktig å bruka når me ønskjer å returnera verdiane i eit objekt, men verna sjølve objektet frå å bli endra. Merk at viss me skal returnera eit objekt som inneheld indre objekt (til dømes ei liste av bokobjekt), må me bruka funksjonen `deepcopy`, som også opprettar kopiar av alle dei indre objekta.

