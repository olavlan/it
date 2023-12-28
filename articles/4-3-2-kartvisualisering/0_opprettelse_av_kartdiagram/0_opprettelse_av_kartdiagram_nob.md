---
title: "Opprettelse av kartdiagram"
figures_to_include:
	- "osm_export_share.png"
	- "4-3-2-kartvisualisering_5_0.png"
	- "4-3-2-kartvisualisering_8_0.png"
	- "4-3-2-kartvisualisering_10_0.png"
	- "4-3-2-kartvisualisering_12_1.png"
	- "4-3-2-kartvisualisering_16_0.png"
	- "4-3-2-kartvisualisering_20_0.png"
---

Hva om vi ønsker å markere sykkelstasjonene som sirkler på på et kart, der størrelsen på sirkelen indikerer hvor populær stasjonen er? I disse seksjonene skal vi lære å visualisere data på kart!

I den første seksjonen skal vi gå gjennom følgende steg: 
1. Laste ned et høyoppløselig bilde av et kart.
2. Bruke Python til å opprette et *plott*, det vil si et diagram med en $x$ -og $y$-akse.
3. Sette bildet av kartet inn i plottet, på riktige koordinater i henhold til lengde -og breddegrad.
4. Sette inn objekter på bestemte lengde -og breddegrader.

For å kunne gjøre kartvisualisering på eksamen må du ta høyde for følgende: 
* Steg 1 krever internettilkobling og må gjøres **før** eksamen.
* Steg 2-4 krever ikke internettilkobling og kan gjøres **under** eksamen.

**1. Laste ned statisk kart.** I dette steget ønsker vi å laste ned et bestemt segment av et kart. I prinsippet kan man ta et skjermbilde fra *Google Maps*, men vi skal her vise en framgangsmåte som gir et mer høyoppløselig og nøyaktig resultat. 

a) Vi går inn på [*OpenStreetMap*](https://www.openstreetmap.org/) i en valgfri nettleser. *OpenStreetMap* (*OSM*) er en svært populær kartdatabase blant programmerere, fordi kartdataene er fritt tilgjengelig for nedlasting og bruk i egne programmer. Databasen vedlikeholdes og oppdateres av frivillige.

b) Vi åpner panelene *Export* og *Share* ved å trykke på følgende knapper:

<img src="/media/markdowncontent/assosiated_files/osm_export_share.png" width=600>

c) Vi flytter og zoomer kartet slik at det ønskede området er i kartvinduet. Dersom du ønsker et mer rektangulært eller mer kvadratisk utsnitt, må du endre **nettleservinduet**. 

d) Vi gjør følgende to steg **uten å bevege** på kartet:

* I *Share*-vinduet er det et felt som heter *Scale*. Vi skriver inn tallet 1 og trykker *Enter*. Da vil tallet endres til lavest mulige verdi og et *PNG*-bilde vil lastes ned. Dette bildet vil ha høyest mulig oppløsning for det valgte kartutsnittet.
* Øverst i *Export*-vinduet finner vi lengde -og breddegraden til sidekantene i bildet. Vi noterer disse verdiene i en Python-fil:


```python
map_image_file = "oslo.png"
left = 10.6426
right = 10.8304
bottom = 59.8915
top = 59.9619
```

Det er svært viktig å ta vare på disse verdiene, slik at vi senere kan plassere bildet riktig i koordinatsystemet. 

**2. Opprette et plott**. Et *plott* er som nevnt et diagram med en $x$ -og $y$-akse, der vi for eksempel kan sette inn punkter, linjer og grafer, slik vi er vant til i matematikkfagene. Vi bruker følgende kommando for å opprette diagrammet: 


```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_5_0.png' width=600>
    


Forklaring:

* Det er vanlig å bruke kommoandoen `fig, ax = plt.subplots()` for å opprette et diagram. Variabelen `ax` vil inneholde koordinatsystemet, mens `fig` vil inneholde hele figuren, med eventuelle overskrifter og annet.
* Vi bruker funksjonen `plt.show()` for å vise figuren. Denne funksjonen skal alltid skrives **til slutt** i Python-filen. Når du kjører Python-programmet, vil den ferdige figuren komme opp i et eget vindu. Deretter kan du lagre figuren som en bildefil.
* Begge funksjonene er hentet fra Python-pakken [*matplotlib.pyplot*](https://matplotlib.org/3.5.3/index.html). En vanlig praksis er å gi navnet `plt` til denne pakken, slik vi har gjort her.

**3. Sette inn kart i plottet.** Nå skal vi igjen opprette et diagram, og sette inn bildet av kartet:


```python
from matplotlib.image import imread

fig, ax = plt.subplots(dpi=500)
image = imread('oslo.png')
ax.imshow(image)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_8_0.png' width=600>
    


Forklaring: 
* Vi bruker parameteren `dpi=500` for å gi figuren høy oppløsning, slik at vi senere kan zoome inn på detaljer i kartet. *Dersom koden tar lang tid å kjøre på din maskin, kan du forsøke å redusere denne verdien.*
* Vi må først laste inn bildet med funksjonen `imread`, som vi importerer fra `matplotlib.image`.
* Vi bruker funksjonen `ax.imshow` for å legge bildet inn i koordinatsystemet. Merk at funksjonen brukes på objektet `ax`, som inneholder selve koordinatsystemet.
* Siden bildet er $2297\times 1717$ piksler, har bildet blitt lagt inn på koordinatene 0 til 2297 i $x$-retning, og 0 til 1717 i $y$-retning. Som standard vokser $y$-aksen nedover når man legger inn et bilde.

Vi skal nå modifisere programmet, slik at $x$-aksen svarer til lengdegrad, og $y$-aksen svarer til breddegrad. Husk at vi tok vare på lengde -og breddegraden til sidekantene i det første steget.


```python
fig, ax = plt.subplots(dpi=500)

left = 10.6426
right = 10.8304
bottom = 59.8915
top = 59.9619

image = imread('oslo.png')
ax.imshow(image, extent=(left, right, bottom, top))

plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_10_0.png' width=600>
    


Her har vi inkludert parameteren `extent=[left, right, bottom, top]`, som definerer en "boks" i koordinatsystemet der bildet skal legges inn. Merk at sidene må listes i nøyaktig denne rekkefølgen.

Men her har det oppstått et problem, nemlig at bildet har blitt "strukket ut" i $x$-retning. Hvorfor har dette skjedd? 

Dersom du finner et bilde av jordkloden med lengde -og breddegrader, vil du se at lengdegradene ($x$-verdiene) ligger tettere sammen nær polene enn nær ekvator, mens breddegradene ($y$-verdiene) ligger i samme avstand over hele jordkloden. Siden Norge er langt nord, må vi sørge for at $x$-verdiene ligger tettere sammen enn $y$-verdiene. 

For å finne nøyaktig riktig forhold mellom $y$ -og $x$-aksen, skal vi bruke en matematisk formel. Du trenger ikke forstå formelen, men kan kopiere kodelinjen inn i ditt eget program.


```python
fig, ax = plt.subplots(dpi=500)

left = 10.6426
right = 10.8304
bottom = 59.8915
top = 59.9619

image = imread('oslo.png')
ax.imshow(image, extent=(left, right, bottom, top))

aspect_ratio = (image.shape[0] / (top - bottom))/(image.shape[1] / (right - left))
ax.set_aspect(aspect_ratio)

print(aspect_ratio)

plt.show()
```

    1.994032483080709



    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_12_1.png' width=600>
    


Sideforholdet mellom $y$ -og $x$-aksen kalles *aspect ratio*, og i dette tilfellet er den omtrent 2. Det betyr at én enhet på $y$-aksen skal være dobbelt så lang som én enhet på $x$-aksen. Vi bruker funksjonen `ax.set_aspect` til å sette ønsket sideforhold. 

Basert på det vi har lært, kan vi nå definere en funksjon som setter et kart inn i et koordinatsystem: 


```python
def insert_map(image_file, left, right, bottom, top):
    ax = plt.gca()
        
    map_image = imread(image_file)
    ax.imshow(map_image, extent=(left, right, bottom, top))

    aspect_ratio = (map_image.shape[0] / (top - bottom))/(map_image.shape[1] / (right - left))
    ax.set_aspect(aspect_ratio)

    ax.set_xticks([])
    ax.set_yticks([])
```

*De siste linjene i funksjonen fjerner merkingen på aksene, siden vi ikke trenger å se koordinatene i de neste stegene.*

Nå kan vi enkelt opprette ett plott, sette inn kartet, og vise diagrammet: 


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_16_0.png' width=600>
    


**4. Sette inn objekter.** Nå er vi klare for å sette inn objekter på kartet. Som eksempel skal vi sette inn følgende stasjon: 

```json
{
    "551": {
        "name": "Olaf Ryes plass",
        "description": "langs Sofienberggata",
        "latitude": 59.922425,
        "longitude": 10.758182  
    }
}
```
Disse dataene henter vi i variabelen `stations`:


```python
p = stations.loc["377"]

x = p["longitude"]
y = p["latitude"]

print(x,y)
```

    10.7775665 59.915667


Vi bruker funksjonen `ax.plot` til å tegne punktet på kartet: 


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
ax.plot(x, y, 'o', color="blue", markersize=3)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_20_0.png' width=600>
    


Forklaring av parametrene til funksjonen `ax.plot`:
* De to første parametrene er $x$ og -$y$-verdien der objektet skal plasseres.
* Den tredje parameteren er en streng eller tall som definerer formen til objektet - [her](https://matplotlib.org/stable/api/markers_api.html) kan du se en oversikt over mulige alternativer.
* Til slutt definerer vi fargen og størrelsen til objektet.

**Oppsummering.** I denne seksjonen har vi sett hvordan vi henter et kartbilde med høy oppløsning, og setter det riktig inn i et koordinatsystem. Dette gjør at vi enkelt kan sette inn punkter (eller andre objekter) med bestemte geografiske koordinater. 

**Aktivitetsforslag.** Følg stegene i denne seksjonen til å vise et kart over ditt hjemsted. Finn koordinatene til din hjemadresse og tegn det som et objekt i kartet. Sett inn andre punkter etter eget ønske. Eksperimenter gjerne med forskjellig form, farge og størrelse på objektene.

