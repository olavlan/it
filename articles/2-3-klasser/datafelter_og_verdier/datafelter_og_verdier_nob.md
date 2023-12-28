---
title: "Datafelter og verdier"
belongs_to_chain: "Hva er en klasse?"
figures_to_include:
	- "modell_eksempeldata.svg"
	- "mal.svg"
	- "objekter_fra_mal.svg"
---

I forrige kapittel begynte vi å planlegge et ønsket bokprogram. Bøker og personer var objektene i den enkleste modellen. Nå kan vi fylle inn eksempeldata i modellen, for å vise hvilke egenskaper vi ønsker å ta med: 

<img src="/media/markdowncontent/assosiated_files/modell_eksempeldata.svg" width="500">

Merk at vi fyller inn data på samme måte i alle bøker. Slik er det lett å se at objektene er av samme type. Hadde vi skrevet sideantallet på en bok, men antall kapitler på en annen bok, ville informasjonen kunne oppfattes som ustrukturert. Vi gjør det strukturert ved å ta utgangspunkt i en *mal*:

<img src="/media/markdowncontent/assosiated_files/mal.svg" width="300">

Figuren viser en mal for bokobjekter, og en mal for personobjekter. Malene forteller hvilke data som skal fylles inn når vi oppretter et objekt av en bestemt type. For eksempel sier den første malen at når vi oppretter et bokobjekt, så skal tittel, forfatter og antall sider fylles ut. Vi viser enda tydeligere hvordan dette skjer i neste figur. Under figuren forklarer vi hva som skjer. 

<img src="/media/markdowncontent/assosiated_files/objekter_fra_mal.svg" width="500">

* For å sette data inn i et objekt, definerer vi variabler i objektet, og setter verdier inn i variablene. Vanligvis kaller vi disse variablene for *datafeltene* til objektet. 
* Malen bestemmer hvilke datafelter som skal settes inn i objektene.
	- Alle bokobjekter får tre datafelter, nemlig `tittel`, `forfatter` og `antall_sider`.
	- Alle personobjekter får to datafelter, nemlig `navn` og `alder`.
* Når vi oppretter objekter, kan vi også sette *verdier* inn i datafeltene. For eksempel kan vi sette verdien `"Sofies verden"` inn i datafeltet `tittel`.
* Datafeltene er vist som hvite bokser i objektene, og verdiene er innholdet i boksene. Dette er en forenklet versjon av et *objektdiagram*, som vi skal komme tilbake til senere. 


