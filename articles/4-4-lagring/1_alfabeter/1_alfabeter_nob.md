---
title: "Alfabeter"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I forrige kapittel sa vi at digitale data kan skrives som en sekvens av tegn. Disse tegnene må komme fra et alfabet. Når vi snakker om et alfabet i informatikk, tenker vi ikke nødvendigvis på det latinske eller norske alfabetet. Et *alfabet* er rett og slett bare en mengde av distinkte tegn.

Følgende mengde er et alfabet: 

```
0,1,2,3,4,5,6,7,8,9
```

Fra dette alfabetet kan vi lage *strenger*, for eksempel *123*, *05235* og  *000000*. En *streng* er rett og slett en sekvens av tegn fra et alfabet.

Arvestoffet vårt (DNA) inneholder utrolig mye digital data. Blant annet finnes rundt $20.000$ gener som fungerer som oppskrifter på proteiner, og proteinene er arbeidsmaskinene som står bak de biologiske prosessene i kroppen. For eksempel er *insulin* et protein som sørger for at karbohydrater blir tatt opp av cellene når vi har spist. Oppskriften på insulin er følgende DNA-sekvens: 

```
AGCCCTCCAGGACAGGCTGCATCAGAAGAGGCCATCAAGCAGGTCTGTTCCAAGGGCCTTTGCGTCAGGT
GGGCTCAGGATTCCAGGGTGGCTGGACCCCAGGCCCCAGCTCTGCAGCAGGGAGGACGTGGCTGGGCTCG
TGAAGCATGTGGGGGTGAGCCCAGGGGCCCCAAGGCAGGGCACCTGGCCTTCAGCCTGCCTCAGCCCTGC
CTGTCTCCCAGATCACTGTCCTTCTGCCATGGCCCTGTGGATGCGCCTCCTGCCCCTGCTGGCGCTGCTG
GCCCTCTGGGGACCTGACCCAGCCGCAGCCTTTGTGAACCAACACCTGTGCGGCTCACACCTGGTGGAAG
CTCTCTACCTAGTGTGCGGGGAACGAGGCTTCTTCTACACACCCAAGACCCGCCGGGAGGCAGAGGACCT
GCAGGGTGAGCCAACTGCCCATTGCTGCCCCTGGCCGCCCCCAGCCACCCCCTGCTCCTGGCGCTCCCAC
CCAGCATGGGCAGAAGGGGGCAGGAGGCTGCCACCCAGCAGGGGGTCAGGTGCACTTTTTTAAAAAGAAG
TTCTCTTGGTCACGTCCTAAAAGTGACCAGCTCCCTGTGGCCCAGTCAGAATCTCAGCCTGAGGACGGTG
TTGGCTTCGGCAGCCCCGAGATACATCAGAGGGTGGGCACGCTCCTCCCTCCACTCGCCCCTCAAACAAA
TGCCCCGCAGCCCATTTCTCCACCCTCATTTGATGACCGCAGATTCAAGTGTTTTGTTAAGTAAAGTCCT
GGGTGACCTGGGGTCACAGGGTGCCCCACGCTGCCTGCCTCTGGGCGAACACCCCATCACGCCCGGAGGA
GGGCGTGGCTGCCTGCCTGAGTGGGCCAGACCCCTGTCGCCAGGCCTCACGGCAGCTCCATAGTCAGGAG
ATGGGGAAGATGCTGGGGACAGGCCCTGGGGAGAAGTACTGGGATCACCTGTTCAGGCTCCCACTGTGAC
GCTGCCCCGGGGCGGGGGAAGGAGGTGGGACATGTGGGCGTTGGGGCCTGTAGGTCCACACCCAGTGTGG
GTGACCCTCCCTCTAACCTGGGTCCAGCCCGGCTGGAGATGGGTGGGAGTGCGACCTAGGGCTGGCGGGC
AGGCGGGCACTGTGTCTCCCTGACTGTGTCCTCCTGTGTCCCTCTGCCTCGCCGCTGTTCCGGAACCTGC
TCTGCGCGGCACGTCCTGGCAGTGGGGCAGGTGGAGCTGGGCGGGGGCCCTGGTGCAGGCAGCCTGCAGC
CCTTGGCCCTGGAGGGGTCCCTGCAGAAGCGTGGCATTGTGGAACAATGCTGTACCAGCATCTGCTCCCT
CTACCAGCTGGAGAACTACTGCAACTAGACGCAGCCCGCAGGCAGCCCCACACCCGCCGCCTCCTGCACC
GAGAGAGATGGAATAAAGCCCTTGAACCAGC
```
Fra et informatisk perspektiv kan vi se på dette som en streng som kommer fra følgende alfabet: 

```
A, C, G, T
```

Oppskriften på insulin er altså laget med bare fire tegn! Det er fordi DNA-sekvensen i kroppen vår er bygget opp med de fire *nitrogenbasene* adenin (A), cytosin (C), guanin (G), og tymin (T). 

Alle gener i arvestoffet vårt er altså strenger som kommer fra dette lille alfabetet. Men proteinene som kan dannes fra disse genene er utrolig forskjellige og komplekse. Proteiner er bygget opp av aminosyrer, og det finnes 20 av dem! Hvordan kan fire tegn være nok til å lage en oppskrift på et protein?

Når oppskriften ovenfor leses i en celle, så leses den ikke tegn for tegn, den leses tre tegn om gangen! Tre tegn oversettes til én aminosyre i henhold til [denne](https://en.wikipedia.org/wiki/DNA_and_RNA_codon_tables#Standard_DNA_codon_table) tabellen. For eksempel vil sekvensen *TTC* oversettes til aminosyren *fenylalanin*, mens sekvensen *TAA* forteller at oppskriften er slutt. 

For å oppsummere kan vi si at størrelsen på et alfabet ikke begrenser hva vi kan uttrykke med alfabetet. Selv om vi har få tegn, kan vi nemlig lage uendelig mange *kombinasjoner av tegn*. 

**Aktivitetsforslag 1**: 

Ta utgangspunkt i følgende DNA-sekvens:

```
ATGCAAGCTAATGGGTTCCAGTAA
```

Anta at dette er et gen, altså en oppskrift på et protein.
Bruk [DNA-til-aminosyre-tabellen](https://en.wikipedia.org/wiki/DNA_and_RNA_codon_tables#Standard_DNA_codon_table) til å finne sekvensen av aminosyrer som proteinet er bygget opp av.  

**Aktivitetsforslag 2:** Ta utgangspunkt i følgende alfabet: 

```
@, !, =
```

*@@* og *!=* er eksempler på strenger av lengde 2. Kan du på en systematisk måte skrive opp alle mulige strenger av lengde 2? Hva med alle strenger av lengde 3? 

Tenk deg nå at *@@@* er en kode som betyr mellomrom. Lag en unik kode for alle bokstavene i alfabetet (du kan utelate *x*, *z*, *w* og *c*), og lag også en unik kode for komma og punktum. Det er viktig at alle tegn har forskjellige koder!

Oversett følgende setning til kodene du har laget: 

*Jeg har bare tre tegn, men kan skrive hva som helst.*

Husk at du også må oversette mellomrom!

