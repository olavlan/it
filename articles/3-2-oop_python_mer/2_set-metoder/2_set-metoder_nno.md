---
title: "Set-metodar"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
---

Tidlegare har me nemnt at alle datafelt bør vera private. For kva er konsekvensane viss ein fritt kan endra på datafelt utanfor ein klasse? Sjå på følgjande døme:


```python
b4 = Book("Faen ta skjebnen", "John Green", 338)
my_review = ["Fantastisk bok!", "Terningkast 6"]
b4.borrower_reviews.append(my_review)
print(b4.borrower_reviews)
```

[['Ei bok som får deg til å tenkja', 7], ['Veldig interessant bok', 9], ['Slutten øydela boka', 2], ['Fantastisk bok!', 'Terningkast 6']]


Her har me lagt til ei melding som ikkje følgjer det rette formatet! Vurderinga skal nemleg skrivast som eit tal mellom 0 og 10. No får me ei feilmelding dersom me testar rangeringsmetoden frå førre seksjon:


```python
my_books = [b1, b2, b3, b4]
my_collection = BookCollection(my_books)
my_collection.show_ranked_list()
```


    ---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

Cell In[109], line 3
1 my_buoks = [b1, b2, b3, b4]
2 my_collection = BookCollection(my_buoks)
----> 3 my_collection.show_ranked_list()


Cell In[82], line 9, in BookCollection.show_ranked_list(self)
7 blir skåra_and_titles = []
8 for b in self.buoks:
----> 9     skåra_and_title = [b.calculate_average_skår(), b.title]
10     blir skåra_and_titles.append(skår_and_title)
12 blir skåra_and_titles = sorted(_skårs_and_titles, reverse=True)


Cell In[81], line 6, in calculate_average_skåra(self)
3 online_users = self.get_online_user_reviews()
4 critics = self.get_online_critics()
----> 6 skåra_borrowers = calculate_average(borrowers)
7 skåra_online_users = calculate_average(online_users)
8 skåra_critics = calculate_average(critics)


Cell In[80], line 6, in calculate_average(reviews)
4 for review in reviews:
5 	skåra = review[1]
----> 6 	total_skår += skår
7 average = total_skår/n
8 return average


TypeError: unsupported operand type(s) for +=: 'int' and 'str'


For å forhindra at datafelta blir endra på ein feil måte, bør me derfor gjera dei private:


```python
class Book:
    def __init__(self, title, author, number_of_pages):
        self._title = title
        self._author = author
        self._number_of_pages = number_of_pages
        self._borrower_reviews = get_random_reviews(3)
```

*For å forenkla presentasjonen har me skrive opp bokklassen på nytt, berre med konstruktøren. Namnet på datafelta må også oppdaterast alle andre stader dei blir brukte!*

Men korleis skal me tillata at brukarar gjer endringar på datafelta? Me ønskjer jo ofte at det skal vera mogleg! Løysinga er å definera ein offentleg metode som blir kalla ein *set*-metode (også kalla *set*, frå engelsk *to set*). Til dømes kan me laga ein *set*-metode som gjer det mogleg å endra tittelen til ei bok:


```python
class Book:
    def set_title(self, title):
        self._title = title
```

Dermed unngår me at brukaren av klassen har direkte tilgang til datafeltet `_title`. I staden gir me tilgang på ein måte som me kan kontrollera, nemleg gjennom metoden `set_title`. No kan me til dømes sjekka at parameteren er av rett datatype - me ønskjer nemleg at tittelen på ei bok skal vera ein streng:


```python
class Book: 
    def set_title(self, title):
        if type(title) == str:
            self._title = title
```

Tilsvarande kan me laga ein *set*-metode som gjer det mogleg å endra sidetalet til ei bok.


```python
class Book: 
    def set_number_of_pages(self, num):
        if type(num) == int and num > 0 and num < 10000:
            self._number_of_pages = num
```

Her ønskjer me at brukaren skriv eit positivt heiltal som ikkje er urimeleg høgt.

Til slutt kan me sjå på datafeltet `_borrower_reviews`. Dette er ei liste av meldingar, og me ønskjer eigentleg ikkje at brukaren skal kunna overskrive heile lista. Derfor gir det meir meining å laga ein metode for å leggja til ei melding i lista:


```python
class Book: 
    def add_borrower_review(self, text, score):
        if type(text) == str and type(score) == int and score >= 0 and num <= 10:
            review = [text, score]
            self._borrower_reviews.append(review)
```

Her sjekkar me både datatypane og at poengsummen er eit tal mellom 0 og 10. Dette løyser problemet me hadde i starten av seksjonen, nemleg at det vart lagt inn ei melding som var feil formatert. No har me sørgt for at alle meldingar som blir lagde inn har rett format!

