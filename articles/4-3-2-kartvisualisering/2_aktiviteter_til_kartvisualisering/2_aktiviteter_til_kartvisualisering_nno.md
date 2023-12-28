---
title: "Aktivitetar til kartvisualisering"
figures_to_include:
	- "blindern.png"
---

**Aktivitetsforslag 1.**
* Lag ein tabell som berre inneheld turar som skjedde på helgar. Vis eit kart med dei mest populære endestasjonane i helgar. Forsøk også med berre søndagsturar. *Hint: sjå seksjonen* Introduksjon til pandas *for bruk av vilkår.*
* Vis eit kart med dei mest populære startstasjonane for kveldsturar (turar som starta mellom 18 og 24). Kva med turar som starta på natta (mellom 0 og 6)? *Hint: du treng ein kolonne som indikerer kva periode på dagen ein tur starta, og deretter laga ein tabell som inneheld dei rette turane.*

**Aktivitetsforslag 2.** I denne oppgåva skal me prøva å finna ut kvar folk reiser frå når dei syklar til *Universitetet i Oslo*. Me avgrensar først universitetsområdet:

<img src="/media/markdowncontent/assosiated_files/blindern.png" width="300">

Her har me brukt [stasjonsoversikta](https://oslobysykkel.no/stasjoner) og [*geojson.io*](https://geojson.io/#map=14.18/59.94056/10.72249) til å teikna eit område som dekkjer dei relevante stasjonane. Ifølgje *geojson.io* har dette området følgjande hjørnekoordinatar:

```
(10.721463545002223, 59.93721185255322)   
(10.728019630851009, 59.94123625428736)      
(10.722107784652138, 59.944159334211946)     
(10.717294935502565, 59.93969868675066)
```

1. Definer eit polygon i Python som svarer til området ovanfor (sjå seksjonen *Geografiske område*).
2. Opprett kolonnen *ends_in_university_area* i tabellen `trips`. Denne kolonnen skal innehalda *yes* for sykkelturar som sluttar i universitetsområdet, og elles *no*.
* *Hint 1: Lag først ein funksjon som konverterer ei enkelt rad til rett svar. Bruk seksjonen* Tabellfunksjoner *til hjelp.*
* *Hint 2: I funksjonen må du oppretta eit punkt og sjekka om det er innanfor universitetsområdet. Bruk seksjonen* Geografiske område *til hjelp*.
4. Opprett ein ny tabell med alle turar som endar i universitetsområdet. *Hint: bruk eit vilkår med kolonnen du oppretta i førre punkt. Sjå seksjonen* Introduksjon til pandas *for hjelp.*
5. Bruk kartvisualisering til å visa dei mest populære startstasjonane frå tabellen du oppretta. Kommenter resultatet.

**Aktivitetsforslag 3.** I denne oppgåva skal me dela inn sykkelturane i to grupper; transportturar (til dømes til og frå jobb) og rekreasjonsturar (til dømes besøk av attraksjonar). Me har ikkje nok informasjon til å vita om ein tur fell i den eine eller andre gruppa, men me kan gjera nokre antakingar med dataa me har tilgjengeleg.

Ei slik antaking er at ein tur som varer meir enn éin time (3600 sekund) er ein rekreasjonstur.

1. Opprett ein ny tabell med rekreasjonturer, det vil seia turar som varer meir enn éin time.
2. Visualiser på eit kart kva som er dei mest populære startstasjonane for rekreasjonsturar. Visualiser også dei mest populære endestasjonane.
3. Trur du resultatet fortel noko om kva attraksjonar i Oslo som er mest populære (blant brukarar av *Oslo Bysykkel*)?

Ei anna antaking er at turar som startar og sluttar på same stasjon er ein rekreasjonstur.

3. Opprett ein tabell med alle turar som starta og slutta på same punkt og visualiser dei mest populære stasjonane i tabellen. Kommenter resultatet.

**Aktivitetsforslag 4.** I denne oppgåva skal me gruppera sykkelturane etter kva stasjon dei enda på. Deretter skal me samanlikna dei ulike gruppene med omsyn til avstand og varigheit på sykkelturane, og dessutan forhold mellom avstand og varigheit.

Me byrjar først med å finna gjennomsnittleg varigheit for sykkelturane, gruppert etter endestasjon:


```python
grouped = trips.groupby("end_station_id")
means = grouped["duration"].mean()

print(means)
```

end_station_id
    1009    1259.064000
    1023     843.815476
    1101     983.459677
    1755     960.944899
    1919     710.907895
               ...     
    744      765.311295
    746     1179.498069
    748      871.735294
    787      882.350254
    970      684.696742
Name: duration, Length: 266, dtype: float64


Kolonnen ovanfor har stasjons-id som indeksar, akkurat som stasjonstabellen. Det betyr at kolonnen kan setjast inn i stasjonstabellen:


```python
stations["average_time_to_arrive"] = means
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
<th>used_as_end</th>
<th>average_time_to_arrive</th>
</tr>
<tr>
<th>id</th>
<th></th>
<th></th>
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
<td>462</td>
<td>1024.896104</td>
</tr>
<tr>
<th>2315</th>
<td>Rostockgata</td>
<td>utanfor Bjørvika visningssenter</td>
<td>59.906920</td>
<td>10.760312</td>
<td>1005</td>
<td>1066</td>
<td>902.244841</td>
</tr>
<tr>
<th>384</th>
<td>Vår Frelsers gravlund</td>
<td>langs Ullevålsveien</td>
<td>59.919440</td>
<td>10.743765</td>
<td>887</td>
<td>876</td>
<td>816.297945</td>
</tr>
<tr>
<th>584</th>
<td>Henrik Wergelands allé</td>
<td>ved Bogstadveien</td>
<td>59.926894</td>
<td>10.720789</td>
<td>723</td>
<td>579</td>
<td>868.561313</td>
</tr>
<tr>
<th>600</th>
<td>Dyvekes bru</td>
<td>ved skatepark</td>
<td>59.905323</td>
<td>10.768958</td>
<td>598</td>
<td>596</td>
<td>913.263423</td>
</tr>
</tbody>
</table>
</div>



Oppgåver:
1. Vis sykkelstasjonane på eit kart, og sørg for at den nye kolonnen *average_time_to_arrive* bestemmer storleiken på sirklane. Er det nokon stasjonar som har spesielt stor sirkel? I så fall, kva trur du er årsaka?
1. Gjenta prosessen ovanfor, men visualiser i staden avstand, det vil seia gjennomsnittleg avstand syklistar reiser frå for å komma seg til kvar stasjon. Kommenter resultatet.

Med følgjande kode kan me oppretta ein ny kolonne i turtabellen, som inneheld forholdet mellom avstand og varigheit, det vil seia ein slags "gjennomsnittleg fart" for turen:


```python
trips["speed"] = trips["distance"]/trips["duration"]
```

*Å kombinera to kolonnar på denne måten fungerer når me bruker enkle matematiske formlar. Dersom me ønskjer å gjera meir kompliserte operasjonar, må me bruka `apply`, som beskrive i seksjonen* Tabellfunksjoner.

3. Gjenta prosessen frå punkt 1, men visualiser i staden "gjennomsnittleg fart" for å komma seg til kvar stasjon. Viss det er nokon stasjonar som har spesielt høg eller låg verdi, kvifor trur du dette er tilfelle?
