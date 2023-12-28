---
title: "Opprette klassar og objekt"
belongs_to_chain: "Klasser og objekter i Python"
figures_to_include:
	- "python_klasse_objekter_bok.svg"
	- "python_class_book.svg"
	- "python_pointers.svg"
---

I planlegginga av bokprogrammet vår definerte me klassen `Bok`, og viste korleis objekt kan opprettast frå denne klassen:

<img src="/media/markdowncontent/assosiated_files/python_klasse_objekter_bok.svg" width="40%">

Korleis kan me oppretta desse objekta i Python? Det er temaet for denne seksjonen!

I dette kapittelet kjem me til å visa mange kodedøme, og koden vil alltid vera på engelsk! Å bruka engelsk som språk er viktig når me skriv kode som skal lesast av andre enn oss sjølv. Men også når me programmerer for oss sjølv er det lurt å innarbeida denne vanen. Dessutan kan personlege prosjekt alltid bli til noko større seinare!

- Bruk alltid engelsk som språk når du programmerer. Alle namn som du vel sjølv (for variablar, klassar og metodar) bør vera på engelsk.

Då me planla og skisserte bokprogrammet brukte me berre norske namn. Derfor er det første steget å omsetja klassediagrammet til engelsk:

<img src="/media/markdowncontent/assosiated_files/python_class_book.svg" width="15%">

No er me klare til å programmera! I Python må me definera ein klasse først, og deretter kan me opprette objekt frå klassen. Me byrjar med ein svært enkel versjon av klassen:


```python
class Book:
    title = ""
    author = ""
    number_of_pages = 0
```

Me følgjer alltid denne strukturen når me opprettar ein klasse:

1. På den første linja skriv me `class Name:`, der `Name` skal vera namnet til klassen.
2. Deretter følgjer ei rykt inn blokk, der me skriv innhaldet i klassen, det vil seia alle datafelt og metodar.
3. Når me sluttar å bruka innrykk  er me utanfor klassen.

I klassen har me definert dei ønskte datafelta (`title`, `author` og `number_of_pages`) og gitt dei nokre standardverdiar. No kan me oppretta vårt første objekt:


```python
Book()
```




<__main__.Book at 0x7f3c6c460d90>



For å oppretta eit objekt skriv me altså klassenamnet etterfølgd av parentesar. Når me køyrer dette programmet, så vil eit objekt opprettast og blir plassert i minnet. Men for at me skal finna objektet seinare må me lagra minneadressa i ein variabel. Derfor opprettar me vanlegvis objekt på følgjande måte:


```python
book1 = Book()
```

Variabelen `book1` lagrar minneadressa for oss, slik at me kan finna objektet og gjera operasjonar på det, som til dømes å endra eit av datafelta:


```python
book1.title = "Sofies verden"
```

Punktumet i `book1.title` er svært viktig, for det fortel at me skal henta ein variabel som ligg inni objektet. Me bruker alltid punktum for å "gå inn" på eit objekt:

* For å henta datafelt eller metodar inni eit objekt bruker me følgjande skrivemåte:
* `object1.datafield1`
* `object1.method1(p1, p2)`
* Forklaring av namn:
- `object1` er ein variabel som inneheld minneadressa til objektet
- `datafield1` er namnet på eit datafelt i objektet
- `method1` er namnet på ein metode i objektet, og `p1` og `p2` er parametrar

Følgjande kode viser forskjellen på ein variabel som "ligg fritt" og ein variabel som ligg inni eit objekt:


```python
title = "Når villdyret våkner"
print(title)
print(book1.title)
```

Når villdyret vaknar
Sofies verd


Her har me to variablar som begge heiter `title`, men den eine variabelen ligg i eit bokobjekt, medan den andre ligg fritt. Variablar som ligg i objekt blir vanlegvis kalla *datafelt*. Me har oppretta eit bokobjekt som har tre datafelt:

- book1.title
- book1.author
- book1.number_of_pages

For å fullføra registreringa av boka *Sofies verd*, kan me endra dei resterande datafelta:


```python
book1.author = "Jostein Gaarder"
book1.number_of_pages = 512
```

For å sjå at det har fungert, kan me skriva ut datafelta:


```python
print(book1.author)
print(book1.number_of_pages)
```

Jostein Gaarder
    512


Men kva skjer viss me prøver å skriva ut variabelen `book1`?


```python
print(book1)
```

<__main__.Book object at 0x7f3c6d4f1190>


Denne utskrifta var litt kryptisk! Som me har nemnt, så inneheld ikkje `book1` sjølve objektet, men *minneadressa* til objektet. Det er nettopp denne adressa (`0x10cbff970`) me får vita når me skriv ut variabelen `book1`. Derfor seier me at `book1` *peikar til objektet* som ligg på adressa. Det er ingenting i vegen for å ha fleire variablar som peikar til det same objektet:


```python
book2 = book1
```

Her kopierer me minneadressa `0x10cbff970` (som ligg i `book1`) til variabelen `book2`. Ved å skriva ut variablane kan me sjekka at dei peikar til det same objektet:


```python
print(book1)
print(book2)
```

<__main__.Book object at 0x7f3c6d4f1190>
<__main__.Book object at 0x7f3c6d4f1190>


Me kan også visa dette i ein figur:

<img src="/media/markdowncontent/assosiated_files/python_pointers.svg" width="50%">

I denne seksjonen har me sett korleis me opprettar objekt og samtidig lagrar minneadressa, slik at me seinare kan finna objekta og gjera operasjonar på dei.


