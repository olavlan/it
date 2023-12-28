---
title: "Programmeringsparadigmer"
belongs_to_chain: "Når og hvorfor brukes objektorientert programmering?"
figures_to_include:
	- "programmeringsparadigmer.svg"
---

Grunnleggende sett handler programmering om å gjøre operasjoner på data. Vi kan for eksempel gjøre operasjoner på punkter i planet, slik som å regne ut avstand (med Pytagoras' setning):

```py
p = (3, 4)
q = (1, 5)
o = (0, 0)

avstand_p_q = ((p[0]-q[0])**2+(p[1]-q[1])**2)**0.5
avstand_q_o = ((q[0]-o[0])**2+(q[1]-o[1])**2)**0.5
```
Her gir vi datamaskinen en rekke kommandoer som skal utføres i sekvens. Det er lett å tenke at all programmering er slik, men det finnes programmeringsspråk der man beskriver hva som er ønsket resultat uten å gi slike kommandoer. 

*Hvis du har tatt Informasjonsteknologi 1, så har du skrevet databasespørringer. Dette er også programmering, der vi gir datamaskinen en presis beskrivelse av tabellen vi ønsker å få ut, og datamaskinen omformer selv denne beskrivelsen til en rekke steg som må utføres.*

Å skrive en sekvens med kommandoer kalles *imperativ programmering*, mens å beskrive ønsket resultat (for eksempel med en databasespørring) kalles *deklarativ programmering*. Følgende diagram viser noen av måtene å programmere på:

<img src="/media/markdowncontent/assosiated_files/programmeringsparadigmer.svg">

De ulike måtene kalles gjerne *programmeringsparadigmer*. Ulike språk benytter seg av ulike paradigmer, eller en kombinasjon. *Java* er et typisk objektorientert (og dermed også imperativt) programmeringsspråk, mens *SQL* er et deklarativt språk. Vi skal bruke *Python*, som befinner seg på venstre side av diagrammet, men som ellers er allsidig. Med Python gir vi altså konkrete kommandoer til datamaskinen, men vi har ellers stor frihet til å benytte ulike paradigmer i den imperative grenen. 

Målet er at du skal utvide din verktøykasse med nye måter å programmere på, og ta i bruk paradigmer som er egnet for problemstillingene du møter. I dette kapittelet skal vi beskrive når og hvorfor objektorientert programmering er nyttig. Vi ser først på et paradigme du antagelig har brukt allerede.

