---
title: "Kommunikasjon mellom objekt"
belongs_to_chain: "Mer om klasser og objekter i Python"
figures_to_include:
	- "python_interface.svg"
---

I førre seksjon programmerte me høgre side av følgjande diagram:

<img src="/media/markdowncontent/assosiated_files/python_interface.svg" width="1000">

På venstre side har me rangeringsmetoden, som ligg i klassen `BookCollection`. Denne metoden skal fungera ved å be alle bokobjekt om å rekna ut den gjennomsnittlege poengsummen sin. Då må metoden `calculate_average_score()` vera ein offentleg metode.

Korleis fortel me om ein metode skal vera offentleg eller privat? Det kjem an på kva programmeringsspråk me bruker! I Java blir til dømes brukte nøkkelorda `public` og `private`, og dersom ein metode er definert med `private`, er det berre mogleg å bruka han internt i klassen. Dersom me prøver å bruka ein privat metode utanfor klassen, får me ei feilmelding!

I Python er det ikkje mogleg å tvinga ein metode til å vera privat! Kva kan me gjera i staden? Tenk deg til dømes at nokon har lyst til å ta i bruk bokklassen vår i sitt eige program. Korleis kan me fortelja denne personen at det berre er `calculate_average_score()` som er offentleg, og at dei andre metodane ikkje bør brukast?

I Python har ein vorte samde om ein spesiell skrivemåte for å skilja mellom offentlege og private metodar:

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

*For å forenkla presentasjonen har me definert klassen på nytt, utan å ta med verken konstruktør eller koda i metodane.*

Ser du kva som er forskjellen på dei private metodane og den offentlege metoden?

For å markera at ein metode er privat, set me altså ein understrek i starten av namnet! Dette forhindrar ikkje nokon frå å bruka metoden, men det gir ein klar beskjed om at metoden kan endra seg eller slutta og fungera, og at det derfor ikkje er trygt å bruka han i sitt eige program!

No er me klare til å definera klassen `BookCollection`, som skal innehalda rangeringsmetoden:


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

**Blokk 1.** I den første blokka hentar me poengsummen og tittelen til kvart bokobjekt, og legg desse i lista `scores_and_titles`. Etter denne blokka kan me til dømes enda opp med følgjande liste:

```
[ [7.8, "Når villdyret våkner"],  [9.2, "Sofies verden"],  [8.9, "Beatles"] ]
```
Merk at kvart element i lista er ei ny liste, som inneheld poengsummen og tittelen til ei bok.

**Blokk 2.** I den andre blokka sorterer me denne lista. Viss me held fram med det same dømet får me følgjande liste:

```
[ [9.2, "Sofies verden"],  [8.9, "Beatles"],  [7.8, "Når villdyret våkner"] ]
```
*Merk at me bruker ein sorteringsfunksjon som er innebygd i Python. Det er viktig at poengsummen kjem først i dei indre listene, sidan det er desse elementa som blir brukte i sorteringa. Legg også merke til at me reverserer lista, fordi sorteringsfunksjonen som standard sorterer i stigande rekkjefølgje.*

3. I den siste linja skriv me ut den sorterte lista. Til dømes vil lista ovanfor bli skriven ut på følgjande måte:

```
9.2 Sofies verden
8.9 Beatles
7.8 Når villdyret våkner
```

Korleis kan me testa at metoden faktisk fungerer? La oss oppretta nokre bokobjekt som me kan testa med:


```python
b1 = Book("Sofies verden", "Jostein Gaarder", 512)
b2 = Book("Beatles", "Lars S. Christensen", 732)
b3 = Book("Når villdyret våkner", "Jack London", 86)
my_books = [b1, b2, b3]
```

Vidare kan me oppretta eit `BookCollection`-objekt og leggja bøkene i samlinga:


```python
my_collection = BookCollection(my_books)
```

No kan me testa rangeringsmetoden:


```python
my_collection.show_ranked_list()
```

6.6 Beatles
6.4 Når villdyret vaknar
5.5 Sofies verd


*Hugs at bokobjekta bruker eit tilfeldig utval av testmeldingane som me oppretta i førre seksjon!*

Som oppsummering kan me seia at boksamlingsobjektet ber kvart bokobjekt om å finna poengsummen sin, og deretter blir desse poenga brukte til å laga ei rangert liste. Kommunikasjonen mellom objekta skjer gjennom den offentlege metoden `calculate_average_score`.

