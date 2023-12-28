---
title: "Dokumentasjon av klasser"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok_offentlig.svg"
---

Tenk deg at du har programmert alle klassene i bokprogrammet, og ett år senere skal du lage en nettside for rangering av bøker. Du husker at du var fornøyd med  `Bok`-klassen, og vil bygge det nye programmet rundt denne klassen.

Du finner igjen`Bok`-klassen i en programfil kalt *Bok.py*, og kopierer denne fila over til den nye prosjektmappa. Hva nå? Du har selvfølgelig glemt all koden, og det vil ta deg en god stund å forstå den. Men for å ta i bruk en klasse trenger du ikke forstå koden, bare å forstå grensesnittet til klassen! Alt vi trenger å vite er hvordan vi skal bruke de offentlig metodene som er relevante for oss. Mer spesifikt bør vi vite: 

* *Signaturen* til metoden, det vil si navnet og parametrene til metoden
* En beskrivelse av handlingen som utføres av metoden
* En beskrivelse av hver parameter, altså hva slags verdier metoden forventer å motta
* En beskrivelse av returverdien

En slik beskrivelse av de offentlige metodene kalles en *dokumentasjon* av klassen. Når vi programmerer `Bok`-klassen, bør vi altså skrive en slik dokumentasjon, slik at det blir lett å gjenbruke klassen senere. 

Følgende klassediagram viser grensesnittet til klassen `Bok`: 

<img src="/media/markdowncontent/assosiated_files/klasse_bok_offentlig.svg" width="200">

Vi skal nå skrive en dokumentasjon for klassen, ved å følge punktene ovenfor. Merk at konstruktører alltid er offentlige metoder, og at de bør komme først i dokumentasjonen. Dette gir mening, for når vi skal ta i bruk en klasse, så er ofte det første vi vil gjøre å opprette objekter. 

**Dokumentasjon av `Bok`-klassen:**

#### `Bok(tittel, forfatter, antall_sider)`

> Oppretter et nytt `Bok`-objekt fra innskrevne verdier. 
> 
> **Parametre:**
> 
> * `tittel` (`str`): Den fulle tittelen på boka.
> * `forfatter` (`str`): Det fulle navnet til forfatteren, skrevet på formen "Fornavn Etternavn".
> * `antall_sider` (`int`): Antall sider i boka. 

#### `Bok(isbn)`

> Oppretter et nytt `Bok`-objekt fra ISBN. Informasjon om boka hentes ved å gjøre ISBN-søk i bokdatabaser på nett. Hvis denne informasjonen ikke blir funnet, opprettes et tomt `Bok`-objekt. 
> 
> **Parametre:**
> * isbn (str): Bokas ISBN. 

#### `lån_ut(person)`

> Registrerer utlån av boka hvis den er ledig. 
> 
> **Parametre:** 
> * `person` (`Person`): Personen som skal registreres som lånetaker. 
> **Returverdi (`bool`):** `True` dersom utlånet blir godkjent, `False` dersom boka ikke er ledig. 

#### `lever_inn()`

> Registrerer innlevering av boka hvis den er utlånt.
> 
> **Returverdi (`bool`):**  `True` dersom innleveringen blir godkjent, `False` dersom boka ikke kan leveres inn (fordi boka ikke er registrert som utlånt). 

#### `regn_ut_gjennomsnittsvurdering()`

> Returnerer en vurdering av boka, basert på anmeldelser fra følgende kilder: 
> 
> * Anmeldelser fra lånetakere
> * Brukeranmeldelser på nett
	> * *Bokelskere*
	> * *Goodreads*
> * Litteraturanmeldelser på nett
> 
> **Returverdi (`float`):** 
> * Dersom minst én anmeldelse blir funnet, returneres et gjennomsnittsverdi på en skala fra 0 til 10, der 10 er høyeste vurdering. 
> * Dersom ingen anmeldelser blir funnet, returneres -1.  

Nå har vi fullført dokumentasjonen. Vi gjentar at dokumentasjonen må inneholde følgende punkter for hver metode: 

1. Signaturen til metoden
2. Beskrivelse av hva metoden gjør
3. Parameterliste (dersom metoden har parametre)
4. Returverdi (dersom metoden har returverdi)
	
Merk også følgende detaljer:

* Når vi lister parametre og returverdi, skriver vi datatypen til disse i parentes. 

* En offentlig metode må alltid gi et resultat, og vi må beskrive alle de mulige returverdiene i dokumentasjonen. For eksempel har metoden`regn_ut_gjennomsnittsvurdering()`ett viktig spesialtilfelle, nemlig at ingen anmeldelser blir funnet, og da returneres -1. 

