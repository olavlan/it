---
title: "*Oslo bysykkel*"
belongs_to_chain: "Datahåndtering"
figures_to_include:
---

For å visa kor spennande datahandtering kan vera, skal me ta utgangspunkt i data frå *Oslo *Bysykkel*, som har 259 sjølvbetente sykkelstasjonar i Oslo (i April 2023); du kan sjå alle sykkelstasjonane på [dette kartet](https://oslobysykkel.no/stasjoner). Når ein person låser opp ein sykkel på ein stasjon A, og leverer han på stasjon B, så har det vorte registrert ein tur frå A til B. Følgende tur vart registrert den 26. April 2023:

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

Her blir diverse informasjon vist om turen, slik som:
* Nøyaktig start -og sluttidpunkt
* Varigheita til turen i sekund
* Nøyaktig start -og sluttposisjon, gitt som geografiske koordinatar

Dataa ovanfor er skrivne i formatet *JSON*, og i neste seksjon skal me læra reglane for å skriva data i dette formatet. Me kan *lagra* *JSON*-dataa ved å oppretta ei fil med filendinga `.json`, og deretter kan me *senda* fila til andre datamaskiner, eller bruka programmering til å lesa fila og *behandla* dataa. Databehandling er  kanskje ikkje så interessant når me berre har éin sykkeltur, men kva om me har fleire tusen registrerte turar?

På *Oslo bysykkel* nettsidene sine kan me gå inn på [historiske data](https://oslobysykkel.no/apne-data/historisk) og henta *JSON*-filer for kvar månad, det vil seia alle registrerte turar! Til dømes startar *JSON*-fila for April 2023 slik:

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

Her ser me dei to første sykkelturane som vart registrerte denne månaden, og heile fila inneheld over 70.000 turar! I Python kan me gjera mykje interessant med desse dataa, som til dømes:

* Finne gjennomsnittleg eller median reisetid mellom to stasjonar, basert på alle turar som har vorte gjorde mellom stasjonane.
* Deretter kan ein til dømes samanlikna reisetidene med alternative transportmetodar. Til dømes kan forventa reisetid med offentleg transport blir frå henta [*Entur*](https://entur.no/), og reisetider med bil kan hentast frå *Google Maps*. Både *Entur* og *Google* tilbyr eit grensesnitt som gjer det mogleg å henta slik data med programmering!
* Finna ut kor ofte kvar stasjon blir brukt, anten som start -eller endestasjon. Resultata kan deretter presenterast på ulike måtar; til dømes kan stasjonane markerast som sirklar på eit kart, der storleiken på sirkelen viser kor populær stasjonen er.
* Me laga eit 24-timeirdiagram for kvar stasjon, som fortel kva tidspunkt stasjonen blir mest brukt.
* Me kan kombinera dei to punkta ovanfor, og laga ein kartanimasjon som viser korleis populæriteten til stasjonane endrar seg gjennom ein dag.


Dette er meint som døme på veldig interessante (men også utfordrande) måtar å behandla data. I seinare seksjonar skal me smått starta på desse døma, og du vil få ein kunnskapsbase som gjer at du sjølv kan byggja vidare på det.

Først må me læra korleis data blir registrerte i formatet *JSON*!


