---
title: "Programmeringsparadigme"
belongs_to_chain: "Når og hvorfor brukes objektorientert programmering?"
figures_to_include:
	- "programmeringsparadigmer.svg"
---

Grunnleggjande sett handlar programmering om å gjera operasjonar på data. Me kan til dømes gjera operasjonar på punkt i planet, slik som å rekna ut avstand (med Pytagoras' setning):

```py
p = (3, 4)
q = (1, 5)
o = (0, 0)

avstand_p_q = ((p[0]-q[0])**2+(p[1]-q[1])**2)**0.5
avstand_q_o = ((q[0]-o[0])**2+(q[1]-o[1])**2)**0.5
```
Her gir me datamaskina ei rekkje kommandoar som skal utførast i sekvens. Det er lett å tenkja at all programmering er slik, men det finst programmeringsspråk der ein beskriv kva som er ønskt resultat utan å gi slike kommandoar.

*Viss du har teke Informasjonsteknologi 1, så har du skrive databasespørjingar. Dette er også programmering, der me gir datamaskina ei presis skildring av tabellen me ønskjer å få ut, og datamaskina formar sjølv om denne skildringa til ei rekkje steg som må utførast.*

Å skriva ein sekvens med kommandoar blir kalla *imperativ programmering*, medan å beskriva ønsket resultat (til dømes med ei databasespørjing) blir kalla *deklarativ programmering*. Følgjande diagram viser nokre av måtane å programmera på:

<img src="/media/markdowncontent/assosiated_files/programmeringsparadigmer.svg">

Dei ulike måtane blir gjerne kalla *programmeringsparadigme*. Ulike språk nyttar seg av ulike paradigme, eller ein kombinasjon. *Java* er eit typisk objektorientert (og dermed også imperativt) programmeringsspråk, medan *SQL* er eit deklarativt språk. Me skal bruka *Python*, som er på venstre side av diagrammet, men som elles er allsidig. Med Python gir me altså konkrete kommandoar til datamaskina, men me har elles stor fridom til å nytta ulike paradigme i den imperative greina.

Målet er at du skal utvida verktøykassa di med nye måtar å programmera på, og ta i bruk paradigme som er eigna for problemstillingane du møter. I dette kapittelet skal me beskriva når og kvifor objektorientert programmering er nyttig. Me ser først på eit paradigme du antakeleg har brukt allereie.

