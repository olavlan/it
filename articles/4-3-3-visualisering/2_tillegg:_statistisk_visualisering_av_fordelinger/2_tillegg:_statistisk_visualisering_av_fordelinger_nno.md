---
title: "Tillegg: Statistisk visualisering av fordelingar"
figures_to_include:
	- "4-3-3-visualisering_61_0.png"
	- "4-3-3-visualisering_65_0.png"
	- "4-3-3-visualisering_67_0.png"
	- "4-3-3-visualisering_71_0.png"
	- "4-3-3-visualisering_73_0.png"
	- "4-3-3-visualisering_80_0.png"
	- "4-3-3-visualisering_86_0.png"
	- "4-3-3-visualisering_88_0.png"
---

I førre seksjon såg me på følgjande søylediagram:


```python
counts.plot(kind='bar')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_61_0.png' width=600>
    


Diagrammet viser talet på turar på kvar klokketime, og gir ei veldig god oversikt over korleis sykkelturane fordeler seg med tanke på klokkeslett.

Kva om me ønskjer ei tilsvarande oversikt med tanke på avstand (mellom start -og sluttpunkt)? Førebels har me følgjande informasjon:


```python
distances = trips["distance"]
print(distances.mean())
print(distances.min())
print(distances.max())
```

    1.5637046147163225
    0.0
    8.17033235134136


Me kjenner altså gjennomsnittleg, minste og største avstand, men me har veldig lite detaljar. Eit søylediagram som viser kva avstandar som finst mest ville gitt oss mykje meir informasjon!

Hugs at kvar søyle må representera ei gruppe, så til dømes kunne den første gruppa vera turar mellom 0 og 0.49 km, den andre gruppa mellom 0.50 og 1.00 km, og så vidare. Heldigvis treng me ikkje å oppretta desse gruppene sjølv - det finst nemleg ein Python-pakke som kan laga diagrammet for oss!


```python
import seaborn as sns

sns.histplot(distances, bins=50)
plt.xlim(0, 8)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_65_0.png' width=600>
    


Dette diagrammet blir kalla eit *histogram*, og skil seg frå eit søylediagram ved at gruppene er små intervall på tallinja.  Me har brukt [*seaborn*](https://seaborn.pydata.org/), som er ein Python-pakke for statistiske datavisualiseringar. Med funksjonen `histplot` kan me laga det ønskte histogrammet:

- Som første parameter bruker me kolonnen med avstandar. Merk at denne kolonnen er henta frå turtabellen og har derfor over 130.000 verdiar!
- Med parameteren `bins` definerer me talet på søyler.

I histogrammet ser me at mange turar ligg rundt 1.2 km, og ettersom avstanden aukar, blir det gradvis færre turar. Merk deg den høge toppen som inkluderer turar med avstand nær null. Dette kan komma av at mange turar startar og sluttar på same stasjon - til dømes er det naturleg å tenkja at mange bruker bysykkel for å handla daglegvarer, altså fram -og tilbaketurar.

Du legg kanskje merke til at toppen av søylene ser ut til å danna ein graf? Ein *KDE*-graf (*kernel density estimate*) er ein jamna ut versjon av histogrammet, som gir ein finare måte å visualisera korleis sykkelturane fordeler seg med tanke på avstand:


```python
sns.kdeplot(distances, color="green", fill=True)
plt.xlim(0, 8)
plt.grid(True, which='both', linestyle='--', linewidth=0.5)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_67_0.png' width=600>
    


Med denne grafen får me eit overblikk over kva avstandar som er mest forekommande. Me treng ikkje å forstå nøyaktig kva tala på $y$-aksen betyr, men dersom me integrerer heile grafen, blir svaret 1. Det betyr at arealet mellom to punkt kan gi oss nyttig informasjon.

Viss til dømes arealet under grafen mellom 1 og 2 km er 0.5, så betyr det at 50% av sykkelturane er i dette intervallet.

For å få endå meir ut av grafen, skal me no leggja til ekstra informasjon. Du treng ikkje å forstå funksjonen under, men du kan kopiera han inn i ditt eige program:


```python
from scipy.stats import gaussian_kde

def kdeplot_with_info(values, central = 90, ax = None, unit = "", color = "green"):
    if ax is None:
        ax = plt.gca()

    d = (100-central)/2.0
    ps = np.percentile(values, d)
    pe = np.percentile(values, 100-d)
    mean = values.mean()
    median = values.median()
        
    kde = gaussian_kde(values)
    kde_mean = kde.evaluate(mean)[0]
    kde_median = kde.evaluate(median)[0]
        
    area90_label = f"Central {central}%: {ps:.2f} - {pe:.2f} {unit}"
    mean_label = f"Mean: {mean:.2f} {unit}"
    median_label = f"Median: {median:.2f} {unit}"

    sns.kdeplot(values, ax=ax, color="grey", fill=True)
    sns.kdeplot(values, ax=ax, color=color, fill=True, label=area90_label, clip=(ps, pe))
    ax.plot([mean, mean], [0, kde_mean], color=color, label=mean_label)
    ax.plot([median, median], [0, kde_median], color=color,  linestyle="--", label=median_label)
    plt.grid(True, which='both', linestyle='--', linewidth=0.5)
    ax.legend()

    xmax = np.percentile(values, 99)
    ymax = ax.get_ylim()[1]
    
    return xmax, ymax
```

Her har me definert funksjonen `kdeplot_with_info`, og me kan til dømes bruka han på avstandskolonnen:


```python
kdeplot_with_info(distances)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_71_0.png' width=600>
    


Her har me fått med gjennomsnitt -og medianverdi i diagrammet. Medianverdien deler grafen opp i to delar med like stort areal. Sagt på ein annan måte; det er like mange sykkelturar til venstre og høgre for medianverdien.

Kvifor er gjennomsnittet og medianen ulikt? Tenk deg at me har registrert tre turar med avstandar 1 km, 2 km og 6 km. Då er medianen (den "midtarste" verdien) lik 2 km, men gjennomsnittet er 3 km! Det er fordi den lengste turen trekkjer gjennomsnittet opp!

Det grøne området markerer 90% av arealet, på ein slik måte at det er like mykje areal på kvar side. Derfor blir det grøne området kalla for *central 90%*. I grafen vår er dette området mellom 0.29 km og 3.45 km. Frå dette kan me gjera følgjande konklusjonar:

* Dei 5 % kortaste turane var 0 - 0.29 km.
* Dei 5 % lengste turane var 3.45 km og lengre.
* Dei 90 % "midtarste" turane var mellom 0.29 og 3.45 km.

Ved å bruka tilleggsparameteren `central`, kan me avgjera kor stort det sentrale området skal vera:


```python
kdeplot_with_info(distances, central=50)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_73_0.png' width=600>
    


Her ser me at 50 % av turane fell omtrent innanfor 1-2 km.

I starten av seksjonen viste me korleis sykkelturane er fordelt på klokketimar. Me kan også visa dette som ein *KDE*-graf. Men då må klokkesletta konverterast til desimaltal på intervallet 0-24. Til dømes, viss ein tur starta på tidspunktet *13:30:00*, så skal dette konverterast til 13.5

Først opprettar me ein funksjon som kan konvertera datostrenger til desimaltal:


```python
def get_time_as_decimal(date_string):
    date_object = datetime.fromisoformat(date_string)
    return date_object.hour + date_object.minute/60 + date_object.second/3600

test = get_time_as_decimal("2023-07-01 10:27:10")
print(test)
```

    10.452777777777778


No kan me oppretta ein ny kolonne i turtabellen som inneheld starttidspunktet som desimaltal:


```python
trips["started_at_as_decimal"] = trips["started_at"].apply(get_hour_as_fraction)
print(trips["started_at_as_decimal"])
```

    0          1.377222
    1          3.045278
    2          3.224444
    3          3.255000
    4          3.368611
                ...    
    131376    22.941111
    131377    22.963333
    131378    22.985278
    131379    23.365556
    131380    23.365556
Name: started_at_as_decimal, Length: 131381, dtype: float64


No som me har ein kolonne med desimaltal, kan me bruka han til å oppretta ein *KDE*-graf:


```python
kdeplot_with_info(trips["started_at_as_decimal"])
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_80_0.png' width=600>
    


Mediantidspunktet for ein sykkeltur er 13.71, som svarer til klokkeslettet 13:43 (fordi 71% av ein time er 43 minutt). Vidare ser me at 90% av sykkelturar skjer mellom 5.85 og 20.68 (kva klokkelsett svarer dette til?).

Grafen har eit tydeleg toppunkt rundt kl. 7, som antakeleg kan forklarast med at folk dreg på jobb rundt dette tidspunktet. Men kva om me samanliknar kvardag og helg?

Her er det fornuftig å oppretta to tabellar; éin med alle kvardagsturar og éin med alle helgesturer:


```python
weekday = trips[trips["part_of_week"]=="weekday"]
weekend = trips[trips["part_of_week"]=="weekend"]
tables = [weekday, weekend]
labels = ["weekday", "weekend"]
```

I førre seksjon såg me korleis me kan bruka ei løkke til å laga fleire diagram samtidig:


```python
for i in range(2):
    table = tables[i]
    label = labels[i]

    kdeplot_with_info(table["started_at_as_decimal"])
    filename = f"kde-{label}.pdf"
    plt.savefig(filename)
    plt.close()
```

Med denne koden har me oppretta to filer:

* *kde-weekday.PDF*


```python
table = tables[0]
label = labels[0]

kdeplot_with_info(table["started_at_as_decimal"])
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_86_0.png' width=600>
    


* *kde-weekend.PDF*


```python
table = tables[1]
label = labels[1]

kdeplot_with_info(table["started_at_as_decimal"])
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_88_0.png' width=600>
    


Her kan me sjå at toppunktet kl. 7 har vorte veldig tydeleg på kvardagar, medan i helgar finn me ikkje eit tilsvarande toppunkt!

**Oppsummering.** I førre seksjon viste me korleis sykkelturane fordelte seg på bestemde kategoriar, medan i denne seksjonen har me vist korleis sykkelturane fordeler seg på talverdiar, slik som varigheit og avstand. Me har brukt både histogram og *KDE*-grafar, som er statistiske metodar for å visualisera data.

**Aktivitetsforslag.** For kvar av dei følgjande gruppene, vis korleis sykkelturane fordeler seg utover ein dag ved å bruka ein *KDE*-graf:

1a. Turar kortare enn éin time (3600 sekund)
1b. Turar på éin time eller lengre
2a. Turar som starta og slutta på same stasjon
2b. Turar som var kortare enn 1 km
2c. Turar som var lengre enn 3 km


Samanlikn grafane 1a-1b og 2a-2c. Kva forskjellar finn du? Kva trur du er årsaka til forskjellane?

