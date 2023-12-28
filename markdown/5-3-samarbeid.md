# Samarbeid med Github

## Åpen kildekode

Har du hørt om konseptet *åpen kildekode* (*open source* på engelsk)? Et dataprogram har ofte en *lisens*, som forteller hvordan det er lov til å bruke programmet. En lisens av typen *åpen kildekode* gir hvem som helst rett til å:

* Kjøre programmet til et hvilket som helst formål
* Laste ned koden til programmet (derfor kalles det *åpen kildekode*)
* Bruke koden i et eget program og deretter publisere programmet, så lenge man benytter den samme lisensen

Man kan altså laste ned et åpent kildekode-program, lage en forbedret versjon, og deretter publisere det på nytt. Man kan også bruke programmet som en komponent i et større program som man deretter publiserer. Det viktige er at man publiserer programmet under den samme lisensen, slik at andre kan benytte det nye programmet videre.  

Det motsatte av åpen kildekode er en lisens av typen *lukket kildekode*, som betyr at koden til programmet ikke er tilgjengelig. Å laste ned og distribuere koden regnes da som piratkopiering og kan straffes. De fleste kommersielle programmer har lukket kildekode.

Programmer med åpen kildekode er ofte et resultat av samarbeid og frivillig koding. Når man publiserer programmet sitt med åpen kildekode, kan andre hjelpe til å forbedre det, dra nytte av det i sine egne programmet, eller til og med bruke det til å lage et konkurrerende program! Det virker kanskje rart, men det er en form for sunn konkurranse der man gjerne deler idéer og tar det beste fra hverandres programmer. Det finnes mange eksempler på at prosjekter med åpen kildekode har svært stor innovasjonskraft, fordi de er et resultat av felles innsats fra et stort og internasjonalt miljø av utviklere. 

Kommersielle programmer foretrekkes fortsatt i mange næringer og offentlig administrasjon, men det er verdt å nevne at kommersielle programmer kan ha mange komponenter hentet fra åpen kildekode. Det bør også nevnes at åpen kildekode og gratis programvare **ikke** fjerner behovet for betalt arbeid. Selv om betalte programpakker kan bli mindre relevant i framtiden, blir det kanskje enda viktigere for firmaer og offentlige institusjoner å ansette personer med kompetanse innen informatikk, slik at de kan utnytte det store mangfoldet av fri programvare, og tilpasse det sitt behov. 

Noen eksempler på programmer og teknologier som har åpen kildekode er: 

* *Linux*-operativsystemer
* Mobiloperativsystemet *Android*
* *Python*, *Java*, *Javascript*, *MySQL*, *PHP*, *C++* og mange andre programmeringsspråk
* Nesten alle populære tilleggspakker for Python, som for eksempel:
    * [*NumPy*](https://github.com/numpy/numpy), [*pandas*](https://github.com/pandas-dev/pandas) og [*matplotlib*](https://github.com/matplotlib/matplotlib) for matematiske beregninger, dataanalyse og datavisualisering
    * [*scikit-learn*](https://github.com/scikit-learn/scikit-learn) og [*TensorFlow*](https://github.com/tensorflow/tensorflow) for maskinlæring
    * [*Django*](https://github.com/django/django) og [*Flask*](https://github.com/pallets/flask) for nettsideutvikling
    * [*NLTK*](https://github.com/nltk/nltk) og [*OpenCV*](https://github.com/opencv/opencv) for prosessering av henholdsvis tekst og bilde/video
* Nettleseren [*Mozilla Firefox*](https://www.mozilla.org/)
* [*Jupyter notebook*](https://github.com/jupyter/notebook) /[*Jupyter lab*](https://github.com/jupyterlab/jupyterlab), populære verktøy som tilbyr *"interactive computing with computational notebooks"*
* [*LibreOffice*](https://www.libreoffice.org/), et alternativ til *Microsoft Office*
* [*WordPress*](https://wordpress.com/), et verktøy for å utvikle nettsider
* [*MediaWiki*](https://www.mediawiki.org/wiki/MediaWiki), programvaren bak *Wikipedia*
* Kartdatabasen [*OpenStreetMap*](https://www.openstreetmap.org/)
* [*Blender*](https://www.blender.org/), et program for 3D-modellering -og animasjon
* Tegneprogrammene [*Inkscape*](https://inkscape.org/) og [*GIMP*](https://www.gimp.org/)
* Videoavspilleren [*VLC*](https://www.videolan.org/)

Koden til nesten alle disse programmene finnes i et *Github*-repository. Mange av dem bruker også *Github* som plattform for videre utvikling, som blir drevet fram av et miljø av utviklere over hele verden! Som programmerer kan man involvere seg i et hvilket som helst *Github*-prosjekt med åpen kildekode. Hvordan gjør man det? Det skal vi se på i de neste seksjonene!

## Hvordan bidra til et eksisterende repository?

Tenk deg at du har lyst til å bidra med kode i et eksisterende repository, altså et *Github*-prosjekt. Hvordan går du fram? Det er noen steg vi alltid bør følge: 

1. Fork
2. Clone
3. Branch
4. Gjøre endringer
5. Commit og push
6. Pull request

Her er det to funksjoner vi enda ikke har sett: 

* *Fork* er en funksjon i *Github* for å kopiere innholdet i et eksisterende *Github*-repository, og legge det i vårt eget *Github*-repository.
* *Clone* er en funksjon i *git* for å kopiere et *Github*-repository til vår maskin, slik at vi får et lokalt repository. Dette kalles å *klone* et *Github*-repository.

Det er en viktig regel vi bør følge:

* Dersom vi skal foreslå en forbedring i et repository som ikke er vårt, så bør vi ikke klone det direkte til maskinen vår. Først bør vi opprette en fork, altså en kopi til vår egen *Github*-bruker. Deretter bør vi klone denne kopien til maskinen vår. Derfor er de to første stegene *fork* og *clone*.

De fire siste stegene er kjent fra forrige seksjon, med én viktig forskjell. Denne gangen skal vi nemlig ikke opprette en pull request på vårt eget repository, men på det originale *Github*-prosjektet. Da sender vi et forslag til eieren av det originale programmet, og vår pull request vil kunne gå gjennom flere prosesser, avhengig av hvordan bidrag håndteres i det aktuelle prosjektet. De vanligste stegene er: 

* Code review
* Automatiske tester
* Merge

**Code review.**  Du kan be om at andre bidragsytere i prosjektet ser gjennom forslagene dine. Det er blant annet nyttig å få tilbakemeldinger av personer med inngående kjennskap til programmet, for å sjekke forslaget ditt passer sammen med resten av koden. I tillegg oppdages feil lettere når nye øyne går gjennom koden. 

En person som gjennomfører en code review kan legge inn kommentarer på spesifikke kodelinjer. I kommentarene kan man påpeke mulige feil, foreslå endringer eller be om oppklaringer. Personen som opprettet en pull request kan deretter svare på tilbakemeldingene, og gjøre ytterligere endringer av koden om nødvendig. Etter noen runder med slik kommunikasjon, kan forslaget godkjennes av personen som gjør code review.

**Tester.** De fleste store prosjekter har definert automatiske tester som gjennomføres når en pull request legges inn. De viktigste testene sjekker at programmet ikke gir feilmeldinger og produserer de forventede resultatene. Testene kan sjekke individuelle funksjoner, men også at endringene er riktig integrert i resten av programmet.

Det er viktig at testene dekker den nye koden som foreslås i en pull request. Dersom koden for eksempel inneholder nye funksjoner, kan man bli bedt om å inkludere testdata, det vil si en liste med inndata og forventet utdata. Mange prosjekter kjører en *code coverage analysis*, som forteller hvor stor del av koden som blir dekket av testene. Jo større deler av koden som blir testet, jo mindre sjanse er det for feil.

Det kan også være tester som sjekker at koden følger samme stil som resten av prosjektet. I store prosjekter har det ofte høy prioritet at koden er ryddig, uniform og godt dokumentert.

**Merge.** Når et forslag blir godkjent av alle som gjorde et code review, og alle tester er gjennomført, så er forslaget klart til å smeltes inn i originalprogrammet. Kanskje vil det være noen avsluttende kommentarer, diskusjoner og små endringer. Til slutt brukes funksjonen *merge* til å smelte endringene inn i programmet. Det må gjøres av en bidragsyter med de nødvendige privileger, eller det kan settes opp en automatisk prosess der merge skjer når alle code reviews har blitt merket godkjent, og alle tester er bestått. 

**Aktivitet 1.** Gå inn på [first-contributions](https://github.com/firstcontributions/first-contributions#first-contributions), som er et repository der man kan øve seg på å bidra i *Github*-prosjekter. Følg stegene på forsiden (de finnes også på [norsk](https://github.com/firstcontributions/first-contributions/blob/main/translations/README.no.md)). *I denne oppskriften brukes en annen måte å opprette en branch. Du kan velge mellom denne og måten vist i forrige seksjon.*

**Aktivitet 2.** 

1. Gå sammen med en klassekamerat. Foreslå en endring i et repository som eies av klassekameraten. Du skal følge de samme stegene som er beskrevet [her](https://github.com/firstcontributions/first-contributions#first-contributions), men bruke klassekameratens repository i stedet. 

*Denne aktiviteten er ekstra gøy dersom klassekameraten din har et repository som inneholder kode, og du kan gjøre en liten forbedring, for eksempel legge til en funksjon eller fikse en feil.*

2. Gå inn på din nye pull request, og legg til klassekameraten din som *Reviewer* (du finner denne funksjonen øverst til høyre på siden). Klassekameraten din vil nå få en notifikasjon på sin *Github*-bruker, og kan starte gjennomgangen av din pull request. Få klassekameraten din til å skrive noen kommentarer på spesifikke kodelinjer, og forsøk å svare på disse. 

3. Forsøk nå å gjøre en endring i koden på din pull request. Merk at din pull request er knyttet til ditt *Github*-repository som du opprettet i steg 1 (når du lagde en fork). Derfor kan du gjøre endringer på vanlig måte, og bruke *add*, *commit* og *push* for å legge endringene inn på ditt *Github*-repository. Din pull request vil også oppdateres når du gjør dette.

4. Be klassekameraten din om å merke sin code review som godkjent. Dette gjøres  ved å trykke på knappen *Review changes* (nederst på siden for din pull review), deretter krysse av *Approve* og til slutt klikke *Submit review*. Klassekameraten din kan nå legge endringene dine inn i originalprogrammet, ved å trykke på knappen *Merge*.

5. Bytt roller og gjør stegene 1-4 på nytt.

## Issues

Når du går inn på et repository på Github, vil du som regel se knappen *Issues*. Her kan hvem som helst opprette et såkalt *issue*, og som navnet tilsier er dette måten å rapportere om en feil i programmet. Som regel oppretter man også et issue for å foreslå ny funksjonalitet eller andre forbedringer av prosjektet. Listen over *issues* blir derfor en slags *todo*-liste for et repository. 

Issues og pull requests er tett knyttet sammen. Når man ønsker en spesifikk forbedring av et repository, er følgende prosess vanlig: 

1. Noen oppretter et issue der den ønskede forbedringen beskrives. Det kan være snakk om å fikse en feil, legge til ny funksjonalitet eller forbedre eksisterende kode.
2. Når man har opprettet et issue, er det her man diskuterer den ønskede forbedringen. Man kan diskutere spørsmål som:
    * Er forbedringen nødvendig? Passer forbedringen med prosjektets overordnede mål? Vil integrasjon med resten av koden bli komplisert? Bør andre forbedringer prioriteres først?
    * Kan man beskrive med ord hvordan forbedringen kan realiseres? Finnes alternative løsninger, og hvilken løsning er eventuelt best?
    * Hvor mye arbeid kreves? Hvilke deler av den eksisterende koden må endres? Hva kan man hente fra andre prosjekter? Hvem skal ta ansvar for forbedringen?
    * I tilfelle feil i programmet, når og hvordan oppstår feilen? Hvilke steg kan man gjøre for å reprodusere feilen på sin egen maskin? Hva betyr eventuelle feilmeldinger? Kan man identifisere hva som forårsaker feilen?
3. En person tar ansvar for forbedringen, og oppretter til slutt en pull request. En slik pull request har gjerne en *referanse* til et issue, og vice versa. I slike tilfeller kan vi si at en pull request *løser* et issue. 
4. Når en pull request er opprettet, er det her diskusjonen fortsetter. Koden som er foreslått går gjennom review, testing, diskusjoner og eventuelle forbedringer. Dersom alt er vellykket, kan koden til slutt smeltes inn i programmet.

Dersom et issue har gått gjennom alle disse stegene, blir det til slutt lukket. Et issue kan også lukkes hvis man blir enige om at forbedringen ikke skal realiseres (fordi den ikke er relevant eller ikke kan prioriteres). Et issue som hverken har blitt fullført eller avvist, er et *åpent* issue. Hvem som helst kan prøve å løse et åpent issue og deretter legge inn en pull request med den foreslåtte løsningen. 

Som konklusjon kan vi si at *Issues* gir en ryddig måte å planlegge enhver type forbedring i et repository, enten det er snakk om retting av en feil, ny funksjonalitet eller andre forbedringer av koden. Issues gir en oversikt over eksisterende oppgaver i et prosjekt, og legger til rette for samarbeid og kommunikasjon rundt disse. 

Listen over alle tidligere issues og pull requests fungerer som et arkiv over alle avgjørelser som har blitt tatt, og kan være en nyttig referanse i framtiden. 

**Aktivitet 1.** Finn noen prosjekter som interesserer deg ved å søke på *Github*. Trykk deretter på *Issues*, og gå inn på noen issues. Finn ut av følgende:
* Hvilken informasjon må tas med i et issue? Følges alltid en bestemt mal? Varierer dette fra prosjekt til prosjekt? 
* Bruk nedtrekksmenyen *Label* til å finne issues med forskjellige merkelapper. Finn minst et issue som registrerer en feil (*bug*) og et issue som foreslår ny funksjonalitet. Brukes forskjellige maler til å registrere ulike typer issues?
    * Prøv gjerne å finne merkelappen *good first issues*, som betyr at forbedringen er relativt enkel å realisere. Dette er en god måte å finne ut hvor man kan gjøre sitt første bidrag! 
* Hva slags diskusjon finner sted på ulike typer issues?
* Trykk på *closed issues* og gå inn på noen lukkede issues. Gå nederst på siden og finn ut hvorfor de ble lukket. Er noen issues koblet til et pull request?

**Aktivitet 2.** Forsøk å opprette et issue på ditt eget repository. Gå inn på *Issues* og trykk på *New issue*. Følg en mal som du fant i *Aktivitet 1* til å skrive et fiktivt issue (eller et ekte issue, dersom du kommer på en en forbedring du ønsker for programmet ditt).
