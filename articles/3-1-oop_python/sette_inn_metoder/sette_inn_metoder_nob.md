---
title: "Sette inn metoder"
belongs_to_chain: "Klasser og objekter i Python"
figures_to_include:
---

I forrige seksjon programmerte vi klassen `Book` og opprettet et objekt fra klassen. Men vi definerte kun datafelter i klassen, så nå lurer du kanskje på hvordan vi definerer metoder? La oss først definere en vanlig funksjon utenfor klassen `Book`:


```python
def print_information(book):
        print(book.title, " has ", book.number_of_pages, " pages.")

print_information(book1)
```

    Sofies verden  has  512  pages.


Denne funksjonen tar et bokobjekt som parameter, og printer ut en setning om boka. Å definere vanlige funksjoner kan ofte være et fint sted å starte. Vi kan nå legge merke til at funksjonen kun brukes på én type data, nemlig data om en bok. Dette er et hint om at vi bør bruke objektorientert programmering, slik at vi kan knytte sammen data og funksjoner som hører sammen. Hvordan knytter vi funksjonen `print_information()` til data om en bok? Svaret er selvfølgelig at funksjonen bør legges i klassen `Book`! Hvordan gjør vi så dette? Kan vi bare kopiere funksjonen inn i klasseblokken? La oss prøve!


```python
class Book:
    title = ""
    author = ""
    number_of_pages = 0
    
    def print_information(book):
        print(book.title, " has ", book.number_of_pages, " pages.")
```

Nå kan vi opprette et nytt bokobjekt og be objektet om å utføre metoden:


```python
book3 = Book()
book3.title = "Når villdyret våkner"
book3.number_of_pages = 86
book3.print_information()
```

    Når villdyret våkner  has  86  pages.


Dette fungerte! Nå har vi to funksjoner som gjør det samme; den ene er definert inni klassen og den andre utenfor. Metodene har til og med helt lik kode! Forskjellen er måten de brukes på:


```python
print_information(book3)
book3.print_information()
```

    Når villdyret våkner  has  86  pages.
    Når villdyret våkner  has  86  pages.


Forklaring:

1. I funksjonen som er definert utenfor klassen må vi sette inn bokobjektet som parameter. 
2. I metoden som er definert i klassen, trenger vi ingen parametre - vi må i stedet "gå inn" på riktig objekt og deretter be objektet om å utføre metoden. Vi gjør dette ved å bruke punktum, som forklart i forrige seksjon.  Men hva er det som skjer bak kulissene når vi skriver `book3.print_information()`? Svaret er faktisk ganske enkelt; Python setter automatisk inn `book3` som den første parameteren! 

Når vi bruker metoder er det altså objektet selv som settes inn i den første parameteren. Her er et annet eksempel: 

- Tenk deg at vi definerer en ny metode i klassen `Book`, som har signaturen `my_method(p1, p2, p3)`. 
- Denne metoden må utføres av et spesifikt bokobjekt, for eksempel med kommandoen `book1.my_method(1, 2)`.  Her ser det ut som vi bare har gitt to parametre, men egentlig har vi gitt tre; den første parameteren blir `book1`, mens den andre og tredje parameteren blir tallene `1` og `2`.

Når vi definerer metoder er det vanlig å gi den første parameteren navnet `self`, siden det alltid er "objektet selv" som settes inn i denne parameteren. Derfor kunne vi i stedet brukt signaturen `my_method(self, p2, p3)` i eksemplet over. I vårt første eksempel kan vi gjøre tilsvarende endring:


```python
class Book:
    title = ""
    author = ""
    number_of_pages = 0
    
    def print_information(self):
        print("This book has " + self.number_of_pages + " pages")
```

Legg merke til siste linje; metoden må vite hvilket objekt datafeltet `number_of_pages` kommer fra. Vanligvis ønsker vi å bruke objektet som kalte på metoden, som vi kan hente med `self`-parameteren. Da må vi skrive `self.number_of_pages`. 

Når vi programmerer i Python, bør vi ha som vane å inkludere `self`-parameteren når vi oppretter nye metoder:


```python
class Book:
    title = ""
    author = ""
    number_of_pages = 0
    
    def register_loan(self, person):
        return False

    def register_delivery(self):
        return False
```

*Foreløpig gjør disse metodene ingenting, men det er ofte lurt å definere alle klasser og metoder først, og senere fylle dem med funksjonell kode.*


