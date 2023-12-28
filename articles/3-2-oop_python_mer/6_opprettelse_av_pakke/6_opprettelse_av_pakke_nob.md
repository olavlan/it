---
title: "Opprettelse av pakke"
figures_to_include:
	- "pythonimport.svg"
---

Fram til nå har vi definert alle klasser i én Python-fil, men det kan være lurt å organisere prosjektet bedre. Kort sagt bør vi ha én fil per klasse. Hvis vi har et klassediagram som består av klassene `Loanable`, `Book`, og `BookCollection`, kan vi opprette følgende mappestruktur:
```
└── Desktop
    └── personal-library-tool
        ├── __init__.py
        ├── Loanable.py
        ├── Book.py  
        ├── BookCollection.py
```

Vi har opprettet mappen `personal-library-tool/`, der vi finner én fil for hver klasse, samt den spesielle filen `__init__.py`. Denne filen er for å fortelle Python at `personal-library-tool` er en pakke! 

Nå er vi klare for å teste programmet vårt i kommandolinjen (for å åpne kommandolinjen, kan du bruke programmet `Terminal` på Mac og Linux, eller `cmd.exe` på Windows). Vi må først navigere oss inn på mappen der vi har lagt `personal-library-tool/` (i eksempelet ovenfor er det altså `Desktop/` vi skal navigere oss inn på). 

```bash
~$ cd Desktop
```

Vi bruker nå kommandoen `python3` til å starte *Python-tolkeren*, som gjør at vi kan kjøre Python-kode direkte i kommandolinjen:

```bash
~/Desktop$ python3
Python 3.8.10 (default, May 26 2023, 14:05:08) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
Det første vi må gjøre er å importere pakken vår:

```python
>>> import personal-library-tool
```
Hvordan tar vi i bruk bokklassen til å opprette et bokobjekt? Først må vi gå inn på riktig *modul*. Hver Python-fil blir til en modul, så pakken vår består av tre moduler: 

* `personal-library-tool.Loanable`
* `personal-library-tool.Book`
* `personal-library-tool.BookCollection`

For å opprette et bokobjekt, må vi gå inn på den andre modulen, og deretter bruke klassen som ligger i modulen:

```python
>>> my_book = personal-library-tool.Book.Book()
```

Følgende diagram viser hva de ulike delene betyr:

<img src="/media/markdowncontent/assosiated_files/pythonimport.svg">

For å slippe å skrive det lange pakkenavnet hele tiden, kan vi importere modulene direkte:

```python
>>> from personal-library-tool import Loanable, Book, BookCollection
```
Nå har vi tilgang til `Book`-modulen uten å gå gjennom pakken: 

```python
>>> my_book = Book.Book()
```

Nå kan vi opprette objekter av typen `Book` og `BookCollection`, og utføre metodene som objektene tilbyr. Slik kan vi gjennom kommandolinjen opprette vårt personlige bibliotek!

Det er viktig å huske at alle objekter vi oppretter kun blir lagret i minnet, så hvis vi lukker Python-tolkeren, mister vi objektene. 

For at programmet vårt skal bli et fullverdig biblioteksverktøy, må vi inkludere funksjonalitet for permanent lagring, for eksempel i en database. Videre ville det være naturlig å lage et grafisk brukergrensesnitt, for eksempel en nettside som kjører på din egen maskin. Disse temaene kan du lære mer om i kurset *Informasjonsteknologi 1*. 

