---
title: "Setja inn metodar"
belongs_to_chain: "Klasser og objekter i Python"
figures_to_include:
---

I førre seksjon programmerte me klassen `Book` og oppretta eit objekt frå klassen. Men me definerte berre datafelt i klassen, så no lurer du kanskje på korleis me definerer metodar? La oss først definera ein vanleg funksjon utanfor klassen `Book`:


```python
def print_information(book):
        print(book.title, " has ", book.number_of_pages, " pages.")

print_information(book1)
```

Sofies verd  blir hatt  512  pages.


Denne funksjonen tek eit bokobjekt som parameter, og skriv ut ei setning om boka. Å definera vanlege funksjonar kan ofte vera ein fin stad å starta. Me kan no leggja merke til at funksjonen berre blir brukt på éin type data, nemleg data om ei bok. Dette er eit hint om at me bør bruka objektorientert programmering, slik at me kan knyta saman data og funksjonar som høyrer saman. Korleis knyter me funksjonen `print_information()` til data om ei bok? Svaret er sjølvsagt at funksjonen bør leggjast i klassen `Book`! Korleis gjer me så dette? Kan me berre kopiera funksjonen inn i klasseblokka? La oss prøva!


```python
class Book:
    title = ""
    author = ""
    number_of_pages = 0
    
    def print_information(book):
        print(book.title, " has ", book.number_of_pages, " pages.")
```

No kan me oppretta eit nytt bokobjekt og be objektet om å utføra metoden:


```python
book3 = Book()
book3.title = "Når villdyret våkner"
book3.number_of_pages = 86
book3.print_information()
```

Når villdyret vaknar  has  86  pages.


Dette fungerte! No har me to funksjonar som gjer det same; den eine er definert inni klassen og den andre utanfor. Metodane har til og med heilt lik kode! Forskjellen er måten dei blir brukte på:


```python
print_information(book3)
book3.print_information()
```

Når villdyret vaknar  has  86  pages.
Når villdyret vaknar  has  86  pages.


Forklaring:

1. I funksjonen som er definert utanfor klassen må me setja inn bokobjektet som parameter.
2. I metoden som er definert i klassen, treng me ingen parametrar - me må i staden "gå inn" på rett objekt og deretter be objektet om å utføra metoden. Me gjer dette ved å bruka punktum, som forklart i førre seksjon.  Men kva er det som skjer bak kulissane når me skriv `book3.print_information()`? Svaret er faktisk ganske enkelt; Python set automatisk inn `book3` som den første parameteren!

Når me bruker metodar er det altså objektet sjølv som blir sett inn i den første parameteren. Her er eit anna døme:

- Tenk deg at me definerer ein ny metode i klassen `Book`, som har signaturen `my_method(p1, p2, p3)`.
- Denne metoden må utførast av eit spesifikt bokobjekt, til dømes med kommandoen `book1.my_method(1, 2)`.  Her ser det ut som me berre har gitt to parametrar, men eigentleg har me gitt tre; den første parameteren blir `book1`, medan den andre og tredje parameteren blir tala `1` og `2`.

Når me definerer metodar er det vanleg å gi den første parameteren namnet `self`, sidan det alltid er "objektet sjølv" som blir sett inn i denne parameteren. Derfor kunne me i staden brukt signaturen `my_method(self, p2, p3)` i dømet over. I vårt første døme kan me gjera tilsvarande endring:


```python
class Book:
    title = ""
    author = ""
    number_of_pages = 0
    
    def print_information(self):
        print("This book has " + self.number_of_pages + " pages")
```

Legg merke til siste linje; metoden må vita noko som objekt datafeltet `number_of_pages` kjem frå. Vanlegvis ønskjer me å bruka objektet som kalla på metoden, som me kan henta med `self`-parameteren. Då må me skriva `self.number_of_pages`.

Når me programmerer i Python, bør me ha som vane å inkludera `self`-parameteren når me opprettar nye metodar:


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

*Førebels gjer desse metodane ingenting, men det er ofte lurt å definera alle klassar og metodar først, og seinare fylla dei med funksjonell kode.*


