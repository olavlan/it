---
title: "Datafelt og verdiar"
belongs_to_chain: "Hva er en klasse?"
figures_to_include:
	- "modell_eksempeldata.svg"
	- "mal.svg"
	- "objekter_fra_mal.svg"
---

I førre kapittel byrja me å planleggja eit ønskt bokprogram. Bøker og personar var objekta i den enklaste modellen. No kan me fylla inn dømedata i modellen, for å visa kva eigenskapar me ønskjer å ta med:

<img src="/media/markdowncontent/assosiated_files/modell_eksempeldata.svg" width="500">

Merk at me fyller inn data på same måte i alle bøker. Slik er det lett å sjå at objekta er av same type. Hadde me skrive sidetalet på ei bok, men talet på kapittel på ei anna bok, ville informasjonen kunna oppfattast som ustrukturert. Me gjer det strukturert ved å ta utgangspunkt i ein *mal*:

<img src="/media/markdowncontent/assosiated_files/mal.svg" width="300">

Figuren viser ein mal for bokobjekt, og ein mal for personobjekt. Malene fortel kva data som skal fyllast inn når me opprettar eit objekt av ein bestemd type. Til dømes seier den første malen at når me opprettar eit bokobjekt, så skal tittel, forfattar og talet på sider fyllast ut. Me viser endå tydelegare korleis dette skjer i neste figur. Under figuren forklarer me kva som skjer.

<img src="/media/markdowncontent/assosiated_files/objekter_fra_mal.svg" width="500">

* For å setja data inn i eit objekt, definerer me variablar i objektet, og set verdiar inn i variablane. Vanlegvis kallar me desse variablane for *datafelta* til objektet.
* Malen bestemmer kva datafelt som skal setjast inn i objekta.
	- Alle bokobjekt får tre datafelt, nemleg `tittel`, `forfatter` og `antall_sider`.
	- Alle personobjekt får to datafelt, nemleg `navn` og `alder`.
* Når me opprettar objekt, kan me også setja *verdiar* inn i datafelta. Til dømes kan me setja verdien `"Sofies verden"` inn i datafeltet `tittel`.
* Datafelta er viste som kvite boksar i objekta, og verdiane er innhaldet i boksane. Dette er ein forenkla versjon av eit *objektdiagram*, som me skal komma tilbake til seinare.


