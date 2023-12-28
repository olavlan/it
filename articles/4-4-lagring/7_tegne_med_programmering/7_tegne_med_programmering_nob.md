---
title: "Tegne med programmering"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I denne seksjonen skal vi se på hvordan man kan tegne med programmering. Dette er en seksjon som er ekstra interessert i vektorgrafikk, og hvordan man kan utvikle nyttige tegneverktøy der alt gjøres med kode!

Vi begynner med en oppgave som du kan prøve deg på. Tegn et mønster med sirkler og linjer, enten på et ark eller i et tegneprogram som *Paint*. Gå deretter inn på [*SVG Viewer*](https://www.svgviewer.dev/s/LfxtOdK1) og forsøk å lage det samme mønsteret med *SVG*-kode. 

Tenk at du nå har lyst til å fortsette det samme mønsteret uten å måtte skrive inn de neste linjene og sirklene selv. Kan du lage et Python-program som finner de riktige koordinatene, og deretter skriver ut *SVG*-koden til et større bilde med samme mønster? 

Som hjelp kan du bruke funksjonene under. Først viser vi hvordan du kan tegne et mønsteret én gang. I vårt eksempel består mønsteret av to linjer og en sirkel (se figuren i [*SVG Viewer*](https://www.svgviewer.dev/s/dnXrdjhk)): 


```python
lineA = [0, 0, 100, 100]
lineB = [0, 100, 100, 0]
circle = [100, 50, 35]

def svg_line(line):
    x1, y1, x2, y2 = line
    return '<line x1="%s" y1="%s" x2="%s" y2="%s" stroke="black"></line>\n' % (x1, y1, x2, y2)

def svg_circle(circle):
    x, y, r = circle
    return '<circle cx="%s" cy="%s" r="%s" fill="white" stroke="black"></circle>\n' % (x, y, r)

svg = '<svg width="150" height="100"> \n'
svg += svg_line(lineA) + svg_line(lineB) + svg_circle(circle)
svg += '</svg>'

print(svg)
```

    <svg width="150" height="100"> 
    <line x1="0" y1="0" x2="100" y2="100" stroke="black"></line>
    <line x1="0" y1="100" x2="100" y2="0" stroke="black"></line>
    <circle cx="100" cy="50" r="35" fill="white" stroke="black"></circle>
    </svg>


[Se i SVG Viewer](https://www.svgviewer.dev/s/65R1QjCn)

Nå viser vi hvordan vi kan repetere dette mønsteret fem ganger mot høyre. Til dette kan vi lage funksjoner som flytter linjer og sirkler en viss avstand i x -eller y-retning (positiv x-retning er mot høyre, og positiv y-retning er nedover). 


```python
def move_line(line, move_x=0, move_y=0):
    x1, y1, x2, y2 = line
    x1 = x1 + move_x
    x2 = x2 + move_x
    y1 = y1 + move_y
    y2 = y2 + move_y
    new_line =  [x1, y1, x2, y2]
    return new_line
    
def move_circle(circle, move_x=0, move_y=0):
    x, y, r = circle
    x = x + move_x
    y = y + move_y
    new_circle = [x, y, r]
    return new_circle
```

*Merk at disse funksjonene ikke returnerer *SVG*-kode, men en liste av verdier for en linje eller sirkel.*

Nå kan vi skrive kode som tegner linjene og sirklene fem ganger. Mellom hver gang vi tegner dem, må vi flytte dem 100 i x-retning, slik at vi oppnår mønsteret vi ønsker oss.


```python
lineA = [0, 0, 100, 100]
lineB = [0, 100, 100, 0]
circle = [100, 50, 35]
move_x = 100

svg = '<svg width="600" height="100" > \n'
for i in range(4): 
    svg += svg_line(lineA) + svg_line(lineB) + svg_circle(circle)
    lineA = move_line(lineA, move_x)
    lineB = move_line(lineB, move_x)
    circle = move_circle(circle, move_x)
svg += '</svg>'

print(svg)
```

    <svg width="600" height="100" > 
    <line x1="0" y1="0" x2="100" y2="100" stroke="black"></line>
    <line x1="0" y1="100" x2="100" y2="0" stroke="black"></line>
    <circle cx="100" cy="50" r="35" fill="white" stroke="black"></circle>
    <line x1="100" y1="0" x2="200" y2="100" stroke="black"></line>
    <line x1="100" y1="100" x2="200" y2="0" stroke="black"></line>
    <circle cx="200" cy="50" r="35" fill="white" stroke="black"></circle>
    <line x1="200" y1="0" x2="300" y2="100" stroke="black"></line>
    <line x1="200" y1="100" x2="300" y2="0" stroke="black"></line>
    <circle cx="300" cy="50" r="35" fill="white" stroke="black"></circle>
    <line x1="300" y1="0" x2="400" y2="100" stroke="black"></line>
    <line x1="300" y1="100" x2="400" y2="0" stroke="black"></line>
    <circle cx="400" cy="50" r="35" fill="white" stroke="black"></circle>
    </svg>


[Se i SVG Viewer](https://www.svgviewer.dev/s/KOAGdP01)

Kan du utvide denne koden, eller din egen kode, slik at mønsteret også repeteres nedover? Du kan tenke deg at vi skal ha flere rader av figuren som er vist over. 

I denne oppgaven har vi sett hvordan vi kan bruke vektorgrafikk og Python til å *tegne med programmering*. Dette er spesielt nyttig når vi skal tegne repetitive mønstre eller mange figurer av samme type. Nå skal vi se på hvor effektivt man kan tegne mange figurer av samme type. 

***Tre på rad.*** Tenk deg at du ønsker å lage spillet *Tre på rad* for datamaskinen. For å tegne spillbrettet, kan vi kan ta utgangspunkt i [denne](https://www.svgviewer.dev/s/oRqxV7rg) *SVG*-koden. Vi skal lage en funksjon `draw_board(rows)` som kan gi *SVG*-koden til et hvilken som helst *Tre på rad*-stilling. Et eksempel på en stilling er:

```
my_rows = [[None, None, 'O'], [None, 'X', None], [None, None, None]]
```

Målet er at vi skal kunne kalle på funksjonen `draw_board(my_rows)`, og at den returnerer [denne](https://www.svgviewer.dev/s/mVIgHwu2) *SVG*-koden. Hvordan får vi til dette?

Først kan vi nummerere radene og kolonnene fra 0 til 2. *Tre på rad*-stillingen vi definerte ovenfor har:
* *O* på rad 0 og kolonne 2
* *X* på rad 1 og kolonne 1

Vi kan derfor begynne med å lage funksjoner som tegner *X* (*cross*) eller *O* (*nought*) på et bestemt kvadrat på brettet:


```python
size = 100

def svg_cross(row, col):
    line1 = [25, 25, 75, 75]
    line2 = [75, 25, 25, 75]
    move_x = col*size
    move_y = row*size
    line1 = move_line(line1, move_x, move_y)
    line2 = move_line(line2, move_x, move_y)
    svg = svg_line(line1) + svg_line(line2)
    return svg

def svg_nought(row, col):
    circle = [50, 50, 30]
    move_x = col*size
    move_y = row*size
    circle = move_circle(circle, move_x, move_y)
    svg = svg_circle(circle)
    return svg
```

Forklaring:
* Vi definerer først riktige koordinater for å tegne figuren på rad 0 og kolonne 0 (øverst til venstre.
* Deretter flytter vi figuren i x -og y-retning avhengig av koordinatene som er gitt. Dersom vi for eksempel ønsker å tegne på rad 1 og kolonne 2, må  vi flytte figuren $1\cdot 100$ i y-retning og $2\cdot 100$ i x-retning. Tallet 100 er bredden/høyden til et kvadrat på brettet.
* Merk at vi bruker funksjonene fra forrige oppgave for å flytte linjer og sirkler.

Nå kan vi lage funksjonen som tegner hele spillbrettet. Vi må først tegne rutenettet med fire linjer, og deretter gå gjennom alle cellene. For hver celle må vi sjekke om det skal plasseres *X* eller *O*, og bruke en av funksjonene ovenfor hvis ja. 

Dersom du ønsker en utfordring, kan du forsøke å programmere denne funksjonen selv!


```python
n = 3

def svg_board(rows):
    svg = '<svg height="300" width="300">\n'

    line1 = [0, 100, 300, 100]
    line2 = [0, 200, 300, 200]
    line3 = [100, 0, 100, 300]
    line4 = [200, 0, 200, 300]

    svg_grid = svg_line(line1) + svg_line(line2) + svg_line(line3) + svg_line(line4) 

    svg += svg_grid
    
    for r in range(n):
        for c in range(n):
            cell = rows[r][c]
            if cell == 'X':
                svg += svg_cross(r, c)
            elif cell == 'O':
                svg += svg_nought(r, c)
    
    svg += '</svg>'    

    return svg
```

Vi kan nå teste denne funksjonen på *Tre på rad*-stillingen vi definerte tidligere: 


```python
my_rows = [[None, None, 'O'], [None, 'X', None], [None, None, None]]
my_board = svg_board(my_rows)
print(my_board)
```

    <svg height="300" width="300">
    <line x1="0" y1="100" x2="300" y2="100" stroke="black"></line>
    <line x1="0" y1="200" x2="300" y2="200" stroke="black"></line>
    <line x1="100" y1="0" x2="100" y2="300" stroke="black"></line>
    <line x1="200" y1="0" x2="200" y2="300" stroke="black"></line>
    <circle cx="250" cy="50" r="30" fill="white" stroke="black"></circle>
    <line x1="125" y1="125" x2="175" y2="175" stroke="black"></line>
    <line x1="175" y1="125" x2="125" y2="175" stroke="black"></line>
    </svg>


[Se i SVG Viewer](https://www.svgviewer.dev/s/W0k9YANG)

Koden fungerer! Forhåpentligvis er du nå overbevist om at tegning med programmering kan være et svært effektivt verktøy! Når vi skal lage mange figurer av samme type, kan vi programmere en funksjon som genererer den riktige *SVG*-koden basert på en eller flere parametre. Tenk deg hvor tungvint det ville vært i et tegneprogram; du måtte ha laget en figur for hver eneste mulige stilling i *Tre på rad*!

Dersom du er mer interessert i vektorgrafikk og tegning med programmering, kan følgende kilder være nyttige: 

* [SVG Shapes](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Basic_Shapes): Forklarer de ulike formene som kan tegnes med *SVG*-kode.
* [drawsvg](https://github.com/cduck/drawsvg#readme): En Python-pakke som gjør det enklere å generere *SVG*-figurer med Python. Installer pakken med terminalkommandoen `python3 -m pip install "drawsvg~=2.0"`og bruk eksemplene gitt på siden for å komme i gang. Det kan være nyttig å programmere i en [Jupyter Notatbok](https://jupyter.org/) for å enkelt kunne se figurene du lager.  

