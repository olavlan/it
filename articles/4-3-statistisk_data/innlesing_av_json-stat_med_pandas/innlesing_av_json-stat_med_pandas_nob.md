---
title: "Innlesing av JSON-stat med pandas"
belongs_to_chain: "Behandling av statistisk data"
figures_to_include:
---


```python
from pyjstat import pyjstat

with open("befolkning.json") as file:
    dataset = pyjstat.Dataset.read(file)

df = dataset.write('dataframe')
print(df)
```

