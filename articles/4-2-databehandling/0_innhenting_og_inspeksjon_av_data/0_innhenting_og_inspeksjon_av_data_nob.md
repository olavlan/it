---
title: "Innhenting og inspeksjon av data"
belongs_to_chain: "Databehandling"
figures_to_include:
---

I disse seksjonene skal vi bruke turdata fra [*Oslo bysykkel*](https://oslobysykkel.no/apne-data/historisk) - mer spesifikt skal vi importere *JSON*-filen for Juni 2023. Vi trenger ikke å laste ned filen manuelt, men kan i stedet kopiere nettadressen til filen:

[*https://data.urbansharing.com/oslobysykkel.no/trips/v1/2023/07.json*](https://data.urbansharing.com/oslobysykkel.no/trips/v1/2023/07.json)

Python-pakken `requests` kan brukes til å hente innholdet i filen:


```python
import requests

url = "https://data.urbansharing.com/oslobysykkel.no/trips/v1/2023/07.json"
page_content = requests.get(url).text

print(page_content[0:1000])
```

    [{"started_at": "2023-07-01 01:22:38.878000+00:00", "ended_at": "2023-07-01 01:40:04.748000+00:00", "duration": 1045, "start_station_id": "387", "start_station_name": "Studenterlunden", "start_station_description": "langs Karl Johan", "start_station_latitude": 59.914586, "start_station_longitude": 10.735453, "end_station_id": "499", "end_station_name": "Bjerregaards gate", "end_station_description": "ovenfor Fredrikke Qvams gate", "end_station_latitude": 59.925488, "end_station_longitude": 10.746058}, {"started_at": "2023-07-01 03:02:43.726000+00:00", "ended_at": "2023-07-01 03:13:45.064000+00:00", "duration": 661, "start_station_id": "2315", "start_station_name": "Rostockgata", "start_station_description": "utenfor Bj\u00f8rvika visningssenter", "start_station_latitude": 59.90691970255054, "start_station_longitude": 10.760311802881915, "end_station_id": "410", "end_station_name": "Landstads gate", "end_station_description": "langs Uelands gate", "end_station_latitude": 59.929005, "end


Siden vi har hentet filinnholdet som en tekststreng, er neste steg å oversette den til en dictionary:


```python
import json

trips = json.loads(page_content)

print(type(trips))
```

    <class 'list'>


Her ser vi at variabelen `trips` er en Python-liste. Det er fordi *Oslo Bysykkel* har lagret dataene som en liste av objekter, der hvert objekt svarer til en sykkeltur. Som eksempel kan vi skrive ut det første elementet i lista:  


```python
first = trips[0]

print(type(first))
print(first)
```

    <class 'dict'>
    {'started_at': '2023-07-01 01:22:38.878000+00:00', 'ended_at': '2023-07-01 01:40:04.748000+00:00', 'duration': 1045, 'start_station_id': '387', 'start_station_name': 'Studenterlunden', 'start_station_description': 'langs Karl Johan', 'start_station_latitude': 59.914586, 'start_station_longitude': 10.735453, 'end_station_id': '499', 'end_station_name': 'Bjerregaards gate', 'end_station_description': 'ovenfor Fredrikke Qvams gate', 'end_station_latitude': 59.925488, 'end_station_longitude': 10.746058}


Hvert element i lista er altså en dictionary. La oss prøve å skrive ut de to første elementene med penere formatering:


```python
two_first = trips[:2]
print(json.dumps(two_first, indent=4))
```

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


Her ser vi tydelig hvordan dataene er organisert. Dersom vi er usikre på hva de ulike nøklene betyr, kan vi lese [dokumentasjonen](https://oslobysykkel.no/apne-data/historisk) (gå lengre ned på siden). 

Merk at alle dataene er skrevet som tall og tekststrenger. Noen av disse er skrevet i henhold til bestemte standarder, som vi nå skal se.

**Tidspunkt.** Start -og sluttidspunkt er skrevet i et standard datoformat ([ISO](https://en.wikipedia.org/wiki/ISO_8601)):

```
yyyy-MM-dd hh:mm:SS.ssssssZ
```
I dette formatet listes tidsenhetene fra størst til minst: 

| år   | måned | dag | time | minutt | sekund | mikrosekund | tidssone |
|------|-------|-----|------|--------|--------|-------------|----------|
| yyyy | MM    | dd  | hh   | mm     | SS     | ss          | Z        |

Merk at tidssonen angis til slutt. I dataene fra *Oslo bysykkel* benyttes tidssonen *+00:00*, som er *London*-tid. Dersom vi ønsker tidspunktene i norsk tid, må én time legges til.

**Varighet.** Varighet er angitt i antall sekunder. Dersom vi ønsker antall minutter og sekunder, må verdiene konverteres. 

**Posisjon.** Geografisk posisjon er angitt i henhold til standarden [WGS](https://no.wikipedia.org/wiki/World_Geodetic_System), som er koordinatsystem for jordas overflate. I eksempelet ovenfor finner vi følgende koordinater:

Startstasjon: *59.91944043984847, 10.7437646218726*   
Endestasjon: *59.922425, 10.758182*

Forsøk å lime *59.922425, 10.758182* inn i søkefeltet på [*Google Maps*](https://www.google.no/maps) for å se den eksakte posisjonen! For å gå motsatt vei kan du høyreklikke på et punkt i *Google Maps* - da vil koordinatene til punktet vises øverst i verktøylisten (trykk for å kopiere til utklippstavlen).

**Stasjoner.** Vi merker oss at en stasjon (start -eller endestasjon) er registrert med fem forskjellige verdier: *id*, *name*, *description*, *latitude*, *longitude*. En stasjon er for eksempel:

```
"id": "551",
"name": "Olaf Ryes plass",
"description": "langs Sofienberggata",
"latitude": 59.922425,
"longitude": 10.758182
```

Det kan være nyttig å opprette en dictionary som kun inneholder stasjonene, slik at vi raskt kan slå opp på en bestemt stasjon. Vi ønsker altså en dictionary på formen: 

```json
{
    "551": {
        "name": "Olaf Ryes plass",
        "description": "langs Sofienberggata",
        "latitude": 59.922425,
        "longitude": 10.758182  
    },
    "384": {
        "name": "V\u00e5r Frelsers gravlund",
        "description": "langs Ullev\u00e5lsveien",
        "latitude": 59.91944043984847,
        "longitude": 10.7437646218726   
    },
    ...
}
```

Merk at vi bruker id'ene til stasjonene som nøkler. For å lage en slik dictionary, kan vi gå gjennom alle turer, og stoppe opp hver gang vi kommer til en stasjon vi enda ikke har registrert: 


```python
stations = {}
for t in trips: 
    for s in ["start", "end"]:
        id = t[f"{s}_station_id"]
        if id not in stations:
            new_station = {
                "name": t[f"{s}_station_name"],
                "description": t[f"{s}_station_description"],
                "latitude": t[f"{s}_station_latitude"],
                "longitude": t[f"{s}_station_longitude"]
            }
            stations[id] = new_station
```

For å hente mer informasjon om stasjonen med id *2358*, slår vi enkelt opp i den nye variabelen `stations`: 


```python
print(stations["2358"])
```

    {'name': 'Aker Brygge 3 mot Fergene', 'description': 'ved bryggen', 'latitude': 59.91087115068967, 'longitude': 10.729828757277915, 'distance_to_oslo_s': 1.1572389016534543}


Hvordan kan vi gå gjennom alle stasjoner? Det er ikke mulig å skrive `for s in stations`, fordi `stations` er en dictionary (som ikke er itererbar). I stedet kan vi hente alle nøklene i `stations`:


```python
print(stations.keys())
```

    dict_keys(['387', '499', '2315', '410', '384', '551', '584', '583', '600', '465', '408', '625', '593', '523', '518', '462', '412', '443', '603', '572', '563', '481', '2333', '619', '508', '597', '478', '2339', '2328', '444', '437', '392', '608', '446', '2305', '456', '425', '460', '489', '428', '576', '534', '2340', '421', '448', '382', '479', '578', '623', '436', '742', '480', '2350', '496', '442', '463', '621', '570', '577', '617', '531', '737', '403', '611', '569', '512', '485', '416', '400', '449', '404', '580', '529', '397', '2307', '620', '579', '502', '517', '535', '599', '2309', '383', '470', '519', '748', '447', '475', '450', '406', '2308', '503', '513', '484', '735', '549', '457', '627', '424', '435', '440', '396', '415', '388', '537', '2358', '507', '455', '2357', '626', '500', '525', '596', '744', '540', '581', '495', '550', '616', '469', '521', '2334', '393', '524', '426', '417', '1009', '398', '738', '614', '407', '491', '427', '558', '1023', '453', '545', '381', '493', '514', '2347', '433', '552', '787', '970', '594', '377', '2270', '390', '468', '486', '586', '2332', '589', '414', '516', '561', '574', '530', '568', '607', '567', '547', '418', '395', '413', '564', '464', '405', '590', '430', '1755', '615', '1919', '441', '575', '399', '571', '401', '445', '506', '548', '609', '402', '624', '461', '497', '378', '618', '423', '511', '2337', '431', '2351', '746', '2349', '389', '588', '582', '554', '542', '452', '522', '509', '487', '459', '473', '505', '585', '610', '622', '451', '587', '541', '598', '422', '592', '566', '562', '526', '380', '429', '488', '458', '434', '411', '483', '476', '474', '438', '1101', '560', '555', '543', '2330', '573', '2304', '454', '394', '472', '739', '482', '595', '565', '2329', '2306', '556', '409', '432', '532', '559', '601', '533', '471', '501', '2280', '420', '498', '439', '591', '466', '527', '2355', '613', '3725', '612'])


Nå kan vi gå gjennom alle nøklene, og på den måten gå gjennom alle stasjoner! La oss lage en løkke som teller antall stasjoner:


```python
i = 0
for id in stations.keys():
    s = stations[id]
    i += 1

print(i)
```

    266


Fra dette kan vi konkludere med at 266 forskjellige stasjoner ble brukt i Juni 2023!

**Oppsummering.** I denne seksjonen har vi hentet data fra *Oslo Bysykkel* og lagt dem i variabelen `trips`. Dataene er strukturert som en liste av turer. Hver tur er lagret som en dictionary, og verdiene følger bestemte standarder.

Videre har trukket ut informasjon om alle stasjoner og lagt dem i variabelen `stations`. Dette er en dictionary der stasjons-id brukes som nøkkel.

**Aktivitetsforslag 1.** Opprett variablene `trips` og `stations` som vist i denne seksjonen. Du kan velge selv hvilken måned du vil hente fra [*Oslo bysykkel*](https://oslobysykkel.no/apne-data/historisk).

Bruk løkker, indekser og nøkler til å skrive ut følgende inforasjon: 

- Skriv ut en liste over alle stasjoner, på formen *navn,  beskrivelse*:
```
Olaf Ryes plass, langs Sofienberggate
Vår Frelsers gravlund, langs Ullevålsveien
...
```
- Skriv ut informasjon om de 50 første turene, på følgende form:
```

Tur 1:
Fra: Studenterlunden
Til: Bjerregaards gate
Varighet: 1045 sekunder

Tur 2:
Fra: Rostockgata
Til: Landstads gate
Varighet: 661 sekunder

Tur 3:
Fra: Vår Frelsers gravlund
Til: Olaf Ryes plass
Varighet: 718 sekunder

...
```

* Utfordring: Skriv ut varighet som antall minutter og sekunder.

**Aktivitetsforslag 2.** Bruk programmering til å finne ut følgende om sykkeldataene: 

1. Hvor mange turer startet og endte på samme stasjon? Hvor stor prosentandel utgjør dette?
2. Hvor mange turer varte kortere enn fem minutter (300 sekunder)? Hvor stor prosentandel utgjør dette? Hva med turer som varte lengre enn én time (3600 sekunder)?
3. Finnes det turer som varte kortere enn 20 sekunder? Skriv ut informasjon om disse turene.
4. Finn sykkelturene som varte kortest og lengst.  Skriv ut informasjon om disse sykkelturene. *Hint: For å finne største verdi i en liste, trenger vi en variabel som oppdateres hver gang vi oppdager et nytt tall som er større enn det hittil største. Tilsvarende metode brukes for å finne minste verdi.* 

**Aktivitetsforslag 3.** 

1. Hvordan kan vi regne ut hva som er gjennomsnittlig varighet til en sykkeltur? 
2. Bruk programmering til å regne ut den gjennomsnittlige varigheten til en sykkeltur.
4. Utfordring: Hva er den gjennomsnittlige varigheten for sykkelturer som startet og endte på samme stasjon.  
  
*Hint: Den grunnleggende formelen er å summere varigheten til alle sykkelturene, og deretter dele på antall turer.* 

