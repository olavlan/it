---
title: "Innhenting og inspeksjon av data"
belongs_to_chain: "Databehandling"
figures_to_include:
---

I desse seksjonane skal me bruka turdata frå [*Oslo bysykkel*](https://oslobysykkel.no/apne-data/historisk) - meir spesifikt skal me importera *JSON*-fila for Juni 2023. Me treng ikkje å lasta ned fila manuelt, men kan i staden kopiera nettadressen til fila:

[*https://data.urbansharing.com/oslobysykkel.no/trips/v1/2023/07.json*](https://data.urbansharing.com/oslobysykkel.no/trips/v1/2023/07.json)

Python-pakken `requests` kan brukast til å henta innhaldet i fila:


```python
import requests

url = "https://data.urbansharing.com/oslobysykkel.no/trips/v1/2023/07.json"
page_content = requests.get(url).text

print(page_content[0:1000])
```

[{"started_at": "2023-07-01 01:22:38.878000+00:00", "ended_at": "2023-07-01 01:40:04.748000+00:00", "duration": 1045, "start_station_id": "387", "start_station_name": "Studenterlunden", "start_station_description": "langs Karl Johan", "start_station_latitude": 59.914586, "start_station_longitude": 10.735453, "end_station_id": "499", "end_station_name": "Bjerregaards gate", "end_station_description": "ovanfor Fredrikke Qvams gate", "end_station_latitude": 59.925488, "end_station_longitude": 10.746058}, {"started_at": "2023-07-01 03:02:43.726000+00:00", "ended_at": "2023-07-01 03:13:45.064000+00:00", "duration": 661, "start_station_id": "2315", "start_station_name": "Rostockgata", "start_station_description": "utanfor Bj\u00f8rvika visningssenter", "start_station_latitude": 59.90691970255054, "start_station_longitude": 10.760311802881915, "end_station_id": "410", "end_station_name": "Landstads gate", "end_station_description": "langs Uelands gate", "end_station_latitude": 59.929005, "end


Sidan me har henta filinnhaldet som ein tekststreng, er neste steg å omsetja han til ein dictionary:


```python
import json

trips = json.loads(page_content)

print(type(trips))
```

<class 'list'>


Her ser me at variabelen `trips` er ei Python-liste. Det er fordi *Oslo Bysykkel* har lagra dataa som ei liste av objekt, der kvart objekt svarer til ein sykkeltur. Som døme kan me skriva ut det første elementet i lista:


```python
first = trips[0]

print(type(first))
print(first)
```

<class 'dict'>
{'started_at': '2023-07-01 01:22:38.878000+00:00', 'ended_at': '2023-07-01 01:40:04.748000+00:00', 'duration': 1045, 'start_station_id': '387', 'start_station_name': 'Studenterlunden', 'start_station_description': 'langs Karl Johan', 'start_station_latitude': 59.914586, 'start_station_longitude': 10.735453, 'end_station_id': '499', 'end_station_name': 'Bjerregaards gate', 'end_station_description': 'ovanfor Fredrikke Qvams gate', 'end_station_latitude': 59.925488, 'end_station_longitude': 10.746058}


Kvart element i lista er altså ein dictionary. La oss prøva å skriva ut dei to første elementa med finare formatering:


```python
two_first = trips[:2]
print(json.dumps(two_first, indent=4))
```

    [
        {
"started_at": "2023-07-01 01:22:38.878000+00:00",
"ended_at": "2023-07-01 01:40:04.748000+00:00",
"duration": 1045
"start_station_id": "387",
"start_station_name": "Studenterlunden",
"start_station_description": "langs Karl Johan",
"start_station_latitude": 59.914586
"start_station_longitude": 10.735453
"end_station_id": "499",
"end_station_name": "Bjerregaards gate",
"end_station_description": "ovanfor Fredrikke Qvams gate",
"end_station_latitude": 59.925488
"end_station_longitude": 10.746058
        },
        {
"started_at": "2023-07-01 03:02:43.726000+00:00",
"ended_at": "2023-07-01 03:13:45.064000+00:00",
"duration": 661
"start_station_id": "2315",
"start_station_name": "Rostockgata",
"start_station_description": "utanfor Bj\u00f8rvika visningssenter",
"start_station_latitude": 59.90691970255054
"start_station_longitude": 10.760311802881915
"end_station_id": "410",
"end_station_name": "Landstads gate",
"end_station_description": "langs Uelands gate",
"end_station_latitude": 59.929005
"end_station_longitude": 10.7496755
        }
    ]


Her ser me tydeleg korleis dataa er organisert. Dersom me er usikre på kva dei ulike nøklane betyr, kan me lesa [dokumentasjonen](https://oslobysykkel.no/apne-data/historisk) (gå lengre ned på sidan).

Merk at alle dataa er skrivne som tal og tekststrenger. Nokre av desse er skrivne i samsvar med bestemde standardar, som me no skal sjå.

**Tidspunkt.** Start -og sluttidpunkt er skrive i eit standard datoformat ([ISO](https://en.wikipedia.org/wiki/iso_8601)):

```
yyyy-MM-dd hh:mm:SS.ssssssZ
```
I dette formatet blir tidseiningane lista frå størst til minst:

| år   | månad | dag | time | minutt | sekund | mikrosekund | tidssone |
|------|-------|-----|------|--------|--------|-------------|----------|
| yyyy | MM    | dd  | hh   | mm     | SS     | ms          | Z        |

Merk at tidssona blir angitt til slutt. I dataa frå *Oslo bysykkel* blir nytta tidssona *+00:00*, som er *London*-tid. Dersom me ønskjer tidspunkta i norsk tid, må éin time leggjast til.

**Varigheit.** Varigheit er angitt i talet på sekund. Dersom me ønskjer talet på minutt og sekund, må verdiane konverterast.

**Posisjon.** Geografisk posisjon er angitt i samsvar med standarden [WGS](https://no.wikipedia.org/wiki/world_geodetic_system), som er koordinatsystem for jordoverflata. I dømet ovanfor finnar me følgjande koordinatar:

Startstasjon: *59.91944043984847, 10.7437646218726*
Endestasjon: *59.922425, 10.758182*

Prøv å lima *59.922425, 10.758182* inn i søkjefeltet på [*Google Maps*](https://www.google.no/maps) for å sjå den eksakte posisjonen! For å gå motsett veg kan du høyreklikke på eit punkt i *Google Maps* - då vil koordinatane til punktet visast øvst i verktøylista (trykk for å kopiera til utklippstavla).

**Stasjonar.** Me merkar oss at ein stasjon (start -eller endestasjon) er registrert med fem ulike verdiar: *id*, *name*, *description*, *latitude*, *longitude*. Ein stasjon er til dømes:

```
"id": "551",
"name": "Olaf Ryes plass",
"description": "langs Sofienberggata",
"latitude": 59.922425,
"longitude": 10.758182
```

Det kan vera nyttig å oppretta ein dictionary som berre inneheld stasjonane, slik at me raskt kan slå opp på ein bestemd stasjon. Me ønskjer altså ein dictionary på forma:

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

Merk at me bruker id-ane til stasjonane som nøklar. For å laga ein slik dictionary, kan me gå gjennom alle turar, og stoppa opp kvar gong me kjem til ein stasjon me endå ikkje har registrert:


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

For å henta meir informasjon om stasjonen med id *2358*, slår me enkelt opp i den nye variabelen `stations`:


```python
print(stations["2358"])
```

{'name': 'Aker Brygge 3 mot Fergene', 'description': 'ved bryggja', 'latitude': 59.91087115068967, 'longitude': 10.729828757277915, 'distance_to_oslo_s': 1.1572389016534543}


Korleis kan me gå gjennom alle stasjonar? Det er ikkje mogleg å skriva `for s in stations`, fordi `stations` er ein dictionary (som ikkje er itererbar). I staden kan me henta alle nøklane i `stations`:


```python
print(stations.keys())
```

dict_keys(['387', '499', '2315', '410', '384', '551', '584', '583', '600', '465', '408', '625', '593', '523', '518', '462', '412', '443', '603', '572', '563', '481', '2333', '619', '508', '597', '478', '2339', '2328', '444', '437', '392', '608', '446', '2305', '456', '425', '460', '489', '428', '576', '534', '2340', '421', '448', '382', '479', '578', '623', '436', '742', '480', '2350', '496', '442', '463', '621', '570', '577', '617', '531', '737', '403', '611', '569', '512', '485', '416', '400', '449', '404', '580', '529', '397', '2307', '620', '579', '502', '517', '535', '599', '2309', '383', '470', '519', '748', '447', '475', '450', '406', '2308', '503', '513', '484', '735', '549', '457', '627', '424', '435', '440', '396', '415', '388', '537', '2358', '507', '455', '2357', '626', '500', '525', '596', '744', '540', '581', '495', '550', '616', '469', '521', '2334', '393', '524', '426', '417', '1009', '398', '738', '614', '407', '491', '427', '558', '1023', '453', '545', '381', '493', '514', '2347', '433', '552', '787', '970', '594', '377', '2270', '390', '468', '486', '586', '2332', '589', '414', '516', '561', '574', '530', '568', '607', '567', '547', '418', '395', '413', '564', '464', '405', '590', '430', '1755', '615', '1919', '441', '575', '399', '571', '401', '445', '506', '548', '609', '402', '624', '461', '497', '378', '618', '423', '511', '2337', '431', '2351', '746', '2349', '389', '588', '582', '554', '542', '452', '522', '509', '487', '459', '473', '505', '585', '610', '622', '451', '587', '541', '598', '422', '592', '566', '562', '526', '380', '429', '488', '458', '434', '411', '483', '476', '474', '438', '1101', '560', '555', '543', '2330', '573', '2304', '454', '394', '472', '739', '482', '595', '565', '2329', '2306', '556', '409', '432', '532', '559', '601', '533', '471', '501', '2280', '420', '498', '439', '591', '466', '527', '2355', '613', '3725', '612'])


No kan me gå gjennom alle nøklane, og på den måten gå gjennom alle stasjonar! La oss laga ei løkke som tel talet på stasjonar:


```python
i = 0
for id in stations.keys():
    s = stations[id]
    i += 1

print(i)
```

    266


Frå dette kan me konkludera med at 266 ulike stasjonar vart brukte i Juni 2023!

**Oppsummering.** I denne seksjonen har me henta data frå *Oslo Bysykkel* og lagt dei i variabelen `trips`. Dataa er strukturerte som ei liste av turar. Kvar tur er lagra som ein dictionary, og verdiane følgjer bestemde standardar.

Vidare har trekt ut informasjon om alle stasjonar og lagt dei i variabelen `stations`. Dette er ein dictionary der stasjons-id blir brukt som nøkkel.

**Aktivitetsforslag 1.** Opprett variablane `trips` og `stations` som vist i denne seksjonen. Du kan velja sjølv kva månad du vil henta frå [*Oslo bysykkel*](https://oslobysykkel.no/apne-data/historisk).

Bruk løkker, indeksar og nøklar til å skriva ut følgjande inforasjon:

- Skriv ut ei liste over alle stasjonar, på forma *namn,  skildring*:
```
Olaf Ryes plass, langs Sofienberggate
Vår Frelsers gravlund, langs Ullevålsveien
...
```
- Skriv ut informasjon om dei 50 første turane, på følgjande form:
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

* Utfordring: Skriv ut varigheit som talet på minutt og sekunder.

**Aktivitetsforslag 2.** Bruk programmering til å finna ut følgjande om sykkeldataa:

1. Kor mange turar starta og enda på same stasjon? Kor stor prosentdel utgjer dette?
2. Kor mange turar varte kortare enn fem minutt (300 sekund)? Kor stor prosentdel utgjer dette? Kva med turar som varte lengre enn éin time (3600 sekund)?
3. Finnes det turar som varte kortare enn 20 sekund? Skriv ut informasjon om desse turane.
4. Finn sykkelturane som varte kortast og lengst.  Skriv ut informasjon om desse sykkelturane. *Hint: For å finna største verdi i ei liste, treng me ein variabel som blir oppdatert kvar gong me oppdagar eit nytt tal som er større enn det hittil største. Tilsvarande metode blir brukt for å finna minste verdi.*

**Aktivitetsforslag 3.**

1. Korleis kan me rekna ut kva som er gjennomsnittleg varigheit til ein sykkeltur?
2. Bruk programmering til å rekna ut den gjennomsnittlege varigheita til ein sykkeltur.
4. Utfordring: Kva er den gjennomsnittlege varigheita for sykkelturar som starta og enda på same stasjon.
  
*Hint: Den grunnleggjande formelen er å summera varigheita til alle sykkelturane, og deretter dela på talet på turar.*

