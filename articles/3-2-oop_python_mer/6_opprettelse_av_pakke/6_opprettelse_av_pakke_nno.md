---
title: "Skiping av pakke"
figures_to_include:
	- "pythonimport.svg"
---

Fram til no har me definert alle klassar i éi Python-fil, men det kan vera lurt å organisera prosjektet betre. Kort sagt bør me ha éi fil per klasse. Viss me har eit klassediagram som består av klassane `Loanable`, `Book`, og `BookCollection`, kan me oppretta følgjande mappestruktur:
```
└── Desktop
    └── personal-library-tool
        ├── __init__.py
        ├── Loanable.py
        ├── Book.py  
        ├── BookCollection.py
```

Me har oppretta mappa `personal-library-tool/`, der me finn éi fil for kvar klasse, og dessutan den spesielle fila `__init__.py`. Denne fila er for å fortelja Python at `personal-library-tool` er ein pakke!

No er me klare for å testa programmet vårt i kommandolinja (for å opna kommandolinja, kan du bruka programmet `Terminal` på Mac og Linux, eller `cmd.exe` på Windows). Me må først navigera oss inn på mappa der me har lagt `personal-library-tool/` (i dømet ovanfor er det altså `Desktop/` me skal navigera oss inn på).

```bash
~$ cd Desktop
```

Me bruker no kommandoen `python3` til å starta *Python-tolkaren*, som gjer at me kan køyra Python-kode direkte i kommandolinja:

```bash
~/Desktop$ python3
Python 3.8.10 (default, May 26 2023, 14:05:08) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
Det første me må gjera er å importera pakken vår:

```python
>>> import personal-library-tool
```
Korleis tek me i bruk bokklassen til å oppretta eit bokobjekt? Først må me gå inn på rett *modul*. Kvar Python-fil blir til ein modul, så pakken vår består av tre modular:

* `personal-library-tool.Loanable`
* `personal-library-tool.Book`
* `personal-library-tool.BookCollection`

For å oppretta eit bokobjekt, må me gå inn på den andre modulen, og deretter bruka klassen som ligg i modulen:

```python
>>> my_book = personal-library-tool.Book.Book()
```

Følgjande diagram viser kva dei ulike delane betyr:

<img src="/media/markdowncontent/assosiated_files/pythonimport.svg">

For å sleppa å skriva det lange pakkenamnet heile tida, kan me importera modulane direkte:

```python
>>> from personal-library-tool import Loanable, Book, BookCollection
```
No har me tilgang til `Book`-modulen utan å gå gjennom pakken:

```python
>>> my_book = Book.Book()
```

No kan me oppretta objekt av typen `Book` og `BookCollection`, og utføra metodane som objekta tilbyr. Slik kan me gjennom kommandolinja oppretta det personlege biblioteket vårt!

Det er viktig å hugsa at alle objekt me opprettar berre blir lagra i minnet, så viss me lukkar Python-tolkaren, mistar me objekta.

For at programmet vårt skal bli eit fullverdig bibliotekverktøy, må me inkludera funksjonalitet for permanent lagring, til dømes i ein database. Vidare ville det vera naturleg å laga eit grafisk brukargrensesnitt, til dømes ei nettside som køyrer på di eiga maskin. Desse temaa kan du læra meir om i kurset *Informasjonsteknologi 1*.

