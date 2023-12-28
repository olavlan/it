---
title: "Hvordan lagres tegn? "
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I forrige seksjon så vi at det finnes en standard for hvilke binærkoder farger skal ha. I denne seksjonen skal vi se at det også finnes standarder for hvilke binærkoder tegn skal ha. Alle tegn du kan skrive på tastaturet ditt må ha en binærkode! Det gjelder både bokstaver og spesialtegn, inkludert mellomrom! 

Datamaskiner hadde i begynnelsen liten lagringsplass, så man ønsket små binærkoder. Man kom fram til at med syv bits kunne man lage koder for de viktigste tegnene (i den vestlige verden). For eksempel brukte man koden *110 0001* for bokstaven *a*. Denne standarden kalles *ASCII*. 

Hvor mange binærkoder kan man lage med syv bits? Det kan man finne ut av ved å telle fra *000 0000*  til *111 1111*, altså det laveste og høyeste tallet man kan skrive med syv bits (i det binære tallsystemet).

Tallet *111 1111* kan oversettes til $64 + 32 + 16 + 8 + 4 +2 +1$, som er lik $127$. Med syv bits kan vi altså skrive alle tall mellom 0 og 127. Det betyr at det finnes 128 forskjellige bitstrenger fra *000 0000* til *111 1111*.  Med andre ord kan vi gi en kode til 128 forskjellige tegn. [Her](https://en.wikipedia.org/wiki/ASCII#Printable_characters) kan du se hvilke tegn man valgte å ta med i standarden ASCII, og du kan se binærkoden til hvert tegn. 

**Aktivitetsforslag 1.**  Følgende bitstreng er et spørsmål skrevet i *ASCII*-kode:

```
1001000 1110110 1100001 0100000 1110011 1111001 1101110 1100101 1110011 0100000 1100100 1110101 0100000 1101111 1101101 0100000 1000001 1010011 1000011 1001001 1001001 0111111
```

Bruk [ASCII-tabellen](https://en.wikipedia.org/wiki/ASCII#Printable_characters) til å oversette bitstrengen, og svar på spørsmålet. 

**Aktivitetsforslag 2.** Skriv en setning til en medelev, og bruk [ASCII-tabellen](https://en.wikipedia.org/wiki/ASCII#Printable_characters) til å skrive den som *ASCII*-kode. Be medeleven din om å oversette setningen. 

