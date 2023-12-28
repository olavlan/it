---
title: "Skiping av kartdiagram"
figures_to_include:
	- "osm_export_share.png"
	- "4-3-2-kartvisualisering_5_0.png"
	- "4-3-2-kartvisualisering_8_0.png"
	- "4-3-2-kartvisualisering_10_0.png"
	- "4-3-2-kartvisualisering_12_1.png"
	- "4-3-2-kartvisualisering_16_0.png"
	- "4-3-2-kartvisualisering_20_0.png"
---

Kva om me ønskjer å markera sykkelstasjonane som sirklar på på eit kart, der storleiken på sirkelen indikerer kor populær stasjonen er? I desse seksjonane skal me læra å visualisera data på kart!

I den første seksjonen skal me gå gjennom følgjande steg:
1. Lasta ned eit høgopplausleg bilete av eit kart.
2. Bruke Python til å oppretta eit *plott*, det vil seia eit diagram med ein $x$ -og $y$-akse.
3. Sette biletet av kartet inn i plottet, på rette koordinatar i samsvar med lengd -og breiddegrad.
4. Setja inn objekt på bestemde lengd -og breiddegrader.

For å kunna gjera kartvisualisering på eksamen må du ta høgd for følgjande:
* Steg 1 krev internettilkopling og må gjerast **før** eksamen.
* Steg 2-4 krev ikkje internettilkopling og kan gjerast **under** eksamen.

**1. Lasta ned statisk kart.** I dette steget ønskjer me å lasta ned eit bestemt segment av eit kart. I prinsippet kan ein ta eit skjermbilete frå *Google Maps*, men me skal her vise ein framgangsmåte som gir eit meir høgopplausleg og nøyaktig resultat.

a) Vi går inn på [*OpenStreetMap*](https://www.openstreetmap.org/) i ein valfri nettlesar. *OpenStreetMap* (*OSM*) er ein svært populær kartdatabase blant programmerarar, fordi kartdataa er fritt tilgjengeleg for nedlasting og bruk i eigne program. Databasen blir halden ved like og blir oppdatert av frivillige.

b) Vi opnar panela *Export* og *Share* ved å trykkja på følgjande knappar:

<img src="/media/markdowncontent/assosiated_files/osm_export_share.png" width=600>

c) Vi flyttar og zoomar kartet slik at det ønskte området er i kartvindauget. Dersom du ønskjer eit meir rektangulært eller meir kvadratisk utsnitt, må du endra **nettlesarvindauget**.

d) Vi gjer følgjande to steg **utan å bevega** på kartet:

* I *Share*-vindauget er det eit felt som heiter *Scale*. Me skriv inn talet 1 og trykkjer *Enter*. Då vil talet endrast til lågast moglege verdi og eit *PNG*-bilete vil lastast ned. Dette biletet vil ha høgast mogleg oppløysing for det valde kartutsnittet.
* Øvst i *Export*-vindauget finn me lengd -og breiddegrada til sidekantane i biletet. Me noterer desse verdiane i ei Python-fil:


```python
map_image_file = "oslo.png"
left = 10.6426
right = 10.8304
bottom = 59.8915
top = 59.9619
```

Det er svært viktig å ta vare på desse verdiane, slik at me seinare kan plassera biletet rett i koordinatsystemet.

**2. Opprette eit plott**. Eit *plott* er som nemnt eit diagram med ein $x$ -og $y$-akse, der me til dømes kan setja inn punkt, linjer og grafar, slik me er vant til i matematikkfaga. Me bruker følgjande kommando for å oppretta diagrammet:


```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_5_0.png' width=600>
    


Forklaring:

* Det er vanleg å bruka kommoandoen `fig, ax = plt.subplots()` for å oppretta eit diagram. Variabelen `ax` vil innehalda koordinatsystemet, medan `fig` vil innehalda heile figuren, med eventuelle overskrifter og anna.
* Me bruker funksjonen `plt.show()` for å visa figuren. Denne funksjonen skal alltid skrivast **til slutt** i Python-fila. Når du køyrer Python-programmet, vil den ferdige figuren komma opp i eit eige vindauge. Deretter kan du lagra figuren som ei biletfil.
* Begge funksjonane er henta frå Python-pakken [*matplotlib.pyplot*](https://matplotlib.org/3.5.3/index.html). Ein vanleg praksis er å gi namnet `plt` til denne pakken, slik me har gjort her.

**3. Setja inn kart i plottet.** No skal me igjen oppretta eit diagram, og setja inn biletet av kartet:


```python
from matplotlib.image import imread

fig, ax = plt.subplots(dpi=500)
image = imread('oslo.png')
ax.imshow(image)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_8_0.png' width=600>
    


Forklaring:
* Me bruker parameteren `dpi=500` for å gi figuren høg oppløysing, slik at me seinare kan zooma inn på detaljar i kartet. *Dersom koden tek lang tid å køyra på maskina di, kan du prøva å redusera denne verdien.*
* Me må først lasta inn biletet med funksjonen `imread`, som me importerer frå `matplotlib.image`.
* Me bruker funksjonen `ax.imshow` for å leggja biletet inn i koordinatsystemet. Merk at funksjonen blir brukt på objektet `ax`, som inneheld sjølve koordinatsystemet.
* Sidan biletet er $2297\times 1717$ pikslar, har biletet vorte lagt inn på koordinatane 0 til 2297 i $x$-retning, og 0 til 1717 i $y$-retning. Som standard veks $y$-aksen nedover når ein legg inn eit bilete.

Me skal no modifisera programmet, slik at $x$-aksen svarer til lengdegrad, og $y$-aksen svarer til breiddegrad. Hugs at me tok vare på lengd -og breiddegrada til sidekantane i det første steget.


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
    


Her har me inkludert parameteren `extent=[left, right, bottom, top]`, som definerer ein "boks" i koordinatsystemet der biletet skal leggjast inn. Merk at sidene må listast i nøyaktig denne rekkjefølgja.

Men her har det oppstått eit problem, nemleg at biletet har vorte "strekt ut" i $x$-retning. Kvifor har dette skjedd?

Dersom du finn eit bilete av jordkloden med lengd -og breiddegrader, vil du sjå at lengdegradene ($x$-verdiane) ligg tettare saman nær pola enn nær ekvator, medan breiddegradene ($y$-verdiane) ligg i same avstand over heile jordkloden. Sidan Noreg er langt nord, må me sørgja for at $x$-verdiane ligg tettare saman enn $y$-verdiane.

For å finna nøyaktig rett forhold mellom $y$ -og $x$-aksen, skal me bruka ein matematisk formel. Du treng ikkje forstå formelen, men kan kopiera kodelinja inn i ditt eige program.


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
    


Sideforholdet mellom $y$ -og $x$-aksen blir kalla *aspect ratio*, og i dette tilfellet er han omtrent 2. Det betyr at éi eining på $y$-aksen skal vera dobbelt så lang som éi eining på $x$-aksen. Me bruker funksjonen `ax.set_aspect` til å setja ønsket sideforhold.

Basert på det me har lært, kan me no definera ein funksjon som set eit kart inn i eit koordinatsystem:


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

*Dei siste linjene i funksjonen fjernar merkinga på aksa, sidan me ikkje treng å sjå koordinatane i dei neste stega.*

No kan me enkelt oppretta eitt plott, setja inn kartet, og visa diagrammet:


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_16_0.png' width=600>
    


**4. Setja inn objekt.** No er me klare for å setja inn objekt på kartet. Som døme skal me setja inn følgjande stasjon:

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
Desse dataa hentar me i variabelen `stations`:


```python
p = stations.loc["377"]

x = p["longitude"]
y = p["latitude"]

print(x,y)
```

    10.7775665 59.915667


Me bruker funksjonen `ax.plot` til å teikna punktet på kartet:


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
ax.plot(x, y, 'o', color="blue", markersize=3)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_20_0.png' width=600>
    


Forklaring av parametrane til funksjonen `ax.plot`:
* Dei to første parametrane er $x$ og -$y$-verdien der objektet skal plasserast.
* Den tredje parameteren er ein streng eller tal som definerer forma til objektet - [her](https://matplotlib.org/stable/api/markers_api.html) kan du sjå ei oversikt over moglege alternativ.
* Til slutt definerer me fargen og storleiken til objektet.

**Oppsummering.** I denne seksjonen har me sett korleis me hentar eit kartbilete med høg oppløysing, og set det rett inn i eit koordinatsystem. Dette gjer at me enkelt kan setja inn punkt (eller andre objekt) med bestemde geografiske koordinatar.

**Aktivitetsforslag.** Følg stega i denne seksjonen til å visa eit kart over din heimstad. Finn koordinatane til heimadressa og teikn ditt det som eit objekt i kartet. Set inn andre punkt etter eige ønske. Eksperiment gjerne med ulik form, farge og storleik på objekta.

