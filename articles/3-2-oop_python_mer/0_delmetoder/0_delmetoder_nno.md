---
title: "Delmetodar"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
	- "python_book_public_private.svg"
	- "python_interface.svg"
---

I boksystemet vårt ønsket me å kunna visa ei rangert liste av bøker. Følgjande klassediagram viser metodane me treng for å oppnå dette:

<img src="/media/markdowncontent/assosiated_files/python_book_public_private.svg" width="">

Følgjande figur viser korleis nokre metodar blir brukte som byggjeblokker til andre metodar:

<img src="/media/markdowncontent/assosiated_files/python_interface.svg" width="1000">

Kvar skal me starta? Me kan sjå at nesten alle metodane er avhengig av nokre andre metodar for å fungera. Nettopp derfor er det lurt å laga figuren ovanfor, slik at me enkelt ser kvar me skal starta. Dei første byggjeblokkene som me treng er følgjande metodar:

- `get_reviews_from_goodreads()`
- `get_reviews_from_librarything()`
- `get_online_critics()`

Det er ofte i dei første metodane at mesteparten av kodearbeidet må gjerast. Derfor er det lurt å starta med å la desse metodane returnera nokre enkle testverdiar. I følgjande kode opprettar me derfor nokre fiktive meldingar, og ein funksjon som returnerer eit tilfeldig utval av desse:


```python
from random import sample

r1 = ["Veldig interessant bok", 9]
r2 = ["Boken var for lang", 5]
r3 = ["Slutten ødela boken", 2]
r4 = ["En bok som får deg til å tenke", 7]
r5 = ["Handlingen var veldig spennende", 8]

all_reviews = [r1, r2, r3, r4, r5]

def get_random_reviews(n):
	return sample(all_reviews, n)

print(get_random_reviews(3))
```

[['Boken var for lang', 5], ['Handlingen var veldig spennande', 8], ['Slutten øydela boka', 2]]


Funksjonen `get_random_reviews` hentar eit altså tilfeldig utval av dei fem testmeldingane me har skrive.

No kan me oppretta dei første metodane, som skal vera i klassen `Book`:


```python
 class Book:
    def __init__(self, title, author, number_of_pages):
        self.title = title
        self.author = author
        self.number_of_pages = number_of_pages
        self.borrower_reviews = get_random_reviews(3)

    def get_reviews_from_goodreads(self):
    	reviews = get_random_reviews(3)
    	return reviews

    def get_reviews_from_librarything(self):
    	reviews = get_random_reviews(3)
    	return reviews

    def get_online_critics(self):
    	critics = get_random_reviews(3)
    	return critics 
```

No kan me lata som me har meldingar frå fleire ulike kjelder:
* Datafeltet `borrower_reviews`, altså meldingar som me har registrert frå våre eigne brukarar. Me har sørgt for at konstruktøren fyller datafeltet med testmeldingar.
* Tre metodar for å henta meldingar på nett. Alle desse returner testmeldingar.

Det neste me ønskjer er ein metode som samlar alle brukarmeldingar på nett. Sidan me allereie har ein metode for kvar av nettsidene me ønskjer å henta brukarmeldingar frå, blir dette enkelt:


```python
def get_online_user_reviews(self):
	from_goodreads = self.get_reviews_from_goodreads()
	from_librarything = self.get_reviews_from_librarything()
	reviews = from_librarything + from_goodreads
	return reviews 

Book.get_online_user_reviews = get_online_user_reviews
```

*I siste linje bruker me ein teknikk i Python for å leggja til ein metode i ein eksisterande klasse. Me kan bruka følgjande kodelinje for å gjera dette:*
```py
MyClass.my_method = my_function
```
* *`MyClass` namnet på klassen*
* *`my_function` er namnet på funksjonen som me har definert utanfor klassen*
* *`my_method` er namnet me ønskjer at funksjonen skal ha inni klassen*

Det neste me ønskjer oss er ein funksjon som kan rekna ut gjennomsnittet til ei liste med meldingar:


```python
def calculate_average(reviews):
	total_score = 0
	n = len(reviews)
	for review in reviews:
		score = review[1]
		total_score += score
	average = total_score/n
	return average

reviews = get_random_reviews(3)
print(reviews)
print(calculate_average(reviews))
```

[['Handlingen var veldig spennande', 8], ['Boken var for lang', 5], ['Ei bok som får deg til å tenkja', 7]]
    6.666666666666667


Les utskrifta for å sjå at metoden reknar ut rett gjennomsnitt, og forsøk gjerne å forstå korleis utrekninga blir gjord.

*I planlegginga av programmet plasserte me denne funksjonen i klassen `Book`. Men her ser me at funksjonen eigentleg berre gjer ein operasjon på ei liste med tal, og me har derfor valt å plassera den utanfor klasseblokka.*


No er me klare til å koda metoden som reknar ut gjennomsnittsvurderinga til ei bok! Funksjonen skal:

1. Henta meldingar frå tre ulike kjelder; lånetakarar, nettbrukarar og kritikarar.
2. Rekna ut gjennomsnittsvurderinga for kvar av desse kjeldene.
3. Rekna ut eit totalt gjennomsnitt.


```python
def calculate_average_score(self): 
	borrowers = self.borrower_reviews
	online_users = self.get_online_user_reviews()
	critics = self.get_online_critics()

	score_borrowers = calculate_average(borrowers)
	score_online_users = calculate_average(online_users)
	score_critics = calculate_average(critics)

	total_score = (score_borrowers + score_online_users + score_critics)/3

	return total_score

Book.calculate_average_score = calculate_average_score
```

Legg merke til korleis dei tre stega blir til tre blokker med kode. I dei to første blokkene blir gjort alt arbeidet av delmetodane, medan det er det siste steget som er metoden sitt "eige arbeid". I denne linja kan me endra kor mykje dei ulike kjeldene skal vektast. Viss me til dømes ønskjer at vurderingar frå nettbrukarar skal telja 50%, medan dei andre kjeldene skal telja 25% kvar, kan me endra til følgjande:

```py
total_score = 0.25*score_borrowers + 0.5*score_online_users + 0.25*score_critics
```

