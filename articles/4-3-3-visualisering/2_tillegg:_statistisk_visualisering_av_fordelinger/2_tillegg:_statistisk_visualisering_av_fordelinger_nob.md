---
title: "Tillegg: Statistisk visualisering av fordelinger"
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

I forrige seksjon så vi på følgende søylediagram:


```python
counts.plot(kind='bar')
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_61_0.png' width=600>
    


Diagrammet viser antall turer på hver klokketime, og gir en veldig god oversikt over hvordan sykkelturene fordeler seg med tanke på klokkeslett.

Hva om vi ønsker en tilsvarende oversikt med tanke på avstand (mellom start -og sluttpunkt)? Foreløpig har vi følgende informasjon:


```python
distances = trips["distance"]
print(distances.mean())
print(distances.min())
print(distances.max())
```

    1.5637046147163225
    0.0
    8.17033235134136


Vi kjenner altså gjennomsnittlig, minste og største avstand, men vi har veldig lite detaljer. Et søylediagram som viser hvilke avstander som forekommer mest ville gitt oss mye mer informasjon!

Husk at hver søyle må representere en gruppe, så for eksempel kunne den første gruppen være turer mellom 0 og 0.49 km, den andre gruppen mellom 0.50 og 1.00 km, og så videre. Heldigvis trenger vi ikke å opprette disse gruppene selv - det finnes nemlig en Python-pakke som kan lage diagrammet for oss! 


```python
import seaborn as sns

sns.histplot(distances, bins=50)
plt.xlim(0, 8)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_65_0.png' width=600>
    


Dette diagrammet kalles et *histogram*, og skiller seg fra et søylediagram ved at gruppene er små intervaller på tallinja.  Vi har brukt [*seaborn*](https://seaborn.pydata.org/), som er en Python-pakke for statistiske datavisualiseringer. Med funksjonen `histplot` kan vi lage det ønskede histogrammet:

- Som første parameter bruker vi kolonnen med avstander. Merk at denne kolonnen er hentet fra turtabellen og har derfor over 130.000 verdier!
- Med parameteren `bins` definerer vi antall søyler.

I histogrammet ser vi at mange turer ligger rundt 1.2 km, og ettersom avstanden øker, blir det gradvis færre turer. Merk deg den høye toppen som inkluderer turer med avstand nær null. Dette kan skyldes at mange turer starter og slutter på samme stasjon - for eksempel er det naturlig å tenke at mange bruker bysykkel for å handle dagligvarer, altså frem -og tilbaketurer. 

Du legger kanskje merke til at toppen av søylene ser ut til å danne en graf? En *KDE*-graf (*kernel density estimate*) er en utjevnet versjon av histogrammet, som gir en penere måte å visualisere hvordan sykkelturene fordeler seg med tanke på avstand:


```python
sns.kdeplot(distances, color="green", fill=True)
plt.xlim(0, 8)
plt.grid(True, which='both', linestyle='--', linewidth=0.5)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_67_0.png' width=600>
    


Med denne grafen får vi et overblikk over hvilke avstander som er mest forekommende. Vi trenger ikke å forstå nøyaktig hva tallene på $y$-aksen betyr, men dersom vi integrerer hele grafen, blir svaret 1. Det betyr at arealet mellom to punkter kan gi oss nyttig informasjon.

Hvis for eksempel arealet under grafen mellom 1 og 2 km er 0.5, så betyr det at 50% av sykkelturene befinner seg i dette intervallet.

For å få enda mer ut av grafen, skal vi nå legge til ekstra informasjon. Du trenger ikke å forstå funksjonen under, men du kan kopiere den inn i ditt eget program:


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

Her har vi definert funksjonen `kdeplot_with_info`, og vi kan for eksempel bruke den på avstandskolonnen:


```python
kdeplot_with_info(distances)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_71_0.png' width=600>
    


Her har vi fått med gjennomsnitt -og medianverdi i diagrammet. Medianverdien deler grafen opp i to deler med like stort areal. Sagt på en annen måte; det er like mange sykkelturer til venstre og høyre for medianverdien. 

Hvorfor er gjennomsnittet og medianen forskjellig? Tenk deg at vi har registrert tre turer med avstander 1 km, 2 km og 6 km. Da er medianen (den "midterste" verdien) lik 2 km, men gjennomsnittet er 3 km! Det er fordi den lengste turen trekker gjennomsnittet opp!

Det grønne området markerer 90% av arealet, på en slik måte at det er like mye areal på hver side. Derfor kalles det grønne området for *central 90%*. I vår graf er dette området mellom 0.29 km og 3.45 km. Fra dette kan vi gjøre følgende konklusjoner:

* De 5 % korteste turene var 0 - 0.29 km.
* De 5 % lengste turene var 3.45 km og lengre.
* De 90 % "midterste" turene var mellom 0.29 og 3.45 km.

Ved å bruke tilleggsparameteren `central`, kan vi bestemme hvor stort det sentrale området skal være:


```python
kdeplot_with_info(distances, central=50)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_73_0.png' width=600>
    


Her ser vi at 50 % av turene faller omtrent innenfor 1-2 km.

I starten av seksjonen viste vi hvordan sykkelturene er fordelt på klokketimer. Vi kan også vise dette som en *KDE*-graf. Men da må klokkeslettene konverteres til desimaltall på intervallet 0-24. For eksempel, hvis en tur startet på tidspunktet *13:30:00*, så skal dette konverteres til 13.5.

Først oppretter vi en funksjon som kan konvertere datostrenger til desimaltall:


```python
def get_time_as_decimal(date_string):
    date_object = datetime.fromisoformat(date_string)
    return date_object.hour + date_object.minute/60 + date_object.second/3600

test = get_time_as_decimal("2023-07-01 10:27:10")
print(test)
```

    10.452777777777778


Nå kan vi opprette en ny kolonne i turtabellen som inneholder starttidspunktet som desimaltall:


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


Nå som vi har en kolonne med desimaltall, kan vi bruke den til å opprette en *KDE*-graf:


```python
kdeplot_with_info(trips["started_at_as_decimal"])
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_80_0.png' width=600>
    


Mediantidspunktet for en sykkeltur er 13.71, som svarer til klokkeslettet 13:43 (fordi 71% av en time er 43 minutter). Videre ser vi at 90% av sykkelturer skjer mellom 5.85 og 20.68 (hvilke klokkelsett svarer dette til?). 

Grafen har et tydelig toppunkt rundt kl. 7, som antagelig kan forklares med at folk drar på jobb rundt dette tidspunktet. Men hva om vi sammenligner hverdag og helg?

Her er det fornuftig å opprette to tabeller; én med alle hverdagsturer og én med alle helgesturer: 


```python
weekday = trips[trips["part_of_week"]=="weekday"]
weekend = trips[trips["part_of_week"]=="weekend"]
tables = [weekday, weekend]
labels = ["weekday", "weekend"]
```

I forrige seksjon så vi hvordan vi kan bruke en løkke til å lage flere diagrammer samtidig:


```python
for i in range(2):
    table = tables[i]
    label = labels[i]

    kdeplot_with_info(table["started_at_as_decimal"])
    filename = f"kde-{label}.pdf"
    plt.savefig(filename)
    plt.close()
```

Med denne koden har vi opprettet to filer: 

* *kde-weekday.pdf* 


```python
table = tables[0]
label = labels[0]

kdeplot_with_info(table["started_at_as_decimal"])
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_86_0.png' width=600>
    


* *kde-weekend.pdf*


```python
table = tables[1]
label = labels[1]

kdeplot_with_info(table["started_at_as_decimal"])
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_88_0.png' width=600>
    


Her kan vi se at toppunktet kl. 7 har blitt veldig tydelig på hverdager, mens i helger finner vi ikke et tilsvarende toppunkt!

**Oppsummering.** I forrige seksjon viste vi hvordan sykkelturene fordelte seg på bestemte kategorier, mens i denne seksjonen har vi vist hvordan sykkelturene fordeler seg på tallverdier, slik som varighet og avstand. Vi har brukt både histogram og *KDE*-grafer, som er statistiske metoder for å visualisere data. 

**Aktivitetsforslag.** For hver av de følgende gruppene, vis hvordan sykkelturene fordeler seg utover en dag ved å bruke en *KDE*-graf:

1a. Turer kortere enn én time (3600 sekunder)   
1b. Turer på én time eller lengre   
2a. Turer som startet og sluttet på samme stasjon   
2b. Turer som var kortere enn 1 km   
2c. Turer som var lengre enn 3 km   


Sammenlign grafene 1a-1b og 2a-2c. Hvilke forskjeller finner du? Hva tror du er årsaken til forskjellene?

