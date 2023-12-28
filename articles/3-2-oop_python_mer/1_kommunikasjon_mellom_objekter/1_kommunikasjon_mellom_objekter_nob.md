---
title: "Kommunikasjon mellom objekter"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
	- "python_interface.svg"
---

I forrige seksjon programmerte vi høyre side av følgende diagram: 

<img src="/media/markdowncontent/assosiated_files/python_interface.svg" width="1000">

På venstre side har vi rangeringsmetoden, som ligger i klassen `BookCollection`. Denne metoden skal fungere ved å be alle bokobjekter om å regne ut sin gjennomsnittlige poengsum. Da må metoden `calculate_average_score()` være en offentlig metode. 

Hvordan forteller vi om en metode skal være offentlig eller privat? Det kommer an på hvilket programmeringsspråk vi bruker! I Java brukes for eksempel nøkkelordene `public` og `private`, og dersom en metode er definert med `private`, er det kun mulig å bruke den innad i klassen. Dersom vi prøver å bruke en privat metode utenfor klassen, får vi en feilmelding!

I Python er det ikke mulig å tvinge en metode til å være privat! Hva kan vi gjøre i stedet? Tenk deg for eksempel at noen har lyst til å ta i bruk bokklassen vår i sitt eget program. Hvordan kan vi fortelle denne personen at det kun er `calculate_average_score()` som er offentlig, og at de andre metodene ikke bør brukes? 

I Python har man blitt enige om en spesiell skrivemåte for å skille mellom offentlige og private metoder:

```python
class Book: 
    def _get_reviews_from_goodreads(self):
    	return

    def _get_reviews_from_librarything(self):
    	return

    def _get_online_critics(self):
    	return

    def calculate_average_score(self):
        return
```

*For å forenkle presentasjonen har vi definert klassen på nytt, uten å ta med verken konstruktør eller kode i metodene.*

Ser du hva som er forskjellen på de private metodene og den offentlige metoden? 

For å markere at en metode er privat, setter vi altså en understrek i starten av navnet! Dette forhindrer ikke noen fra å bruke metoden, men det gir en klar beskjed om at metoden kan endre seg eller slutte og fungere, og at det derfor ikke er trygt å bruke den i sitt eget program!

Nå er vi klare til å definere klassen `BookCollection`, som skal inneholde rangeringsmetoden:


```python
class BookCollection: 
    def __init__(self, books):
        self.books = books

    def show_ranked_list(self):
        
        scores_and_titles = []
        for b in self.books: 
            score_and_title = [b.calculate_average_score(), b.title]
            scores_and_titles.append(score_and_title)
        
        scores_and_titles = sorted(scores_and_titles, reverse=True)

        for s, t in scores_and_titles:
            print(round(s, 1), t)
```

Rangeringsmetoden har fire blokker med kode: 

**Blokk 1.** I den første blokken henter vi poengsummen og tittelen til hvert bokobjekt, og legger disse i listen `scores_and_titles`. Etter denne blokken kan vi for eksempel ende opp med følgende liste:

```
[ [7.8, "Når villdyret våkner"],  [9.2, "Sofies verden"],  [8.9, "Beatles"] ]
```
Merk at hvert element i listen er en ny liste, som inneholder poengsummen og tittelen til en bok. 

**Blokk 2.** I den andre blokken sorterer vi denne listen. Hvis vi fortsetter med det samme eksempelet får vi følgende liste:

```
[ [9.2, "Sofies verden"],  [8.9, "Beatles"],  [7.8, "Når villdyret våkner"] ]
```
*Merk at vi bruker en sorteringsfunksjon som er innebygd i Python. Det er viktig at poengsummen kommer først i de indre listene, siden det er disse elementene som brukes i sorteringen. Legg også merke til at vi reverserer listen, fordi sorteringsfunksjonen som standard sorterer i stigende rekkefølge.*

3. I den siste linjen printer vi den sorterte listen. For eksempel vil listen ovenfor bli printet på følgende måte:

```
9.2 Sofies verden
8.9 Beatles
7.8 Når villdyret våkner
```

Hvordan kan vi teste at metoden faktisk fungerer? La oss opprette noen bokobjekter som vi kan teste med:


```python
b1 = Book("Sofies verden", "Jostein Gaarder", 512)
b2 = Book("Beatles", "Lars S. Christensen", 732)
b3 = Book("Når villdyret våkner", "Jack London", 86)
my_books = [b1, b2, b3]
```

Videre kan vi opprette et `BookCollection`-objekt og legge bøkene i samlingen: 


```python
my_collection = BookCollection(my_books)
```

Nå kan vi teste rangeringsmetoden:


```python
my_collection.show_ranked_list()
```

    6.6 Beatles
    6.4 Når villdyret våkner
    5.5 Sofies verden


*Husk at bokobjektene bruker et tilfeldig utvalg av testanmeldelsene som vi opprettet i forrige seksjon!*

Som oppsummering kan vi si at boksamlingobjektet ber hvert bokobjekt om å finne sin poengsum, og deretter brukes disse poengene til å lage en rangert liste. Kommunikasjonen mellom objektene skjer gjennom den offentlige metoden `calculate_average_score`. 

