---
title: "Alfabet"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I førre kapittel sa me at digitale data kan skrivast som ein sekvens av teikn. Desse teikna må komma frå eit alfabet. Når me snakkar om eit alfabet i informatikk, tenkjer me ikkje nødvendigvis på det latinske eller norske alfabetet. Eit *alfabet* er rett og slett berre ei mengd av distinkte teikn.

Følgjande mengd er eit alfabet:

```
0,1,2,3,4,5,6,7,8,9
```

Frå dette alfabetet kan me laga *strenger*, til dømes *123*, *05235* og  *000000*. Ein *streng* er rett og slett ein sekvens av teikn frå eit alfabet.

Arvestoffet vårt (DNA) inneheld utruleg mykje digitalt data. Mellom anna finst rundt $20.000$ gen som fungerer som oppskrifter på protein, og proteina er arbeidsmaskinene som står bak dei biologiske prosessane i kroppen. Til dømes er *insulin* eit protein som sørgjer for at karbohydrat blir tekne opp av cellene når me har ete. Oppskrifta på insulin er følgjande DNA-sekvens:

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
Frå eit informatisk perspektiv kan me sjå på dette som ein streng som kjem frå følgjande alfabet:

```
A, C, G, T
```

Oppskrifta på insulin er altså laget med berre fire teikn! Det er fordi DNA-sekvensen i kroppen vår er bygd opp med dei fire *nitrogenbasane* adenin (A), cytosin (C), guanin (G), og tymin (T).

Alle gen i arvestoffet vårt er altså strenger som kjem frå dette vesle alfabetet. Men proteina som kan dannast frå desse gena er utruleg ulike og komplekse. Protein er bygd opp av aminosyrer, og det finst 20 av dei! Korleis kan fira teikn vera nok til å laga ei oppskrift på eit protein?

Når oppskrifta ovanfor blir lesen i ei celle, så blir lese ho ikkje teikn for teikn, ho blir lese tre teikn om gongen! Tre teikn blir omsette til éi aminosyre i samsvar med [denne](https://en.wikipedia.org/wiki/dna_and_rna_codon_tables#Standard_DNA_codon_table) tabellen. Til dømes vil sekvensen *TTC* blir omsett til aminosyra *fenylalanin*, medan sekvensen *TAA* fortel at oppskrifta er slutt.

For å samanfatta kan me seia at storleiken på eit alfabet ikkje avgrensar kva me kan uttrykkja med alfabetet. Sjølv om me har få teikn, kan me nemleg laga uendeleg mange *kombinasjonar av teikn*.

**Aktivitetsforslag 1**:

Ta utgangspunkt i følgjande DNA-sekvens:

```
ATGCAAGCTAATGGGTTCCAGTAA
```

Gå ut frå at dette er eit gen, altså ei oppskrift på eit protein.
Bruk [DNA-til-aminosyre-tabellen](https://en.wikipedia.org/wiki/dna_and_rna_codon_tables#Standard_DNA_codon_table) til å finna sekvensen av aminosyrer som proteinet er bygd opp av.

**Aktivitetsforslag 2:** Ta utgangspunkt i følgjande alfabet:

```
@, !, =
```

*@@* og *!=* er døme på strenger av lengd 2. Kan du på ein systematisk måte skriva opp alle moglege strenger av lengd 2? Kva med alle strenger av lengd 3?

Tenk deg no at *@@@* er ein kode som betyr mellomrom. Lag ein unik kode for alle bokstavane i alfabetet (du kan utelata *x*, *z*, *w* og *c*), og lag også ein unik kode for komma og punktum. Det er viktig at alle teikn har ulike kodar!

Oversett følgjande setning til kodane du har laga:

*Eg har berre tre teikn, men kan skriva kva som helst.*

Hugs at du også må omsetja mellomrom!

