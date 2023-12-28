---
title: "Korleis blir lagra teikn?"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I førre seksjon såg me at det finnast ein standard for kva binærkoder fargar skal ha. I denne seksjonen skal me sjå at det også finst standardar for kva binærkoder teikn skal ha. Alle teikn du kan skriva på tastaturet ditt må ha ein binærkode! Det gjeld både bokstavar og spesialteikn, inkludert mellomrom!

Datamaskiner hadde i byrjinga liten lagringsplass, så ein ønskte små binærkoder. Ein kom fram til at med sju bitar kunne ein laga kodar for dei viktigaste teikna (i den vestlege verda). Til dømes brukte ein koden *110 0001* for bokstaven *a*. Denne standarden blir kalla *ASCII*.

Kor mange binærkoder kan ein laga med sju bitar? Det kan ein finna ut av ved å telja frå *000 0000*  til *111 1111*, altså det lågaste og høgaste talet ein kan skriva med sju bitars (i det binære talsystemet).

Talet *111 1111* kan omsetjast til $64 + 32 + 16 + 8 + 4 +2 +1$, som er lik $127$. Med sju bitar kan me altså skriva alle tal mellom 0 og 127. Det betyr at det finst 128 ulike bitstrenger frå *000 0000* til *111 1111*.  Med andre ord kan me gi ein kode til 128 ulike teikn. [Her](https://en.wikipedia.org/wiki/ascii#Printable_characters) kan du sjå kva teikn ein valde å ta med i standarden ASCII, og du kan sjå binærkoden til kvart teikn.

**Aktivitetsforslag 1.**  Følgjande bitstreng er eit spørsmål skrive i *ASCII*-kode:

```
1001000 1110110 1100001 0100000 1110011 1111001 1101110 1100101 1110011 0100000 1100100 1110101 0100000 1101111 1101101 0100000 1000001 1010011 1000011 1001001 1001001 0111111
```

Bruk [ASCII-tabellen](https://en.wikipedia.org/wiki/ascii#Printable_characters) til å omsetja bitstrengen, og svar på spørsmålet.

**Aktivitetsforslag 2.** Skriv ei setning til ein medelev, og bruk [ASCII-tabellen](https://en.wikipedia.org/wiki/ascii#Printable_characters) til å skriva den som *ASCII*-kode. Be medeleven din om å omsetja setninga.

