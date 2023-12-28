---
title: "Dokumentasjon av klassar"
belongs_to_chain: "Mer om objekter og klasser"
figures_to_include:
	- "klasse_bok_offentlig.svg"
---

Tenk deg at du har programmert alle klassane i bokprogrammet, og eitt år seinare skal du laga ei nettside for rangering av bøker. Du hugsar at du var fornøgd med  `Bok`-klassen, og vil byggja det nye programmet rundt denne klassen.

Du finn igjen`Bok`-klassen i ei programfil kalla *bok.py*, og kopierer denne fila over til den nye prosjektmappa. Kva no? Du har sjølvsagt gløymt all koden, og det vil ta deg ei god stund å forstå ho. Men for å ta i bruk ein klasse treng du ikkje forstå koden, berre å forstå grensesnittet til klassen! Alt me treng å vita er korleis me skal bruka dei offentleg metodane som er relevante for oss. Meir spesifikt bør me vita:

* *Signaturen* til metoden, det vil seia namnet og parametrane til metoden
* Ei skildring av handlinga som blir utført av metoden
* Ei skildring av kvar parameter, altså kva slags verdiar metoden forventar å få
* Ei skildring av returverdien

Ei slik skildring av dei offentlege metodane blir kalla ein *dokumentasjon* av klassen. Når me programmerer `Bok`-klassen, bør me altså skriva ein slik dokumentasjon, slik at det blir lett å gjenbruka klassen seinare.

Følgjande klassediagram viser grensesnittet til klassen `Bok`:

<img src="/media/markdowncontent/assosiated_files/klasse_bok_offentlig.svg" width="200">

Me skal no skriva ein dokumentasjon for klassen, ved å følgja punkta ovanfor. Merk at konstruktørar alltid er offentlege metodar, og at dei bør komma først i dokumentasjonen. Dette gir meining, for når me skal ta i bruk ein klasse, så er ofte det første me vil gjera å oppretta objekt.

**Dokumentasjon av `Bok`-klassen:**

#### `Bok(tittel, forfatter, antall_sider)`

> Opprettar eit nytt `Bok`-objekt frå innskrivne verdiar.
> 
> **Parametrar:**
> 
> * `tittel` (`str`): Den fulle tittelen på boka.
> * `forfatter` (`str`): Det fulle namnet til forfattaren, skrive på forma "Fornavn Etternavn".
> * `antall_sider` (`int`): Talet på sider i boka.

#### `Bok(isbn)`

> Opprettar eit nytt `Bok`-objekt frå ISBN. Informasjon om boka blir henta ved å gjera ISBN-søk i bokdatabasar på nett. Viss denne informasjonen ikkje blir funnen, blir oppretta eit tomt `Bok`-objekt.
> 
> **Parametrar:**
> * isbn (str): Bokas ISBN.

#### `lån_ut(person)`

> Registrerer utlån av boka viss ho er ledig.
> 
> **Parametrar:**
> * `person` (`Person`): Personen som skal registrerast som lånetakar.
> **Returverdi (`bool`):** `True` dersom utlånet blir godkjent, `False` dersom boka ikkje er ledig.

#### `lever_inn()`

> Registrerer innlevering av boka viss ho er utlånt.
> 
> **Returverdi (`bool`):**  `True` dersom innleveringa blir godkjend, `False` dersom boka ikkje kan leverast inn (fordi boka ikkje er registrert som utlånt).

#### `regn_ut_gjennomsnittsvurdering()`

> Returnerer ei vurdering av boka, basert på meldingar frå følgjande kjelder:
> 
> * Meldingar frå lånetakarar
> * Brukarmeldingar på nett
	> * *Bokelskarar*
	> * *Goodreads*
> * Litteraturmeldingar på nett
> 
> **Returverdi (`float`):**
> * Dersom minst éi melding blir funnen, blir eit gjennomsnittsverdi returnert på ein skala frå 0 til 10, der 10 er høgaste vurdering.
> * Dersom ingen meldingar blir funne, blir returnerte -1

No har me fullført dokumentasjonen. Me gjentek at dokumentasjonen må innehalda følgjande punkt for kvar metode:

1. Signaturen til metoden
2. Skildring av kva metoden gjer
3. Parametersliste (dersom metoden har parametrar)
4. Returverdi (dersom metoden har returverdi)
	
Merk også følgjande detaljar:

* Når me listar parametrar og returverdi, skriv me datatypen til desse i parentes.

* Ein offentleg metode må alltid gi eit resultat, og me må beskriva alle dei moglege returverdiane i dokumentasjonen. Til dømes har metoden`regn_ut_gjennomsnittsvurdering()`eitt viktig spesialtilfelle, nemleg at ingen meldingar blir funne, og då blir returnerte -1

