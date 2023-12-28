---
title: "Delmetoder"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
	- "python_book_public_private.svg"
	- "python_interface.svg"
---

I boksystemet vårt ønsket vi å kunne vise en rangert liste av bøker. Følgende klassediagram viser metodene vi trenger for å oppnå dette:

<img src="/media/markdowncontent/assosiated_files/python_book_public_private.svg" width="">

Følgende figur viser hvordan noen metoder brukes som byggeblokker til andre metoder:

<img src="/media/markdowncontent/assosiated_files/python_interface.svg" width="1000">

Hvor skal vi starte? Vi kan se at nesten alle metodene er avhengig av noen andre metoder for å fungere. Nettopp derfor er det lurt å lage figuren ovenfor, slik at vi enkelt ser hvor vi skal starte. De første byggeblokkene som vi trenger er følgende metoder: 

- `get_reviews_from_goodreads()`
- `get_reviews_from_librarything()`
- `get_online_critics()`

Det er ofte i de første metodene at mesteparten av kodearbeidet må gjøres. Derfor er det lurt å starte med å la disse metodene returnere noen enkle testverdier. I følgende kode oppretter vi derfor noen fiktive anmeldelser, og en funksjon som returnerer et tilfeldig utvalg av disse: 


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

    [['Boken var for lang', 5], ['Handlingen var veldig spennende', 8], ['Slutten ødela boken', 2]]


Funksjonen `get_random_reviews` henter et altså tilfeldig utvalg av de fem testanmeldelsene vi har skrevet. 

Nå kan vi opprette de første metodene, som skal være i klassen `Book`:


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

Nå kan vi late som vi har anmeldelser fra flere forskjellige kilder: 
* Datafeltet `borrower_reviews`, altså anmeldelser som vi har registrert fra våre egne brukere. Vi har sørget for at konstruktøren fyller datafeltet med testanmeldelser.
* Tre metoder for å hente anmeldelser på nett. Alle disse returner testanmeldelser. 

Det neste vi ønsker er en metode som samler alle brukeranmeldelser på nett. Siden vi allerede har en metode for hver av nettsidene vi ønsker å hente brukeranmeldelser fra, blir dette enkelt: 


```python
def get_online_user_reviews(self):
	from_goodreads = self.get_reviews_from_goodreads()
	from_librarything = self.get_reviews_from_librarything()
	reviews = from_librarything + from_goodreads
	return reviews 

Book.get_online_user_reviews = get_online_user_reviews
```

*I siste linje bruker vi en teknikk i Python for å legge til en metode i en eksisterende klasse. Vi kan bruke følgende kodelinje for å gjøre dette:*
```py
MyClass.my_method = my_function
```
* *`MyClass` navnet på klassen*
* *`my_function` er navnet på funksjonen som vi har definert utenfor klassen*
* *`my_method` er navnet vi ønsker at funksjonen skal ha inni klassen*

Det neste vi ønsker oss er en funksjon som kan regne ut gjennomsnittet til en liste med anmeldelser:


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

    [['Handlingen var veldig spennende', 8], ['Boken var for lang', 5], ['En bok som får deg til å tenke', 7]]
    6.666666666666667


Les utskriften for å se at metoden regner ut riktig gjennomsnitt, og forsøk gjerne å forstå hvordan utregningen gjøres.

*I planleggingen av programmet plasserte vi denne funksjonen i klassen `Book`. Men her ser vi at funksjonen egentlig bare gjør en operasjon på en liste med tall, og vi har derfor valgt å plassere den utenfor klasseblokken.*


Nå er vi klare til å kode metoden som regner ut gjennomsnittsvurderingen til en bok! Funksjonen skal:

1. Hente anmeldelser fra tre forskjellige kilder; lånetakere, nettbrukere og kritikere.
2. Regne ut gjennomsnittsvurderingen for hver av disse kildene.
3. Regne ut et totalt gjennomsnitt.


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

Legg merke til hvordan de tre stegene blir til tre blokker med kode. I de to første blokkene gjøres alt arbeidet av delmetodene, mens det er det siste steget som er metodens "eget arbeid". I denne linjen kan vi endre hvor mye de ulike kildene skal vektes. Hvis vi for eksempel ønsker at vurderinger fra nettbrukere skal telle 50%, mens de andre kildene skal telle 25% hver, kan vi endre til følgende:

```py
total_score = 0.25*score_borrowers + 0.5*score_online_users + 0.25*score_critics
```

