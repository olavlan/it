---
title: "Introduksjon til pandas"
figures_to_include:
---

Kort sagt er [*pandas*](https://pandas.pydata.org/) ein Python-pakke som gjer det meir effektivt å driva databehandling. I dei førre seksjonane jobba me med dictionary og listar, medan i *pandas* brukast *tabellar*. Me kan oppretta tabellar og utføra operasjonar på dei.

Først viser me korleis ein kan konvertera ein dictionary til ein tabell:


```python
data = [
    {"fornavn": "Ola", "etternavn": "Nordmann", "alder": 17, "bosted": "Oslo", "number_of_children": 0},
    {"fornavn": "Kari", "etternavn": "Svendsen", "alder": 42, "bosted": "Trondheim", "number_of_children": 1},
    {"fornavn": "Per", "etternavn": "Hansen", "alder": 64, "bosted": "Tromsø", "number_of_children": 3}
]

people = pd.DataFrame(data)

print(people)
```

førenamn etternamn  alder     bustad  number_of_children
0     Ola  Nordmann     17       Oslo                   0
1    Kari  Svendsen     42  Trondheim                   1
2     Per    Hansen     64     Tromsø                   3


Legg merke til at me har importert *pandas* under namnet *pd*, som er ein vanleg praksis. Deretter har me oppretta eit såkalla *DataFrame*-objekt.

I pandas finnes to typar objekt; *DataFrame* og *Series*. Ein *DataFrame* er ein tabell, medan ein *Series* er ein kolonne i tabellen - frå no av skal me halda oss til omgrepa *tabell* og *kolonne*.

La oss henta ein kolonne:


```python
ages = people["alder"]
print(ages)
```

    0    17
    1    42
    2    64
Name: alder, dtype: int64


I pandas bruker me altså skrivemåten `table["column_name"]` for å henta ein bestemd kolonne.

Pandas gir oss mange nyttige funksjonar for tabellar og kolonnar. Eit døme på ein *kolonnefunksjon* er `mean`, som reknar ut gjennomsnittet av alle verdiane:


```python
average_age = ages.mean()
print(average_age)
```

    41.0


**Importera data.** All data som er på tabellform kan setjast inn i ein pandas-tabell. For å lasta inn data frå ein *Excel*-fil, blir følgjande kommando brukt:

```py
table = pd.read_excel("path_to_file.xls", sheet_name="Sheet1")
```
For å lasta inn data frå ein *CSV*-fil, blir funksjonen i staden `read_csv` brukt.

Men kva med sykkeldataa, som er lagra med *JSON*? Me har sett at ei slik fil består av attributt, objekt og lister, som ikkje nødvendigvis kan konverterast til ein tabell.

Sykkeldataa er likevel strukturerte på ein enkel måte:

```json
[
    {
        "started_at": "2023-07-01 01:22:38.878000+00:00",
        "ended_at": "2023-07-01 01:40:04.748000+00:00",
        "duration": 1045,
        "start_station_id": "387",
        "start_station_name": "Studenterlunden",
        "start_station_description": "langs Karl Johan",
        "start_station_latitude": 59.914586,
        "start_station_longitude": 10.735453,
        "end_station_id": "499",
        "end_station_name": "Bjerregaards gate",
        "end_station_description": "ovenfor Fredrikke Qvams gate",
        "end_station_latitude": 59.925488,
        "end_station_longitude": 10.746058
    },
    {
        "started_at": "2023-07-01 03:02:43.726000+00:00",
        "ended_at": "2023-07-01 03:13:45.064000+00:00",
        "duration": 661,
        "start_station_id": "2315",
        "start_station_name": "Rostockgata",
        "start_station_description": "utenfor Bj\u00f8rvika visningssenter",
        "start_station_latitude": 59.90691970255054,
        "start_station_longitude": 10.760311802881915,
        "end_station_id": "410",
        "end_station_name": "Landstads gate",
        "end_station_description": "langs Uelands gate",
        "end_station_latitude": 59.929005,
        "end_station_longitude": 10.7496755
    }
]
```

Me merkar oss at alle turane har dei same datafelta, nemleg *duration*, *end_station_description*, og så vidare. Ved å skriva desse som kolonnar, og kvar sykkeltur som ei rad, får me følgjande tabell:

| started_at                       | ended_at                         | duration | start_station_id | start_station_name | start_station_description       | start_station_latitude | start_station_longitude | end_station_id | end_station_name  | end_station_description      | end_station_latitude | end_station_longitude |
|----------------------------------|----------------------------------|----------|------------------|--------------------|---------------------------------|------------------------|-------------------------|----------------|-------------------|------------------------------|----------------------|-----------------------|
| 2023-07-01 01:22:38.878000+00:00 | 2023-07-01 01:40:04.748000+00:00 | 1045     | 387              | Studenterlunden    | langs Karl Johan                | 59.914586              | 10.735453               | 499            | Bjerregaards gate | ovanfor Fredrikke Qvams gate | 59.925488            | 10.746058             |
| 2023-07-01 03:02:43.726000+00:00 | 2023-07-01 03:13:45.064000+00:00 | 661      | 2315             | Rostockgata        | utanfor Bjørvika visningssenter | 59.90691970255054      | 10.760311802881915      | 410            | Landstads gate    | langs Uelands gate           | 59.929005            | 10.7496755            |

Me kan konkludera med at sykkeldataa kan setjast inn i ein tabell. Korleis gjer me dette?

Som vist i seksjonen *Innhenting og inspeksjon av data*, kan me byrja med å lasta dataa inn i ein dictionary:


```python
url = "https://data.urbansharing.com/oslobysykkel.no/trips/v1/2023/07.json"
page = requests.get(url).text
data = json.loads(page)
```

Når dette er gjort, kan me leggja dadtaene inn i ein tabell, som vist i starten av seksjonen:


```python
trips = pd.DataFrame(data)
trips.head()
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
<th>started_at</th>
<th>ended_at</th>
<th>duration</th>
<th>start_station_id</th>
<th>start_station_name</th>
<th>start_station_description</th>
<th>start_station_latitude</th>
<th>start_station_longitude</th>
<th>end_station_id</th>
<th>end_station_name</th>
<th>end_station_description</th>
<th>end_station_latitude</th>
<th>end_station_longitude</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>2023-07-01 01:22:38.878000+00:00</td>
<td>2023-07-01 01:40:04.748000+00:00</td>
<td>1045</td>
<td>387</td>
<td>Studenterlunden</td>
<td>langs Karl Johan</td>
<td>59.914586</td>
<td>10.735453</td>
<td>499</td>
<td>Bjerregaards gate</td>
<td>ovanfor Fredrikke Qvams gate</td>
<td>59.925488</td>
<td>10.746058</td>
</tr>
<tr>
<th>1</th>
<td>2023-07-01 03:02:43.726000+00:00</td>
<td>2023-07-01 03:13:45.064000+00:00</td>
<td>661</td>
<td>2315</td>
<td>Rostockgata</td>
<td>utanfor Bjørvika visningssenter</td>
<td>59.906920</td>
<td>10.760312</td>
<td>410</td>
<td>Landstads gate</td>
<td>langs Uelands gate</td>
<td>59.929005</td>
<td>10.749676</td>
</tr>
<tr>
<th>2</th>
<td>2023-07-01 03:13:28.322000+00:00</td>
<td>2023-07-01 03:25:26.944000+00:00</td>
<td>718</td>
<td>384</td>
<td>Vår Frelsers gravlund</td>
<td>langs Ullevålsveien</td>
<td>59.919440</td>
<td>10.743765</td>
<td>551</td>
<td>Olaf Ryes plass</td>
<td>langs Sofienberggata</td>
<td>59.922425</td>
<td>10.758182</td>
</tr>
<tr>
<th>3</th>
<td>2023-07-01 03:15:18.482000+00:00</td>
<td>2023-07-01 03:32:54.956000+00:00</td>
<td>1056</td>
<td>584</td>
<td>Henrik Wergelands allé</td>
<td>ved Bogstadveien</td>
<td>59.926894</td>
<td>10.720789</td>
<td>583</td>
<td>Galgeberg</td>
<td>langs St. Halvards gate</td>
<td>59.907076</td>
<td>10.779164</td>
</tr>
<tr>
<th>4</th>
<td>2023-07-01 03:22:07.761000+00:00</td>
<td>2023-07-01 03:25:41.579000+00:00</td>
<td>213</td>
<td>600</td>
<td>Dyvekes bru</td>
<td>ved skatepark</td>
<td>59.905323</td>
<td>10.768958</td>
<td>465</td>
<td>Bjørvika</td>
<td>under brua Nylandsveien</td>
<td>59.909006</td>
<td>10.756180</td>
</tr>
</tbody>
</table>
</div>



Her ser me eit døme på ein nyttig tabellfunksjon, nemleg `head`, som skriv ut dei første radene i tabellen. Me bør alltid gjera dette for å sjekka at tabellen har vorte oppretta rett.

Me kan no henta ut ein kolonne og rekna ut gjennomsnittet av verdiane:


```python
durations = trips["duration"]
print(durations.mean())
```

    873.4412814638342


Så enkelt var det å finna den gjennomsnittlege variheten til sykkelturane!

Vidare kan me trekkja ut sykkelturar som tilfredsstiller eit bestemt krav, til dømes at varigheita er mindre enn 180 sekund (tre minutt):


```python
short_trips = trips[trips["duration"] < 180] 
short_trips.head()
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
<th>started_at</th>
<th>ended_at</th>
<th>duration</th>
<th>start_station_id</th>
<th>start_station_name</th>
<th>start_station_description</th>
<th>start_station_latitude</th>
<th>start_station_longitude</th>
<th>end_station_id</th>
<th>end_station_name</th>
<th>end_station_description</th>
<th>end_station_latitude</th>
<th>end_station_longitude</th>
</tr>
</thead>
<tbody>
<tr>
<th>34</th>
<td>2023-07-01 04:55:13.425000+00:00</td>
<td>2023-07-01 04:56:45.208000+00:00</td>
<td>91</td>
<td>2350</td>
<td>Blindern T-bane</td>
<td>ved Blindernveien</td>
<td>59.940252</td>
<td>10.716724</td>
<td>2350</td>
<td>Blindern T-bane</td>
<td>ved Blindernveien</td>
<td>59.940252</td>
<td>10.716724</td>
</tr>
<tr>
<th>36</th>
<td>2023-07-01 04:57:18.873000+00:00</td>
<td>2023-07-01 04:59:56.660000+00:00</td>
<td>157</td>
<td>442</td>
<td>Vulkan</td>
<td>ved Maridalsveien</td>
<td>59.922510</td>
<td>10.751010</td>
<td>463</td>
<td>Schous plass trikkestopp</td>
<td>ved biblioteket</td>
<td>59.920728</td>
<td>10.759486</td>
</tr>
<tr>
<th>56</th>
<td>2023-07-01 05:30:20.792000+00:00</td>
<td>2023-07-01 05:32:35.367000+00:00</td>
<td>134</td>
<td>584</td>
<td>Henrik Wergelands allé</td>
<td>ved Bogstadveien</td>
<td>59.926894</td>
<td>10.720789</td>
<td>579</td>
<td>Bogstadveien</td>
<td>ved Sporveisgata</td>
<td>59.924732</td>
<td>10.724628</td>
</tr>
<tr>
<th>65</th>
<td>2023-07-01 05:41:52.369000+00:00</td>
<td>2023-07-01 05:43:44.970000+00:00</td>
<td>112</td>
<td>600</td>
<td>Dyvekes bru</td>
<td>ved skatepark</td>
<td>59.905323</td>
<td>10.768958</td>
<td>737</td>
<td>Munkegata</td>
<td>langs Oslo gate</td>
<td>59.908255</td>
<td>10.767800</td>
</tr>
<tr>
<th>71</th>
<td>2023-07-01 05:47:06.312000+00:00</td>
<td>2023-07-01 05:50:00.209000+00:00</td>
<td>173</td>
<td>737</td>
<td>Munkegata</td>
<td>langs Oslo gate</td>
<td>59.908255</td>
<td>10.767800</td>
<td>600</td>
<td>Dyvekes bru</td>
<td>ved skatepark</td>
<td>59.905323</td>
<td>10.768958</td>
</tr>
</tbody>
</table>
</div>



Som forventa får me ein ny tabell med radene som tilfredsstiller kravet. Men korleis gjorde me eigentleg dette? Kva betyr det å skriva `trips[trips["duration"] < 180]`?

Me er jo vant til å bruka indeksar, som til dømes `trips[:10]` for å henta dei ti første turane. Men sidan me no jobbar med ein pandas-tabell, har me fleire moglegheiter - i staden for indeksar kan me skriva eit vilkår! I dette tilfellet er vilkåret at kolonnen *duration* har ein talverdi som er mindre enn 180. Då vil *pandas* sørgja for å henta ut alle radene der vilkåret stemmer!

**Oppsummering.** I denne seksjonen har me sett at pandas gir oss høvet til å jobba med to typar objekt; tabellar og kolonnar. Me har sett korleis tabellar i nokre tilfelle kan opprettast frå *JSON*-filer. Vidare har me sett korleis me hentar spesifikke kolonnar frå ein tabell, og dessutan henta rrader som tilfredsstiller eit vilkår.

