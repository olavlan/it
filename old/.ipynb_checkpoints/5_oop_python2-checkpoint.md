## Delmetoder

I boksystemet vårt ønsket vi å kunne vise en rangert liste av bøker. Følgende klassediagram viser metodene vi trenger for å oppnå dette:

<img src="../fig/python_book_public_private.svg" width="">

Følgende figur viser hvordan noen metoder brukes som byggeblokker til andre metoder:

<img src="../fig/python_interface.svg" width="1000">

De minste byggeblokkene er metodene som henter anmeldelser fra ulike kilder. Metoden `calculate_average` kan deretter bruke disse anmeldelsene til å regne ut en gjennomsnittsvurdering for en bok. Til slutt kan metoden `show_ranked_list` hente vurderingen til hver bok i samlingen, og til slutt bruke disse tallene til å rangere bøkene. 

Figuren over viser kommunikasjon innad i et objekt (røde piler) og kommunikasjon mellom objekter (grønn pil). I denne seksjonen skal vi se hvordan vi koder dette. 

Ofte er det de minste byggeblokkene som inneholder den meste koden. I vårt eksempel så er de minste byggeblokkene metoder som henter anmeldelser fra diverse nettsider. Siden vi ikke er interessert i å vise slik programmering i dette kurset, skal vi opprette noen anmeldelser som kan brukes til testing: 


```py
from random import sample

r1 = ["Very interesting book", 9]
r2 = ["The book was too long", 5]
r3 = ["The ending ruined the book", 2]
r4 = ["A book that makes you think", 7]
r5 = ["The story is very exciting", 8]

all_reviews = [r1, r2, r3, r4, r5]

def get_random_reviews(n):
	return sample(all_reviews, n)

print(get_random_reviews(3))
```

```
[['The story is very exciting', 8], ['A book that makes you think', 7], ['The book was too long', 5]]
```

Funksjonen `get_random_reviews` henter et tilfeldig utvalg av de fem testanmeldelsene vi har skrevet. 

Nå kan vi begynne med de minste byggeblokkene, som skal være i klassen `Book`:

```py
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

 Merk at konstruktøren oppretter datafeltet `borrower_reviews` og fyller denne med tilfeldige anmeldelser. Nå kan vi late som vi har anmeldelser fra fire forskjellige kilder; lånetakere, brukeranmeldelser fra *Goodreads* og *Librarything*, og kritikker på nett. 

Det neste vi ønsker er en metode som samler alle brukeranmeldelser på nett. Dette blir enkelt når vi har byggeblokkene.  

```py
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

Tenk deg nå at du ønsker å inkludere brukeranmeldelser fra en tredje nettside? Hvordan vil du gjøre denne endringen? 

Det neste vi ønsker oss er en funksjon som kan regne ut gjennomsnittet til en liste med anmeldelser.

```py
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

```
[['The story is very exciting', 8], ['The book was too long', 5], ['A book that makes you think', 7]]
6.666666666666667
```

Forsøk gjerne å forstå hvordan metoden regner ut gjennomsnittet av anmeldelsene. I de siste kodelinjene gjør vi en test for å sjekke at utregningen er riktig. Tallene 8, 5 og 7 har gjennomsnittet 6.66, så metoden fungerer. 

*I planleggingen av programmet plasserte vi denne funksjonen i klassen `Book`. Men vi bør merke oss at den egentlig ikke gjør noen operasjoner på et bokobjekt; derfor har vi heller ingen `self`-parameter. Funksjonen gjør egentlig bare en operasjon på en liste med tall.*

*Vi kan godt legge til funksjonen i klassen, og argumentere for at det er en hjelperfunksjon som vi bare trenger i *Bok*-klassen. Men dersom vi tenker at funksjonen kan være nyttig andre steder, bør vi la den være utenfor klassen. Det som er viktig at klassen `Book` har tilgang til funksjonen, for eksempel ved at funksjonen og klassen er definert i samme programfil. Dersom funksjonen er definert i en annen programfil, må vi importere den før vi kan bruke den i klassen.*

Nå er vi klare til å kode metoden som regner ut gjennomsnittsvurderingen til en bok! Funksjonen skal:

1. Hente anmeldelser fra tre forskjellige kilder; lånetakere, nettbrukere og kritikere
2. Regne ut gjennomsnittsvurderingen for hver av disse kildene
3. Regne ut et totalt gjennomsnitt

```py
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

Legg merke til hvordan de tre stegene blir til tre blokker med kode. I de to første blokkene gjøres alt arbeidet av delmetodene, og det er bare utregningen av `total_score` som er metodens "eget arbeid". I denne linjen kan vi endre hvor mye de ulike kildene skal vektes. Hvis vi for eksempel ønsker at nettbrukere skal telle 50%, mens de andre kildene skal telle 25% hver, kan vi endre til følgende:

```py
total_score = 0.25*score_borrowers + 0.5*score_online_users + 0.25*score_critics
```

Metoden `calculate_average_score` ville blitt lang og komplisert dersom vi hadde skrevet all kode her. Ved å bruke delmetoder som hver har sin oppgave, blir metoden i stedet lettlest og forståelig!

## Offentlige og private metoder

I forrige seksjon programmerte vi høyre side av følgende diagram: 

<img src="../fig/python_interface.svg" width="1000">

Har nesten rangeringsfunksjon. Plassering til rangeringsfunksjon. Trenger å kommunisere med alle bokobjekter. Spesifikt trengs poengsummen. Hvordan gjøres offentlig? 

Python har ikke offentlige metoder! Programmerere bruker en spesiell skrivemåte for å fortelle hverandre hvilke metoder som skal brukes. Tenk deg at Bok-klassen din har blitt så bra at mange vil bruke den i sine egen programmer, og at du til og med gir ut nye versjoner. 

Hva er det brukerne ønsker å gjøre? De ønsker å opprette Bok-objekter og bruke funksjonaliteten som følger med slike objekter. En slik funksjonalitet er å regne ut gjennomsnitt. Ved å ta i bruk denne metoden oppretter brukerne en kommunikasjonslinje mellom bokobjekter og objekter som de har i sitt eget program. Dersom du gir ut en versjon der metoden slutter å fungere som forventet, vil denne kommunikasjonen brytes, og brukerne blir sure!

Siden du har bestemt deg for at viktig funksjonalitet, så vil du fortelle brukerne at denne vil fungere i alle framtidige versjoner av klassen. Men du ønsker ikke å forplikte deg til at delmetodene alltid fungerer. For eksempel kan det tenkes at du en dag vil slette Goodreads, fordi det ble for vanskelig å hente anmeldelser etter at nettsiden ble oppdatert. Hvordan skal du formidle at delmetodene IKKE bør brukes? 

I Python gjør vi dette med understreker! 

Private datafelter, getters og setters

## Dokumentasjon

For at det skal bli enda lettere for brukerne av Book å se hvilke funksjoner som er offentlige og hvordan de brukes. Da kan vi skrive en dokumentasjon. Denne kan skrives direkte i koden. 


## Kommunikasjon mellom objekter

Når vi skal programmere klassen BookCollection, kan vi godt tenke oss at vi er en annen person som ønsker å ta i bruk Book i vårt eget program. Vi ser i dokumentasjonen at klassen har den offentlige metoden , og ønsker å bruke denne til å rangere bøker.


## Oppdeling av klasser

## Arv

## Oppsummering og oppgaver




