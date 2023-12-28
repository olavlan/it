---
title: "Aktiviteter"
figures_to_include:
---

**Prosjektoppgave 7.** Ta utgangspunkt i klassediagrammet og Python-filene du har fra de forrige prosjektoppgavene. Gjør følgende oppgaver:

1. Definer alle metoder i sine riktige klasser. Her trenger du bare å skrive `return` i selve metodeblokken, men du skal sørge for at metodene er riktig definert med tanke på parametre, og om metoden skal være offentlig eller privat.
2. Dersom du har delmetoder, skal du nå skrive kode i disse. Tegn gjerne figurer som vist i seksjonen *Delmetoder*, slik at du enkelt kan se hvilke metoder som er lurt å starte med. På dette stadiet trenger ikke delmetodene å returnere riktige verdier! Det er nok at delmetodene returnerer noen testverdier.
3. Skriv kode for resten av metodene. Når du skriver kode for en metode som er oppdelt, er det viktig at du tar i bruk delmetodene. Fortsett å bruke testverdier når det er nødvendig. Forsøk å gjøre koden så oversiktlig som mulig, ved å dele den opp i noen enkle steg.
4. Finnes kommunikasjon mellom objekter i koden? Finn i så fall kodelinjene der dette skjer.
6. Marker alle datafelter som private, og opprett offentlige *set*-metoder for de datafeltene som det skal være mulig å endre. Vurder om noen av metodene bør sjekke at parameteren har en gyldig verdi.
7. Opprett offentlige *get*-metoder for de datafeltene som det skal være mulig å hente. Husk at dersom et datafelt har et muterbart objekt, så må du returnere en kopi av objektet.
8.  Har du noen klasser som arver fra en superklasse? Hvilken endring må du gjøre for at disse klassene arver datafeltene metodene til superklassen? 
9. Skriv dokumentasjon av alle klasser og metoder ved å bruke *docstring*.
10. Opprett en mappe for prosjektet ditt, og sørg for at hver klasse er i sin egen modul (sin egen fil). Hvilken ekstra fil må du opprette for at prosjektet ditt skal bli en pakke?
11. Åpne kommandolinjen og importer modulene fra pakken din. Opprett objekter, minst ett objekt fra hver klasse. Forsøk å printe ut objektene. Test alle de offentlige metodene som objektene dine tilbyr, og print ut resultatene. Er utskriftene som forventet?

