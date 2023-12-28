---
title: "Aktiviteter til kartvisualisering"
figures_to_include:
	- "blindern.png"
---

**Aktivitetsforslag 1.** 
* Lag en tabell som kun inneholder turer som skjedde på helger. Vis et kart med de mest populære endestasjonene i helger. Forsøk også med kun søndagsturer. *Hint: se seksjonen* Introduksjon til pandas *for bruk av betingelser.* 
* Vis et kart med de mest populære startstasjonene for kveldsturer (turer som startet mellom 18 og 24). Hva med turer som startet på natta (mellom 0 og 6)? *Hint: du trenger en kolonne som indikerer hvilken periode på dagen en tur startet, og deretter lage en tabell som inneholder de riktige turene.*

**Aktivitetsforslag 2.** I denne oppgaven skal vi prøve å finne ut hvor folk reiser fra når de sykler til *Universitetet i Oslo*. Vi avgrenser først universitetsområdet: 

<img src="/media/markdowncontent/assosiated_files/blindern.png" width="300">

Her har vi brukt [stasjonsoversikten](https://oslobysykkel.no/stasjoner) og [*geojson.io*](https://geojson.io/#map=14.18/59.94056/10.72249) til å tegne et område som dekker de relevante stasjonene. Ifølge *geojson.io* har dette området følgende hjørnekoordinater: 

```
(10.721463545002223, 59.93721185255322)   
(10.728019630851009, 59.94123625428736)      
(10.722107784652138, 59.944159334211946)     
(10.717294935502565, 59.93969868675066)
```

1. Definer et polygon i Python som svarer til området ovenfor (se seksjonen *Geografiske områder*).
2. Opprett kolonnen *ends_in_university_area* i tabellen `trips`. Denne kolonnen skal inneholde *yes* for sykkelturer som slutter i universitetsområdet, og ellers *no*.
* *Hint 1: Lag først en funksjon som konverterer en enkelt rad til riktig svar. Bruk seksjonen* Tabellfunksjoner *til hjelp.*   
* *Hint 2: I funksjonen må du opprette et punkt og sjekke om det er innenfor universitetsområdet. Bruk seksjonen* Geografiske områder *til hjelp*.  
4. Opprett en ny tabell med alle turer som ender i universitetsområdet. *Hint: bruk en betingelse med kolonnen du opprettet i forrige punkt. Se seksjonen* Introduksjon til pandas *for hjelp.*
5. Bruk kartvisualisering til å vise de mest populære startstasjonene fra tabellen du opprettet. Kommenter resultatet. 

**Aktivitetsforslag 3.** I denne oppgaven skal vi dele inn sykkelturene i to grupper; transportturer (for eksempel til og fra jobb) og rekreasjonsturer (for eksempel besøk av attraksjoner). Vi har ikke nok informasjon til å vite om en tur faller i den ene eller andre gruppen, men vi kan gjøre noen antagelser med dataene vi har tilgjengelig. 

En slik antagelse er at en tur som varer mer enn én time (3600 sekunder) er en rekreasjonstur.

1. Opprett en ny tabell med rekreasjonturer, det vil si turer som varer mer enn én time.
2. Visualiser på et kart hva som er de mest populære startstasjonene for rekreasjonsturer. Visualiser også de mest populære endestasjonene.
3. Tror du resultatet forteller noe om hvilke attraksjoner i Oslo som er mest populære (blant brukere av *Oslo Bysykkel*)?

En annen antagelse er at turer som starter og slutter på samme stasjon er en rekreasjonstur. 

3. Opprett en tabell med alle turer som startet og sluttet på samme punkt og visualiser de mest populære stasjonene i tabellen. Kommenter resultatet.

**Aktivitetsforslag 4.** I denne oppgaven skal vi gruppere sykkelturene etter hvilken stasjon de endte på. Deretter skal vi sammenligne de ulike gruppene med hensyn på avstand og varighet på sykkelturene, samt forhold mellom avstand og varighet. 

Vi begynner først med å finne gjennomsnittlig varighet for sykkelturene, gruppert etter endestasjon: 


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


Kolonnen ovenfor har stasjons-id som indekser, akkurat som stasjonstabellen. Det betyr at kolonnen kan settes inn i stasjonstabellen:


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
      <td>utenfor Bjørvika visningssenter</td>
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



Oppgaver:  
1. Vis sykkelstasjonene på et kart, og sørg for at den nye kolonnen *average_time_to_arrive* bestemmer størrelsen på sirklene. Er det noen stasjoner som har spesielt stor sirkel? I så fall, hva tror du er årsaken?
1. Gjenta prosessen ovenfor, men visualiser i stedet avstand, det vil si gjennomsnittlig avstand syklister reiser fra for å komme seg til hver stasjon. Kommenter resultatet.

Med følgende kode kan vi opprette en ny kolonne i turtabellen, som inneholder forholdet mellom avstand og varighet, det vil si en slags "gjennomsnittlig hastighet" for turen: 


```python
trips["speed"] = trips["distance"]/trips["duration"]
```

*Å kombinere to kolonner på denne måten fungerer når vi bruker enkle matematiske formler. Dersom vi ønsker å gjøre mer kompliserte operasjoner, må vi bruke `apply`, som beskrevet i seksjonen* Tabellfunksjoner.

3. Gjenta prosessen fra punkt 1, men visualiser i stedet "gjennomsnittlig hastighet" for å komme seg til hver stasjon. Hvis det er noen stasjoner som har spesielt høy eller lav verdi, hvorfor tror du dette er tilfelle? 
