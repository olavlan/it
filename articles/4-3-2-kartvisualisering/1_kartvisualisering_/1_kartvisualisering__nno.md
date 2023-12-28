---
title: "Kartvisualisering"
figures_to_include:
	- "4-3-2-kartvisualisering_25_0.png"
	- "4-3-2-kartvisualisering_35_0.png"
	- "4-3-2-kartvisualisering_41_0.png"
---

Me ønskjer no å gå gjennom alle stasjonane og plassera dei på kartet. Sidan stasjonane er lagra i ein tabell, skal me ikkje bruka ei løkke. Me følgjer i staden den faste oppskrifta (frå seksjonen *Tabelloperasjoner*) med å laga ein funksjon for det som skal gjerast på **éi rad** i tabellen:


```python
def place_on_map(row):
    x = row["longitude"]
    y = row["latitude"]
    ax.plot(x, y, 'o', color="blue", markersize=1)
    return
```

Med `apply` kan me no utføra funksjonen på alle radene i turtabellen:


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
stations.apply(place_on_map, axis=1)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_25_0.png' width=600>
    


Men kva om me no ønskjer at storleiken til kvar sirkel skal indikera populariteten til stasjonen?

Me må byrja med å henta talet på førekomstar av kvar stasjon i turtabellen:


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


Forklaring: ved å skriva `trips["start_station_id"].value_counts()`, hentar me først kolonnen *start_station_id*, og deretter ber me om talet på førekomstar av kvar verdi.

Resultatet me får er ein kolonne som inneheld tala 1598, 1590, 1550, og så vidare. Kolonnen er også indeksert etter *start_station_id*, og dermed kan me lesa at talet 1598 tilhøyrer stasjonen med id 464. Altså vart denne stasjonen brukt 2598 gonger som startstasjon.

I førre seksjon sørgde me for at stasjonstabellen er indeksert etter stasjons-id. Sidan kolonnen me fekk over også har denne indekseringa, kan me setja ho inn i tabellen:


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
<td>utanfor Bjørvika visningssenter</td>
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



No inneheld altså stasjonstabellen kolonnen *used_as_start*, som me skal bruka til å bestemma storleiken på sirklane.

Den mest populære stasjonen bør ha den største sirkelen:


```python
max_value = stations["used_as_start"].max()
print(max_value)
```

    1598


Den mest populære stasjonen vart altså brukt 1598 gonger.
La oss seia at denne stasjonen skal ha ein sirkel med diameter 80 mm.

Kva med dei andre stasjonane? Viss ein stasjon til dømes vart brukt 799 gonger, skal diameteren vera $799/1598 = 0.5$ gonger så stor som den største sirkelen. Diameteren blir då 80 $\cdot$ 0.5 mm $=$ 40 mm. Ein stasjon som blir brukt halvparten så mykje som ein annan stasjon, får altså ein halvparten så stor sirkel.

Som vanleg må me definera ein funksjon for det me ønskjer å gjera med **éi rad** i stasjonstabellen:


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

Merk at me har brukt parameteren *markersize* til å angi diameteren til sirkelen. Legg også merke til formelen for å rekna ut diameteren.

No kan me igjen plotta kartet og bruka funksjonen på alle radene:


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
stations.apply(place_on_map_by_popularity, axis=1)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_35_0.png' width=600>
    


Her har me visualisert kva som er mest populært som startstasjonar, men kanskje me også ønskjer å visualisera dei mest populære endestasjonane?

Ved å følgja same metode som før, kan me oppretta ein kolonne i stasjonstabellen som inneheld talet på gonger kvar stasjon er brukt som endestasjon:


```python
stations["used_as_end"] = trips["end_station_id"].value_counts()
```

Det neste steget er som vanleg ein funksjon for det me ønskjer å gjera med éi rad i stasjonstabellen.

Funksjonen me no treng er nesten heilt lik den førre. Den einaste forskjellen er at me skal bruka kolonnen *used_as_end* i staden for *used_as_start*.

For å gjera koden vår meir effektiv, kan me laga ein generell funksjon for å setja inn alle punkta:


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

Merk at denne funksjonen tek ein tabell og eit kolonnenamn som parametrar. Tenk deg at tabellen `stations` og kolonnenamnet *used_as_end* blir brukt som parametrar. Då vil følgjande skje:

1. Maksimumsverdien til kolonnen blir henta.
2. Ein radfunksjon blir definert i henold til kva kolonne som er vald.
3. Radfunksjonen blir brukt på alle rader i stasjonstabellen.

Me testar den nye funksjonen:


```python
fig, ax = plt.subplots(dpi=500)
insert_map("oslo.png", 10.6426, 10.8304, 59.8915, 59.9619)
place_weighted_points(stations, "used_as_end")
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-2-kartvisualisering_41_0.png' width=600>
    


**Oppsummering.** I denne seksjonen har me teke utgangspunkt i ein tabell med geografiske punkt, og vist korleis me kan visualisera alle punkta som sirklar på eit kart. Dersom kvart punkt har ein tilknytta talverdi, kan dette visast gjennom storleiken på sirklane. Dette gjer at me effektivt kan samanlikna punkt eller område på kartet, og finna trendar i dataa.

