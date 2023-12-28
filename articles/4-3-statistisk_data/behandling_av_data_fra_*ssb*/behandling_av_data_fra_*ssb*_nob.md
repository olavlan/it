---
title: "Behandling av data fra *SSB*"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---

I denne seksjonen skal vi behandle data som er lagret etter *JSON-stat*-standarden. Vi skal hente ferdige datasett publisert av *SSB*, som ligger [her](https://data.ssb.no/api/). 

**Versjoner av *JSON*-stat.** I seksjonen om *JSON-stat* forklarte vi strukturen til et *JSON-stat*-objekt basert på den nyeste versjonen, *JSON-stat* 2.0. Dette registrerte vi også som første attributt i objektet: 

```json
"version": "2.0"
```

*SSB* benytter imidlertid en eldre versjon av *JSON-stat*. Måten å registrere data på er helt likt, men attributtene er organisert litt annerledes. Følgende viser strukturen til ny og gammel *JSON-stat*.


***JSON-stat* 2.0**:

```json
    {
    "version": "2.0",
    "class": "dataset",
    "label": "", 

    "id": ["Dimension1", "Dimension2"],
    "size": [], 
    "dimension": {
        "Dimension1": {
            "category": {
                "index": {}
                "label": {}
            }
        },
        "Dimension2": {
            "category": {
                "index": {}
                "label": {}
            }
        } 
    }

    "value": []
}
```
***JSON-stat* brukt av SSB:**

```json
{
    "dataset": {
        
        "label": ""
        
        "dimension": {
            "id": ["Dimension1", "Dimension2"],
            "size": [], 
            "Dimension1": {
                "category": {
                    "index": {}
                    "label": {}
                }
            },
            "Dimension2": {
                "category": {
                    "index": {}
                    "label": {}
                }
            }
        
        "value": []
    }
}
```

Det er to hovedforskjeller:

1. I *JSON-stat* brukt av *SSB* plasseres alt inni attributtet "dataset". 
2. I *JSON-stat* brukt av *SSB* plasseres alle dimensjonsdata i attributtet "dimension". Dette inkluderer "id" og "size". 

