---
title: "Det objektorienterte paradigmet"
belongs_to_chain: "Når og hvorfor brukes objektorientert programmering?"
figures_to_include:
---

Når vi bruker programmering for matematiske beregninger, lager vi en slags utvidet kalkulator. Men: 

- En kalkulator er spesifikk - den gjør visse utregninger med tall. 
- En datamaskin er universell - den kan behandle alle typer data, og gjøre enhver operasjon som kan beskrives med en presis algoritme. 

Som programmerer møter man komplekse problemer som ikke nødvendigvis handler om tall og beregninger. Da må vi utnytte datamaskinens universelle natur, og ikke begrense oss til ett paradigme. Å alltid separere data og funksjoner kan være en slik begrensning. Med objektorientert programmering kan vi i stedet knytte sammen data og funksjoner som hører sammen. Vi skal vise når dette er nyttig gjennom et eksempel.

Se for deg at du koder et prosedyreorientert program for å skrive en hilsen til personer:

```py
def skriv_hilsen(navn):
    return "Hei, " + navn + "!" + " Takk for meldingen. Håper du har det bra! Hilsen meg."

person1_navn = "Geir"
person2_navn = "Kari"
skriv_hilsen(person1_navn)
skriv_hilsen(person2_navn)
```
Dersom vi ønsker en annen hilsen, trenger vi kun å endre koden i funksjonen. Det er en viktig styrke ved prosedyreorientert programmering. Men hva om vi ønsker å bruke mer data enn bare navnet? Kanskje vet vi når vi sist fikk melding fra hver person, og ønsker å bruke dette til å skrive en mer personlig hilsen:

```py
def skriv_hilsen(navn, dato_for_siste_melding):
    return "Hei, " + navn + "!" + " Takk for meldingen du sendte meg den " + dato_for_siste_melding + ". Håper du har det bra! Hilsen meg."

person1_navn = "Geir"
person2_navn = "Kari"
person1_dato_for_siste_melding = "2. februar"
person2_dato_for_siste_melding = "15. april"
skriv_hilsen(person1_navn, person1_dato_for_siste_melding)
skriv_hilsen(person2_navn, person2_dato_for_siste_melding)
```
Her måtte vi gjøre mange endringer, og koden har allerede blitt ganske stygg! Merk at vi må endre parameterlisten alle steder funksjonen kalles. Et større program kan ha veldig mange funksjonskall, og da blir slike endringer svært langtekkelig og repetitivt, noe vi nettopp vil unngå når vi programmerer. Så hvordan kunne vi gjort det på en bedre måte? Vi vet at funksjonen `skriv_hilsen`kun skal behandle én type data, nemlig data om personer. Det kan vi utnytte. 

Situasjonen er at vi har to datavariabler (`navn ` og `dato_for_siste_melding`) og én funksjon (`skriv_hilsen`) . Hva har disse til felles? De har med en person å gjøre! Med objektorientert programmering kan vi lage en "boks" som inneholder alt som handler om en person, både data og funksjoner. Det kalles en *klasse* (*class* på engelsk):

```py
class Person:
    navn = ""
    dato_for_siste_melding = ""

    def skriv_hilsen(self):
        return "Hei, " + self.navn + "!" + " Takk for meldingen du sendte meg den " + self.dato_for_siste_melding + ". Håper du har det bra! Hilsen meg."
```
Klassen `Person` definerer ikke en spesifikk person, men er en *mal* som forteller hva en person skal inneholde av data og funksjoner. Vi kan bruke denne malen til å definere en spesifikk person:

```py
person1 = Person()
person1.navn = "Geir" 
person1.dato_for_siste_melding = "2. februar"
```
Her oppretter vi et `Person`-objekt, som får en spesifikk plass i datamaskinens minne. Deretter setter vi data inn i objektet. Hvis du har brukt Python tidligere, så har du opprettet mange objekter, for i Python er nemlig alt objekter!  Når du skriver `mitt_tall=-4`, så opprettes egentlig et `int`-objekt, og verdien -4 settes inn i objektet. Deretter kan du gjøre `int`-operasjoner på objektet, for eksempel skrive `mitt_tall.abs()` for å finne absoluttverdien til tallet. På samme måte kan vi gjøre `Person`-operasjoner på `Person`-objektet vårt. Vi har foreløpig bare en slik operasjon:

```py
person1.skriv_hilsen()
```
Siden funksjonen brukes på et spesifikt `Person`-objekt, og objektet inneholder alle data om personen, trenger vi ingen parametre! Nå blir det enkelt å endre funksjonen. Kanskje ønsker vi å bruke bursdagen til hver person, for å gjøre meldingen enda mer personlig. Da endrer vi først `Person`-klassen, altså malen for personobjekter:

```py
class Person:
    fornavn = ""
    dato_for_siste_melding = ""
    bursdag = ""

    def skriv_hilsen(self):
        return "Hei, " + self.navn + "!" + " Takk for meldingen du sendte meg den " + self.dato_for_siste_melding + ". Håper du har det bra, og til lykke med dagen den " + self.bursdag + "!" + " Hilsen meg."
```
Vi oppretter nå et nytt `Person`-objekt fra denne klassen:

```py
person2 = Person()
person2.navn = "Kristine"
person2.dato_for_siste_melding = "1. mars"
person2.bursdag = "13. januar"
person2.skriv_hilsen()
```
Disse linjene er lett å lese, og trenger aldri å endres senere. Selv i et lite program ser vi altså nytteverdien av å koble sammen data og funksjoner. Denne koblingen oppnår vi ved hjelp av klasser og objekter, så her bruker vi objektorientert programmering! 

Det er viktig å kunne begrunne hvorfor man tar i bruk et bestemt paradigme:

* Hvorfor var det fornuftig å bruke det objektorienterte paradigmet i denne seksjonen? Fordi funksjonen `skriv_hilsen` kun brukes på spesifikk data, nemlig data om personer. 
* Hvorfor brukte vi det prosedyreorienterte paradigmet i den forrige seksjonen? Fordi `avstand` er en generell, matematisk funksjon, som kan brukes på data fra ulike kilder. 

*I eksemplene over setter vi data direkte inn i variablene til objektene. Senere skal vi se at variablene i et objekt bør være beskyttet, slik at man kun har tilgang til dem gjennom visse funksjoner.*


