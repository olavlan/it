---
title: "Behandling av data frå *SSB*"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---

I denne seksjonen skal me behandla data som er lagra etter *JSON-stat*-standarden. Me skal henta ferdige datasett publisert av **SSB*, som ligg [her](https://data.ssb.no/api/).

**Versjonar av *JSON*-stat.** I seksjonen om *JSON-stat* forklarte me strukturen til eit *JSON-stat*-objekt basert på den nyaste versjonen, *JSON-stat* 2.0. Dette registrerte me også som første attributt i objektet:

```json
"version": "2.0"
```

*SSB* nyttar likevel ein eldre versjon av *JSON-stat*. Måten å registrera data på er heilt likt, men attributta er organiserte litt annleis. Følgjande viser strukturen til ny og gammal *JSON-stat*.


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

Det er to hovudforskjellar:

1. I *JSON-stat* brukt av *SSB* blir plassert alt inni attributtet "dataset".
2. I *JSON-stat* brukt av *SSB* blir plasserte alle dimensjonsdata i attributtet "dimension". Dette inkluderer "id" og "size".

