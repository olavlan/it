---
title: "Kartvisualisering "
figures_to_include:
	- "4-3-2-kartvisualisering_25_0.png"
	- "4-3-2-kartvisualisering_35_0.png"
	- "4-3-2-kartvisualisering_41_0.png"
---

Vi ønsker nå å gå gjennom alle stasjonene og plassere dem på kartet. Siden stasjonene er lagret i en tabell, skal vi ikke bruke en løkke. Vi følger i stedet den faste oppskriften (fra seksjonen *Tabelloperasjoner*) med å lage en funksjon for det som skal gjøres på **én rad** i tabellen:


```python
def place_on_map(row):
    x = row["longitude"]
    y = row["latitude"]
    ax.plot(x, y, 'o', color="blue", markersize=1)
    return
```

Med `apply` kan vi nå utføre funksjonen på alle radene i turtabellen:


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
stations.apply(place_on_map, axis=1)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_25_0.png' width=600>
    


Men hva om vi nå ønsker at størrelsen til hver sirkel skal indikere populariteten til stasjonen? 

Vi må begynne med å hente antall forekomster av hver stasjon i turtabellen: 


```python
counts = trips["start_station_id"].value_counts()
print(counts)
```

    start_station_id
    464     1598
    551     1590
    479     1550
    421     1525
    396     1468
            ... 
    1919      75
    560       65
    527       37
    3725       5
    612        1
    Name: count, Length: 266, dtype: int64


Forklaring: ved å skrive `trips["start_station_id"].value_counts()`, henter vi først kolonnen *start_station_id*, og deretter ber vi om antall forekomster av hver verdi. 

Resultatet vi får er en kolonne som inneholder tallene 1598, 1590, 1550, og så videre. Kolonnen er også indeksert etter *start_station_id*, og dermed kan vi lese at tallet 1598 tilhører stasjonen med id 464. Altså ble denne stasjonen brukt 2598 ganger som startstasjon. 

I forrige seksjon sørget vi for at stasjonstabellen er indeksert etter stasjons-id. Siden kolonnen vi fikk over også har denne indekseringen, kan vi sette den inn i tabellen: 


```python
stations["used_as_start"] = trips["start_station_id"].value_counts()
stations.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>description</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>used_as_start</th>
    </tr>
    <tr>
      <th>id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>387</th>
      <td>Studenterlunden</td>
      <td>langs Karl Johan</td>
      <td>59.914586</td>
      <td>10.735453</td>
      <td>466</td>
    </tr>
    <tr>
      <th>2315</th>
      <td>Rostockgata</td>
      <td>utenfor Bjørvika visningssenter</td>
      <td>59.906920</td>
      <td>10.760312</td>
      <td>1005</td>
    </tr>
    <tr>
      <th>384</th>
      <td>Vår Frelsers gravlund</td>
      <td>langs Ullevålsveien</td>
      <td>59.919440</td>
      <td>10.743765</td>
      <td>887</td>
    </tr>
    <tr>
      <th>584</th>
      <td>Henrik Wergelands allé</td>
      <td>ved Bogstadveien</td>
      <td>59.926894</td>
      <td>10.720789</td>
      <td>723</td>
    </tr>
    <tr>
      <th>600</th>
      <td>Dyvekes bru</td>
      <td>ved skatepark</td>
      <td>59.905323</td>
      <td>10.768958</td>
      <td>598</td>
    </tr>
  </tbody>
</table>
</div>



Nå inneholder altså stasjonstabellen kolonnen *used_as_start*, som vi skal bruke til å bestemme størrelsen på sirklene.

Den mest populære stasjonen bør ha den største sirkelen:


```python
max_value = stations["used_as_start"].max()
print(max_value)
```

    1598


Den mest populære stasjonen ble altså brukt 1598 ganger.
La oss si at denne stasjonen skal ha en sirkel med diameter 80 mm.

Hva med de andre stasjonene? Hvis en stasjon for eksempel ble brukt 799 ganger, skal diameteren være $799/1598 = 0.5$ ganger så stor som den største sirkelen. Diameteren blir da 80 $\cdot$ 0.5 mm $=$ 40 mm. En stasjon som blir brukt halvparten så mye som en annen stasjon, får altså en halvparten så stor sirkel.

Som vanlig må vi definere en funksjon for det vi ønsker å gjøre med **én rad** i stasjonstabellen:


```python
max_value = stations["used_as_start"].max()
max_diameter = 5
def place_on_map_by_popularity(row):
    x = row["longitude"]
    y = row["latitude"]
    value = row["used_as_start"]
    diameter = max_diameter * (value/max_value)
    ax.plot(x, y, 'o', color="blue", markersize=diameter)
    return
```

Merk at vi har brukt parameteren *markersize* til å angi diameteren til sirkelen. Legg også merke til formelen for å regne ut diameteren.

Nå kan vi igjen plotte kartet og bruke funksjonen på alle radene:


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
stations.apply(place_on_map_by_popularity, axis=1)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_35_0.png' width=600>
    


Her har vi visualisert hva som er mest populært som startstasjoner, men kanskje vi også ønsker å visualisere de mest populære endestasjonene?

Ved å følge samme metode som tidligere, kan vi opprette en kolonne i stasjonstabellen som inneholder antall ganger hver stasjon er brukt som endestasjon:


```python
stations["used_as_end"] = trips["end_station_id"].value_counts()
```

Det neste steget er som vanlig en funksjon for det vi ønsker å gjøre med én rad i stasjonstabellen. 

Funksjonen vi nå trenger er nesten helt lik den forrige. Den eneste forskjellen er at vi skal bruke kolonnen *used_as_end* i stedet for *used_as_start*. 

For å gjøre koden vår mer effektiv, kan vi lage en generell funksjon for å sette inn alle punktene: 


```python
def place_weighted_points(table, column):
    max_value = table[column].max()
    max_markersize = 5

    def place_weighted_point(row):
        x = row["longitude"]
        y = row["latitude"]
        value = row[column]
        markersize = max_markersize * (value/max_value)
        ax.plot(x, y, 'o', color="blue", markersize=markersize)
        return
    
    table.apply(place_weighted_point, axis=1)
```

Merk at denne funksjonen tar en tabell og et kolonnenavn som parametre. Tenk deg at tabellen `stations` og kolonnenavnet *used_as_end* blir brukt som parametre. Da vil følgende skje:

1. Maksimumsverdien til kolonnen hentes.
2. En radfunksjon defineres i henold til hvilken kolonne som er valgt. 
3. Radfunksjonen brukes på alle rader i stasjonstabellen.

Vi tester den nye funksjonen:


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
place_weighted_points(stations, "used_as_end")
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_41_0.png' width=600>
    


**Oppsummering.** I denne seksjonen har vi tatt utgangspunkt i en tabell med geografiske punkter, og vist hvordan vi kan visualisere alle punktene som sirkler på et kart. Dersom hvert punkt har en tilknyttet tallverdi, kan dette vises gjennom størrelsen på sirklene. Dette gjør at vi effektivt kan sammenligne punkter eller områder på kartet, og finne trender i dataene.

