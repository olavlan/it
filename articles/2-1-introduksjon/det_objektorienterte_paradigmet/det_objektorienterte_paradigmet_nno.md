---
title: "Det objektorienterte paradigmet"
belongs_to_chain: "Når og hvorfor brukes objektorientert programmering?"
figures_to_include:
---

Når me bruker programmering for matematiske berekningar, lagar me ein slags utvida kalkulator. Men:

- Ein kalkulator er spesifikk - han gjer visse utrekningar med tal.
- Ei datamaskin er universell - ho kan behandla alle typar data, og gjera alle operasjonar som kan beskrivast med ein presis algoritme.

Som programmerer møter ein komplekse problem som ikkje nødvendigvis handlar om tal og berekningar. Då må me utnytta den universelle naturen til datamaskina, og ikkje avgrensa oss til eitt paradigme. Å alltid separera data og funksjonar kan vera ei slik avgrensing. Med objektorientert programmering kan me i staden knyta saman data og funksjonar som høyrer saman. Me skal visa når dette er nyttig gjennom eit døme.

Sjå for deg at du kodar eit prosedyreorientert program for å skriva ei helsing til personar:

```py
def skriv_hilsen(navn):
    return "Hei, " + navn + "!" + " Takk for meldingen. Håper du har det bra! Hilsen meg."

person1_navn = "Geir"
person2_navn = "Kari"
skriv_hilsen(person1_navn)
skriv_hilsen(person2_navn)
```
Dersom me ønskjer ei anna helsing, treng me berre å endra koden i funksjonen. Det er ein viktig styrke ved prosedyreorientert programmering. Men kva om me ønskjer å bruka meir data enn berre namnet? Kanskje veit me når me sist fekk melding frå kvar person, og ønskjer å bruka dette til å skriva ei meir personleg helsing:

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
Her måtte me gjera mange endringar, og koden har allereie vorte ganske stygg! Merk at me må endra parameterslista alle stader funksjonen blir kalla. Eit større program kan ha veldig mange funksjonskall, og då blir slike endringar svært langtekkjeleg og repetitivt, noko me nettopp vil unngå når me programmerer. Så korleis kunne me gjort det på ein betre måte? Me veit at funksjonen `skriv_hilsen`berre skal behandla éin type data, nemleg data om personar. Det kan me utnytta.

Situasjonen er at me har to datavariablar (`navn ` og `dato_for_siste_melding`) og éin funksjon (`skriv_hilsen`) . Kva har desse til felles? Dei har med ein person å gjera! Med objektorientert programmering kan me laga ein "boks" som inneheld alt som handlar om ein person, både data og funksjonar. Det blir kalla ein *klasse* (*class* på engelsk):

```py
class Person:
    navn = ""
    dato_for_siste_melding = ""

    def skriv_hilsen(self):
        return "Hei, " + self.navn + "!" + " Takk for meldingen du sendte meg den " + self.dato_for_siste_melding + ". Håper du har det bra! Hilsen meg."
```
Klassen `Person` definerer ikkje ein spesifikk person, men er ein *mal* som fortel kva ein person skal innehalda av data og funksjonar. Me kan bruka denne malen til å definera ein spesifikk person:

```py
person1 = Person()
person1.navn = "Geir" 
person1.dato_for_siste_melding = "2. februar"
```
Her opprettar me eit `Person`-objekt, som får ein spesifikk plass i minnet til datamaskina. Deretter set me data inn i objektet. Viss du har brukt Python tidlegare, så har du oppretta mange objekt, for i Python er nemleg alt objekt!  Når du skriv `mitt_tall=-4`, så blir oppretta eigentleg eit `int`-objekt, og verdien -4 blir sette inn i objektet. Deretter kan du gjera `int`-operasjonar på objektet, til dømes skriva `mitt_tall.abs()` for å finna absoluttverdien til talet. På same måte kan me gjera `Person`-operasjonar på `Person`-objektet vårt. Me har førebels berre ein slik operasjon:

```py
person1.skriv_hilsen()
```
Sidan funksjonen blir brukt på eit spesifikt `Person`-objekt, og objektet inneheld alle data om personen, treng me ingen parametrar! No blir det enkelt å endra funksjonen. Kanskje ønskjer me å bruka bursdagen til kvar person, for å gjera meldinga endå meir personleg. Då endrar me først `Person`-klassen, altså malen for personobjekt:

```py
class Person:
    fornavn = ""
    dato_for_siste_melding = ""
    bursdag = ""

    def skriv_hilsen(self):
        return "Hei, " + self.navn + "!" + " Takk for meldingen du sendte meg den " + self.dato_for_siste_melding + ". Håper du har det bra, og til lykke med dagen den " + self.bursdag + "!" + " Hilsen meg."
```
Me opprettar no eit nytt `Person`-objekt frå denne klassen:

```py
person2 = Person()
person2.navn = "Kristine"
person2.dato_for_siste_melding = "1. mars"
person2.bursdag = "13. januar"
person2.skriv_hilsen()
```
Desse linjene er lett å lesa, og treng aldri å endrast seinare. Sjølv i eit lite program ser me altså nytteverdien av å kopla saman data og funksjonar. Denne koplinga oppnår me ved hjelp av klassar og objekt, så her bruker me objektorientert programmering!

Det er viktig å kunna grunngi kvifor ein tek i bruk eit bestemt paradigme:

* Kvifor var det fornuftig å bruka det objektorienterte paradigmet i denne seksjonen? Fordi funksjonen `skriv_hilsen` berre blir brukt på spesifikk data, nemleg data om personar.
* Kvifor brukte me det prosedyreorienterte paradigmet i den førre seksjonen? Fordi `avstand` er ein generell, matematisk funksjon, som kan brukast på data frå ulike kjelder.

*I døma over set me data direkte inn i variablane til objekta. Seinare skal me sjå at variablane i eit objekt bør vera verna, slik at ein berre har tilgang til dei gjennom visse funksjonar.*


