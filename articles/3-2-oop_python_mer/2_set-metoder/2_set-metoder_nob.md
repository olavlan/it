---
title: "Set-metoder"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
---

Tidligere har vi nevnt at alle datafelter bør være private. For hva er konsekvensene hvis man fritt kan endre på datafelter utenfor en klasse? Se på følgende eksempel: 


```python
b4 = Book("Faen ta skjebnen", "John Green", 338)
my_review = ["Fantastisk bok!", "Terningkast 6"]
b4.borrower_reviews.append(my_review)
print(b4.borrower_reviews)
```

    [['En bok som får deg til å tenke', 7], ['Veldig interessant bok', 9], ['Slutten ødela boken', 2], ['Fantastisk bok!', 'Terningkast 6']]


Her har vi lagt til en anmeldelse som ikke følger det riktige formatet! Vurderingen skal nemlig skrives som et tall mellom 0 og 10. Nå får vi en feilmelding dersom vi tester rangeringsmetoden fra forrige seksjon:


```python
my_books = [b1, b2, b3, b4]
my_collection = BookCollection(my_books)
my_collection.show_ranked_list()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[109], line 3
          1 my_books = [b1, b2, b3, b4]
          2 my_collection = BookCollection(my_books)
    ----> 3 my_collection.show_ranked_list()


    Cell In[82], line 9, in BookCollection.show_ranked_list(self)
          7 scores_and_titles = []
          8 for b in self.books: 
    ----> 9     score_and_title = [b.calculate_average_score(), b.title]
         10     scores_and_titles.append(score_and_title)
         12 scores_and_titles = sorted(scores_and_titles, reverse=True)


    Cell In[81], line 6, in calculate_average_score(self)
          3 online_users = self.get_online_user_reviews()
          4 critics = self.get_online_critics()
    ----> 6 score_borrowers = calculate_average(borrowers)
          7 score_online_users = calculate_average(online_users)
          8 score_critics = calculate_average(critics)


    Cell In[80], line 6, in calculate_average(reviews)
          4 for review in reviews:
          5 	score = review[1]
    ----> 6 	total_score += score
          7 average = total_score/n
          8 return average


    TypeError: unsupported operand type(s) for +=: 'int' and 'str'


For å forhindre at datafeltene blir endret på en feil måte, bør vi derfor gjøre dem private: 


```python
class Book:
    def __init__(self, title, author, number_of_pages):
        self._title = title
        self._author = author
        self._number_of_pages = number_of_pages
        self._borrower_reviews = get_random_reviews(3)
```

*For å forenkle presentasjonen har vi skrevet opp bokklassen på nytt, kun med konstruktøren. Navnet på datafeltene må også oppdateres alle andre steder de brukes!*

Men hvordan skal vi tillate at brukere gjør endringer på datafeltene? Vi ønsker jo ofte at det skal være mulig! Løsningen er å definere en offentlig metode som kalles en *set*-metode (også kalt *setter*, fra engelsk *to set*). For eksempel kan vi lage en *set*-metode som gjør det mulig å endre tittelen til en bok:


```python
class Book:
    def set_title(self, title):
        self._title = title
```

Dermed unngår vi at brukeren av klassen har direkte tilgang til datafeltet `_title`. I stedet gir vi tilgang på en måte som vi kan kontrollere, nemlig gjennom metoden `set_title`. Nå kan vi for eksempel sjekke at parameteren er av riktig datatype - vi ønsker nemlig at tittelen på en bok skal være en streng: 


```python
class Book: 
    def set_title(self, title):
        if type(title) == str:
            self._title = title
```

Tilsvarende kan vi lage en *set*-metode som gjør det mulig å endre sideantallet til en bok.


```python
class Book: 
    def set_number_of_pages(self, num):
        if type(num) == int and num > 0 and num < 10000:
            self._number_of_pages = num
```

Her ønsker vi at brukeren skriver et positivt heltall som ikke er urimelig høyt.

Til slutt kan vi se på datafeltet `_borrower_reviews`. Dette er en liste av anmeldelser, og vi ønsker egentlig ikke at brukeren skal kunne overskrive hele listen. Derfor gir det mer mening å lage en metode for å legge til en anmeldelse i lista: 


```python
class Book: 
    def add_borrower_review(self, text, score):
        if type(text) == str and type(score) == int and score >= 0 and num <= 10:
            review = [text, score]
            self._borrower_reviews.append(review)
```

Her sjekker vi både datatypene og at poengsummen er et tall mellom 0 og 10. Dette løser problemet vi hadde i starten av seksjonen, nemlig at det ble lagt inn en anmeldelse som var feil formatert. Nå har vi sørget for at alle anmeldelser som blir lagt inn har riktig format!

