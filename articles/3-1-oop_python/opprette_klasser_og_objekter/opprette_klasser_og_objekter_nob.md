---
title: "Opprette klasser og objekter"
belongs_to_chain: "Klasser og objekter i Python"
figures_to_include:
	- "python_klasse_objekter_bok.svg"
	- "python_class_book.svg"
	- "python_pointers.svg"
---

I planleggingen av bokprogrammet vår definerte vi klassen `Bok`, og viste hvordan objekter kan opprettes fra denne klassen: 

<img src="/media/markdowncontent/assosiated_files/python_klasse_objekter_bok.svg" width="40%">

Hvordan kan vi opprette disse objektene i Python? Det er temaet for denne seksjonen! 

I dette kapitlet kommer vi til å vise mange kodeeksempler, og koden vil alltid være på engelsk! Å bruke engelsk som språk er viktig når vi skriver kode som skal leses av andre enn oss selv. Men også når vi programmerer for oss selv er det lurt å innarbeide denne vanen. Dessuten kan personlige prosjekter alltid bli til noe større senere!

- Bruk alltid engelsk som språk når du programmerer. Alle navn som du velger selv (for variabler, klasser og metoder) bør være på engelsk. 

Da vi planla og skisserte bokprogrammet brukte vi bare norske navn. Derfor er det første steget å oversette klassediagrammet til engelsk: 

<img src="/media/markdowncontent/assosiated_files/python_class_book.svg" width="15%">

Nå er vi klare til å programmere! I Python må vi definere en klasse først, og deretter kan vi opprette objekter fra klassen. Vi begynner med en svært enkel versjon av klassen:


```python
class Book:
    title = ""
    author = ""
    number_of_pages = 0
```

Vi følger alltid denne strukturen når vi oppretter en klasse: 

1. På den første linjen skriver vi `class Name:`, der `Name` skal være navnet til klassen.
2. Deretter følger en innrykket blokk, hvor vi skriver innholdet i klassen, det vil si alle datafelter og metoder.
3. Når vi slutter å bruke innrykk  er vi utenfor klassen. 

I klassen har vi definert de ønskede datafeltene (`title`, `author` og `number_of_pages`) og gitt dem noen standardverdier. Nå kan vi opprette vårt første objekt:


```python
Book()
```




    <__main__.Book at 0x7f3c6c460d90>



For å opprette et objekt skriver vi altså klassenavnet etterfulgt av parenteser. Når vi kjører dette programmet, så vil et objekt opprettes og plasseres i minnet. Men for at vi skal finne objektet senere må vi lagre minneadressen i en variabel. Derfor oppretter vi vanligvis objekter på følgende måte:


```python
book1 = Book()
```

Variabelen `book1` lagrer minneadressen for oss, slik at vi kan finne objektet og gjøre operasjoner på det, som for eksempel å endre et av datafeltene:


```python
book1.title = "Sofies verden"
```

Punktumet i `book1.title` er svært viktig, for det forteller at vi skal hente en variabel som ligger inni objektet. Vi bruker alltid punktum for å "gå inn" på et objekt: 

* For å hente datafelter eller metoder inni et objekt bruker vi følgende skrivemåte:
    * `object1.datafield1`
    * `object1.method1(p1, p2)`
* Forklaring av navn: 
    - `object1` er en variabel som inneholder minneadressen til objektet
    - `datafield1` er navnet på et datafelt i objektet
    - `method1` er navnet på en metode i objektet, og `p1` og `p2` er parametre

Følgende kode viser forskjellen på en variabel som "ligger fritt" og en variabel som ligger inni et objekt:


```python
title = "Når villdyret våkner"
print(title)
print(book1.title)
```

    Når villdyret våkner
    Sofies verden


Her har vi to variabler som begge heter `title`, men den ene variabelen ligger i et bokobjekt, mens den andre ligger fritt. Variabler som ligger i objekter kalles vanligvis *datafelter*. Vi har opprettet et bokobjekt som har tre datafelter:

- book1.title
- book1.author
- book1.number_of_pages

For å fullføre registreringen av boken *Sofies verden*, kan vi endre de resterende datafeltene:


```python
book1.author = "Jostein Gaarder"
book1.number_of_pages = 512
```

For å se at det har fungert, kan vi printe ut datafeltene:


```python
print(book1.author)
print(book1.number_of_pages)
```

    Jostein Gaarder
    512


Men hva skjer hvis vi forsøker å printe variabelen `book1`?


```python
print(book1)
```

    <__main__.Book object at 0x7f3c6d4f1190>


Denne utskriften var litt kryptisk! Som vi har nevnt, så inneholder ikke `book1` selve objektet, men *minneadressen* til objektet. Det er nettopp denne adressen (`0x10cbff970`) vi får vite når vi printer variabelen `book1`. Derfor sier vi at `book1` *peker til objektet* som ligger på adressen. Det er ingenting i veien for å ha flere variabler som peker til det samme objektet:


```python
book2 = book1
```

Her kopierer vi minneadressen `0x10cbff970` (som ligger i `book1`) til variabelen `book2`. Ved å printe variablene kan vi sjekke at de peker til det samme objektet:


```python
print(book1)
print(book2)
```

    <__main__.Book object at 0x7f3c6d4f1190>
    <__main__.Book object at 0x7f3c6d4f1190>


Vi kan også vise dette i en figur: 

<img src="/media/markdowncontent/assosiated_files/python_pointers.svg" width="50%">

I denne seksjonen har vi sett hvordan vi oppretter objekter og samtidig lagrer minneadressen, slik at vi senere kan finne objektene og gjøre operasjoner på dem.


