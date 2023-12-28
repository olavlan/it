---
title: "Teikna med programmering"
belongs_to_chain: "Lagring av data"
figures_to_include:
---

I denne seksjonen skal me sjå på korleis ein kan teikna med programmering. Dette er ein seksjon som er ekstra interessert i vektorgrafikk, og korleis ein kan utvikla nyttige teikneverktøy der alt blir gjort med kode!

Me byrjar med ei oppgåve som du kan prøva deg på. Teikn eit mønster med sirklar og linjer, anten på eit ark eller i eit teikneprogram som *Paint*. Gå deretter inn på [*SVG Viewer*](https://www.svgviewer.dev/s/LfxtOdK1) og forsøk å laga det same mønsteret med *SVG*-kode.

Tenk at du no har lyst til å halda fram det same mønsteret utan å måtta skriva inn dei neste linjene og sirklane sjølv. Kan du laga eit Python-program som finn dei rette koordinatane, og deretter skriv ut *SVG*-koden til eit større bilete med same mønster?

Som hjelp kan du bruka funksjonane under. Først viser me korleis du kan teikna eit mønsteret éin gong. I vårt døme består mønsteret av to linjer og ein sirkel (sjå figuren i [*SVG Viewer*](https://www.svgviewer.dev/s/dnXrdjhk)):


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


[Sjå i SVG Viewer](https://www.svgviewer.dev/s/65R1QjCn)

No viser me korleis me kan repetera dette mønsteret fem gonger mot høgre. Til dette kan me laga funksjonar som flyttar linjer og sirklar ein viss avstand i x -eller y-retning (positiv x-retning er mot høgre, og positiv y-retning er nedover).


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

*Merk at desse funksjonane ikkje returnerer *SVG*-kode, men ei liste av verdiar for ei linje eller sirkel.*

No kan me skriva kode som teiknar linjene og sirklane fem gonger. Mellom kvar gong me teiknar dei, må me flytta dei 100 i x-retning, slik at me oppnår mønsteret me ønskjer oss.


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


[Sjå i SVG Viewer](https://www.svgviewer.dev/s/@@KOAGdP01)

Kan du utvida denne koden, eller din eigen kode, slik at mønsteret også blir repetert nedover? Du kan tenkja deg at me skal ha fleire rader av figuren som er vist over.

I denne oppgåva har me sett korleis me kan bruka vektorgrafikk og Python til å *teikna med programmering*. Dette er spesielt nyttig når me skal teikna repetitive mønster eller mange figurar av same type. No skal me sjå på kor effektivt ein kan teikna mange figurar av same type.

***Tre på rad.*** Tenk deg at du ønskjer å laga spelet *Tre på rad* for datamaskina. For å teikna spelebrettet, kan me kan ta utgangspunkt i [denne](https://www.svgviewer.dev/s/oRqxV7rg) *SVG*-koden. Me skal laga ein funksjon `draw_board(rows)` som kan gi *SVG*-koden til kva Tre som helst * på rad*-stilling. Eit døme på ei stilling er:

```
my_rows = [[None, None, 'O'], [None, 'X', None], [None, None, None]]
```

Målet er at me skal kunna kalla på funksjonen `draw_board(my_rows)`, og at han returnerer [denne](https://www.svgviewer.dev/s/mVIgHwu2) *SVG*-koden. Korleis får me til dette?

Først kan me nummerera radene og kolonnane frå 0 til 2. *Tre på rad*-stillinga me definerte ovanfor har:
* *O* på rad 0 og kolonne 2
* *X* på rad 1 og kolonne 1

Me kan derfor byrja med å laga funksjonar som teiknar *X* (*cross*) eller *O* (*nought*) på eit bestemt kvadrat på brettet:


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
* Me definerer først rette koordinatar for å teikna figuren på rad 0 og kolonne 0 (øvst til venstre.
* Deretter flyttar me figuren i x -og y-retning avhengig av koordinatane som er gitt. Dersom me til dømes ønskjer å teikna på rad 1 og kolonne 2, må  me flytta figuren $1\cdot 100$ i y-retning og $2\cdot 100$ i x-retning. Talet 100 er breidda/høgda til eit kvadrat på brettet.
* Merk at me bruker funksjonane frå førre oppgåve for å flytta linjer og sirklar.

No kan me laga funksjonen som teiknar heile spelebrettet. Me må først teikna rutenettet med fire linjer, og deretter gå gjennom alle cellene. For kvar celle må me sjekka om det skal plasserast *X* eller *O*, og bruka ein av funksjonane ovanfor viss ja.

Dersom du ønskjer ei utfordring, kan du prøva å programmera denne funksjonen sjølv!


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

Me kan no testa denne funksjonen på *Tre på rad*-stillinga me definerte tidlegare:


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


[Sjå i SVG Viewer](https://www.svgviewer.dev/s/W0k9YANG)

Koden fungerer! Forhåpentleg er du no overtydd om at teikning med programmering kan vera eit svært effektivt verktøy! Når me skal laga mange figurar av same type, kan me programmera ein funksjon som genererer den rette *SVG*-koden basert på ein eller fleire parametrar. Tenk deg kor tungvint det ville vore i eit teikneprogram; du måtte ha laga ein figur for kvar einaste moglege stilling i *Tre på rad*!

Dersom du er meir interessert i vektorgrafikk og teikning med programmering, kan følgjande kjelder vera nyttige:

* [SVG Shapes](https://developer.mozilla.org/en-us/docs/web/svg/tutorial/basic_shapes): Forklarer dei ulike formene som kan teiknast med *SVG*-kode.
* [drawsvg](https://github.com/cduck/drawsvg#readme): Ein Python-pakke som gjer det enklare å generera *SVG*-figurar med Python. Installer pakken med terminalkommandoen `python3 -m pip install "drawsvg~=2.0"`og bruk døma gitt på sidan for å komma i gang. Det kan vera nyttig å programmera i ein [Jupyter Notatbok](https://jupyter.org/) for å enkelt kunna sjå figurane du lagar.

