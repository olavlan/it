---
title: "Objektorientert programmering"
belongs_to_chain: "Oppgavebibliotek"
figures_to_include:
---

**Når og kvifor brukast objektorientert programmering?**

**Aktivitet A.** Tenk deg at du skal laga følgjande program - ville du brukt prosedyreorientert eller objektorientert programmering? Grunngi valet.

1. Eit program som les ei fil med hastighetdata, og som bruker dette til å estimera distansen. Til dømes har du kanskje vore på sykkeltur og registrert farten kvart sekund med eit speedometer. Du ønskjer å vita omtrent kor langt du har sykla.
2. Eit program for eit bibliotek, som held oversikt over kva bøker som er tilgjengelege og kva for nokre av dei som er utlånte. Det skal vera mogleg å registrera utlån og innlevering.
3. Eit program som les ei fil med GPS-data for ein tur. Fila inneheld ei liste med koordinatar, som til dømes er registrerte kvart sekund. Programmet skal estimera lengda på turen, og dessutan estimera kor lenge ein var i rørsle og kor lenge ein tok pause.

**Prosjektoppgåve 1.** Kan du tenkja på eit program som du har lyst til å laga? Viss ja, beskriv kva funksjonar du ønskjer at programmet skal ha. Vurder deretter om prosedyreorientert eller objektorientert programmering er mest eigna, og grunngi svaret.

Dersom du kom fram til at prosedyreorientert programmering var mest eigna, forsøk å utvida idéen slik at det passar for objektorientert programmering.

*Vel ein idé som du synest verkar interessant, sjølv om det verkar for vanskeleg å koda! I dette kapittelet skal me berre planleggja programmet!*

---

**Kva er objekt?**

**Aktivitet A.** Sjå rundt deg og skriv ned nokre objekt.

1. Er nokon objekt innehaldne i andre eller knytte til på ein annan måte?
2. Kva kategoriar finst?
3. Finn objekt som er i ulike kategoriar, men som har noko til felles. Bruk dette til å laga større kategoriar. Gi meiningsfulle namn til dei større kategoriane.

**Aktivitet B.** Tenk deg at du skal starta opp ein butikk. Vel sjølv kva varer og/eller tenester du vil tilby. Du ønskjer no eit program for å halda oversikt over varebehaldning, forteneste og anna.

1. Skriv ein kravspesifikasjon, altså nokre setningar om kva funksjonar du ønskjer at programmet skal ha.
2. Teikn dei relevante objekta i eit diagram. Skil mellom ulik typar objekt, og få fram relasjonar mellom objekt (det er ikkje så viktig korleis du gjer det, så lenge det gir meining for deg og du kan forklara diagrammet).
3. Kva eigenskapar og handlingar har objekta?
4. Viss du manglar nokre handlingar frå kravspesifikasjonen, tenk over kva objekt handlingane blir gjorde på, og legg til desse objekta i modellen.

**Aktivitet C.** Under følgjer kravspesifikasjonar for nokon etterspurde program. For kvar av dei, svar på punkta 2-4 frå *Aktivitet B*.

* Eit hotell ønskjer eit program for å handtera rombestillingar. Programmet skal kunna sjekka om eit bestemt rom er ledig ein gitt periode og ta imot ei rombestilling. Me ønskjer også å kunna visa alle ledige rom ein gitt periode.
* Ein takeaway-restaurant ønskjer eit program for å halda oversikt over meny, behaldning av råvarer og bestillingar. Ein ønskjer å kunna visa tilgjengelege retter (basert på varebehaldning), og dessutan liste over råvarer som eventuelt manglar. Restauranten skal ta imot bestillingar frå klokka tre kvar dag, registrera når bestillingar blir fullførte, og kunne visa ei liste over gjenståande bestillingar.

**Prosjektoppgåve 2.** Ta utgangspunkt i *Prosjektoppgave 1* frå førre seksjon. Svar på alle spørsmåla i *Aktivitet B*, men for ditt eige prosjekt.

----

**Kva er ein klasse?**

**Aktivitet A.** Ta utgangspunkt i *Aktivitet B* frå førre seksjon. Sjå på objekta i modellen. Kva klassar kjem objekta frå? Teikn eit klassediagram etter dømet gitt i førre seksjon. Få med alle relevante datafelt og handlingar.

**Prosjektoppgåve 3.** Ta utgangspunkt i *Prosjektoppgave 2* frå førre seksjon og teikn eit klassediagram (som i aktiviteten over).

----

**Meir om objekt og klassar**

**Prosjektoppgåve 4.**

Ta utgangspunkt i *Prosjektoppgave 3* frå førre kapittel og gjer følgjande oppgåver:

1. Skriv opp nokre objekt som kjem frå klassane i klassediagrammet ditt (følg døma gitt i seksjonen *Skrivemåte for objekt*).
2. Gjer klassediagrammet meir detaljert ved å skriva datatypar på alle datafelt og metodar (følg døma gitt i seksjonen *Datatyper*). På metodane skal du skriva datatypen til returverdien.
3. Følg dømet i seksjonen *Objektdiagram og peikarar* til å teikna objekta frå punkt 1. Sørg for å få med peikarar mellom objekt!
4. Tenk over kva steg som må utførast for kvar av metodane i klassediagrammet. Kan du finna ein metode som krev fleire steg? Forsøk i så fall å dela opp denne metoden i delmetodar (følg dømet gitt i seksjonen *Oppdeling av metodar*).
5. Teikn eit flytdiagram for metoden i punkt 4 (følg dømet gitt i seksjonen *flytdiagram*).
6. Kan du laga ein metode som fungerer ved å senda meldingar til alle objekt? Her er nokre døme som kan vera til hjelp.
* Tenk at ein har klassane `Butikk` og `Vare`, og den sistnemnde har metoden `antall_dager_til_utgått()`. Då kan `Butikk` ha ein metode som listar alle varer som går ut om mindre enn éi veke.
* Tenk at ein har klassane `Videobibliotek` og `Video`, og den sistnemnde har metoden `komprimer_video()`. Då kan `Videobibliotek` ha ein metode som komprimerer alle videoane i biblioteket.
7. Vis korleis objekta i oppgåve 6 kommuniserer ved å følgja teikninga i seksjonen *Kommunikasjon mellom objekt*. Kva metode må vera offentleg for at kommunikasjonen skal vera mogleg?
8. Følg døma gitt i seksjonen *Konstruktører*, og definer minst éin konstruktør i kvar av klassane. Gjer klassediagrammet meir detaljert ved å leggja til konstruktørane, og dessutan å markera kva metodar som må vera offentlege. Marker datafelta og resten av metodane som private.
9. Vurder no om fleire av dei private metodane bør gjerast offentlege. Du må tenkja over om metoden berre skal brukast internt i eit objekt, eller om andre objekt skal kunna bruka metodane.
10. Følg dømet gitt i seksjonen *Dokumentasjon av metodar*; skriv ein dokumentasjon av alle metodar som du har valt å gjera offentlege.
11. Finn ut om ein av klassane dine har datafelt og metodar som kan leggjast i ein ny klasse. Gi eit passande namn til denne klassen og teikn den i diagrammet. Vis avhengnaden mellom dei to klassane etter oppdelinga (følg figurane i seksjonen *Oppdeling av klassar*).

----

**Arv**

**Prosjektoppgåve 5.** Ta utgangspunkt i klassediagrammet du har frå *Prosjektoppgave 4*. Finnes det to klassar som har både datafelt og metodar til felles? Viss ja, flote desse eigenskapane og metodane til ein superklasse, og gi denne eit passande namn. Teikn opp det nye klassediagrammet, der du også viser "arvar frå"-relasjonane mellom klassane.

----

**Klassar og objekt i Python**

**Prosjektoppgåve 6.** Ta utgangspunkt i det ferdige klassediagrammet du har frå prosjektoppgåvene i kapittelet *Konsepter i objektorientert programmering*. Gjer følgjande oppgåver:

1. Opprett éi Python-fil for heile prosjektet. Seinare skal me visa korleis me kan fordela koden i fleire filer, men på dette stadiet skal me ha all kode i éi fil.
2. Opprett klassen med éin konstruktør (følg dømet gitt i seksjonen *Setja inn ein konstruktør*.
3. Forsøk å laga ein metode som skriva ut ei setning om eit objekt frå klassen (følg dømet gitt i seksjonen *Setja inn metodar*).
4. Forsøk å oppretta nokre objekt frå klassen, og bruk metoden du laga i punkt 3 til å skriva ut ei setning om kvart av objekta. Denne koden kan du skriva under klasseblokka.
5. Gjenta steg 1-4 med alle dei andre klassane i klassediagrammet. Det skal vera ei fil for kvar klasse. Dersom nokon av klassane dine har fleire konstruktørar, kan du følgja dømet gitt i seksjonen *Setja inn fleire konstruktørar*. Dersom nokon av konstruktørane dine skal gjera fleire operasjonar, treng du ikkje å skriva kode for desse; du kan i staden laga ein funksjon som returnerer standardverdiar.

----

**Meir om klassar og objekt i Python**

**Prosjektoppgåve 7.** Ta utgangspunkt i klassediagrammet og Python-filene du har frå dei førre prosjektoppgåvene. Gjer følgjande oppgåver:

1. Definer alle metodar i dei rette klassane sine. Her treng du berre å skriva `return` i sjølve metodeblokka, men du skal sørgja for at metodane er riktig definerte med tanke på parametrar, og om metoden skal vera offentleg eller privat.
2. Dersom du har delmetodar, skal du no skriva kode i desse. Teikn gjerne figurar som vist i seksjonen *Delmetoder*, slik at du enkelt kan sjå kva metodar som er lurt å starta med. På dette stadiet treng ikkje delmetodane å returnera rette verdiar! Det er nok at delmetodane returnerer nokre testverdiar.
3. Skriv kode for resten av metodane. Når du skriv kode for ein metode som er oppdelt, er det viktig at du tek i bruk delmetodane. Hald fram med å bruka testverdiar når det er nødvendig. Forsøk å gjera koden så oversiktleg som mogleg, ved å dela den opp i nokre enkle steg.
4. Finnes kommunikasjon mellom objekt i koden? Finn i så fall kodelinjene der dette skjer.
6. Marker alle datafelt som private, og opprett offentlege *set*-metodar for dei datafelta som det skal vera mogleg å endra. Vurder om nokon av metodane bør sjekka at parameteren har ein gyldig verdi.
7. Opprett offentlege *get*-metodar for dei datafelta som det skal vera mogleg å henta. Hugs at dersom eit datafelt har eit muterbart objekt, så må du returnera ein kopi av objektet.
8. Skriv dokumentasjon av alle klassar og metodar ved å bruka *docstring*.
9. Har du nokon klassar som arvar frå ein superklasse? Kva endring må du gjera for at desse klassane arvar datafelta metodane til superklassen?
10. Opprett ei mappe for prosjektet ditt, og sørg for at kvar klasse er i sin eigen modul (si eiga fil). Kva for ei ekstra fil må du oppretta for at prosjektet ditt skal bli ein pakke?
11. Overskriv metoden `__str__()` i kvar av klassane dine, og sørg for at denne returnerer ein streng som gir ei skildring av objektet.
12. Opne kommandolinja og importar modulane frå pakken din. Opprett objekt, minst eitt objekt frå kvar klasse. Forsøk å skriva ut objekta. Test alle dei offentlege metodane som objekta dine tilbyr, og skriv ut resultata. Er utskriftene som forventa?
13. Dersom utskfriftene ikkje er som forventa, bruk `pdb` til finna ut kvar feilen skjer, og rett programmet.
