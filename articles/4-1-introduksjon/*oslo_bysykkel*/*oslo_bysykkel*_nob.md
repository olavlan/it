---
title: "*Oslo bysykkel*"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

For å vise hvor spennende datahåndtering kan være, skal vi ta utgangspunkt i data fra *Oslo Bysykkel*, som har 259 selvbetjente sykkelstasjoner i Oslo (i April 2023); du kan se alle sykkelstasjonene på [dette kartet](https://oslobysykkel.no/stasjoner). Når en person låser opp en sykkel på en stasjon A, og leverer den på stasjon B, så har det blitt registrert en tur fra A til B. Følgende tur ble registrert den 26. April 2023: 

```json
{
        "started_at": "2023-04-29 12:10:38.207000+00:00",
        "ended_at": "2023-04-29 12:14:34.256000+00:00",
        "duration": 236,
        "start_station_id": "463",
        "start_station_name": "Schous plass trikkestopp",
        "start_station_description": "ved biblioteket",
        "start_station_latitude": 59.9207284,
        "start_station_longitude": 10.7594857,
        "end_station_id": "437",
        "end_station_name": "Sentrum Scene",
        "end_station_description": "ved Arbeidersamfunnets plass",
        "end_station_latitude": 59.91546786564256,
        "end_station_longitude": 10.751140873016311
}
```

Her vises diverse informasjon om turen, slik som:
* Nøyaktig start -og sluttidspunkt
* Turens varighet i sekunder
* Nøyaktig start -og sluttposisjon, gitt som geografiske koordinater

Dataene ovenfor er skrevet i formatet *JSON*, og i neste seksjon skal vi lære reglene for å skrive data i dette formatet. Vi kan *lagre* *JSON*-dataene ved å opprette en fil med filendelsen `.json`, og deretter kan vi *sende* filen til andre datamaskiner, eller bruke programmering til å lese filen og *behandle* dataene. Databehandling er  kanskje ikke så interessant når vi bare har én sykkeltur, men hva om vi har flere tusen registrerte turer? 

På *Oslo bysykkel* sine hjemmesider kan vi gå inn på [historiske data](https://oslobysykkel.no/apne-data/historisk) og hente *JSON*-filer for hver måned, det vil si alle registrerte turer! For eksempel starter *JSON*-filen for April 2023 slik:

```json
{
    "started_at": "2023-04-01 03:23:05.537000+00:00",
    "ended_at": "2023-04-01 03:32:55.489000+00:00",
    "duration": 589,
    "start_station_id": "424",
    "start_station_name": "Birkelunden",
    "start_station_description": "langs Seilduksgata",
    "start_station_latitude": 59.9256113,
    "start_station_longitude": 10.760926,
    "end_station_id": "464",
    "end_station_name": "Sukkerbiten",
    "end_station_description": "ved gangbroen",
    "end_station_latitude": 59.905124380703484,
    "end_station_longitude": 10.753763553726515
},
{
    "started_at": "2023-04-01 03:28:06.449000+00:00",
    "ended_at": "2023-04-01 03:34:52.075000+00:00",
    "duration": 405,
    "start_station_id": "592",
    "start_station_name": "Badebakken",
    "start_station_description": "langs Maridalsveien",
    "start_station_latitude": 59.94558091179507,
    "start_station_longitude": 10.760323881579982,
    "end_station_id": "397",
    "end_station_name": "Storo Storsenter",
    "end_station_description": "langs Vitaminveien",
    "end_station_latitude": 59.94671044754387,
    "end_station_longitude": 10.773805285879131
}
```

Her ser vi de to første sykkelturene som ble registrert denne måneden, og hele filen inneholder over 70.000 turer! I Python kan vi gjøre masse interessant med disse dataene, som for eksempel: 

* Finne gjennomsnittlig eller median reisetid mellom to stasjoner, basert på alle turer som har blitt gjort mellom stasjonene. 
    * Deretter kan man for eksempel sammenligne reisetidene med alternative transportmetoder. For eksempel kan forventet reisetid med offentlig transport hentes fra [*Entur*](https://entur.no/), og reisetider med bil kan hentes fra *Google Maps*. Både *Entur* og *Google* tilbyr et grensesnitt som gjør det mulig å hente slik data med programmering!
* Finne ut hvor ofte hver stasjon brukes, enten som start -eller endestasjon. Resultatene kan deretter presenteres på forskjellige måter; for eksempel kan stasjonene markeres som sirkler på et kart, der størrelsen på sirkelen viser hvor populær stasjonen er. 
* Vi lage et 24-timersdiagram for hver stasjon, som forteller hvilke tidspunkter stasjonen brukes mest. 
* Vi kan kombinere de to punktene ovenfor, og lage en kartanimasjon som viser hvordan populæriteten til stasjonene endrer seg gjennom en dag.


Dette er ment som eksempler på veldig interessante (men også utfordrende) måter å behandle data. I senere seksjoner skal vi smått starte på disse eksemplene, og du vil få en kunnskapsbase som gjør at du selv kan bygge videre på det. 

Først må vi lære hvordan data registreres i formatet *JSON*!


