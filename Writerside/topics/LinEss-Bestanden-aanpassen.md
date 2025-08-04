# Bestanden en output aanpassen

Soms is de output van een bestand of commando niet helemaal hoe je het wilt.\
In dat geval kan je de inhoud of de output van het bestand of commando aanpassen.

## Inhoud aanpassen

In vorige hoofdstukken is **al uitgelegd hoe je `>` & `>>` kan gebruiken** in combinatie met commando's zoals `echo` om
de inhoud van een bestand aan te passen.

```
gebruiker@ubuntu:~$ echo "Dit is een test" > test.txt
gebruiker@ubuntu:~$ cat >> test.txt
Dit is een tweede regel
gebruiker@ubuntu:~$ cat test.txt
Dit is een test
Dit is een tweede regel
```

Dat is een **manier om kleine simpele stukjes tekst** toe te voegen aan een bestand.\
**Maar als je iets ingewikkelder wilt doen is het onhandig.**

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Zoals notepad op Windows bestaan er ook **tekstverwerkers voor de CLI in Linux**.\
**Een van de bekendste is `nano`.**

<note><p>Misschien heb je ook al gehoord van <code>vim</code>.</p>
<p>We gebruiken <control><code>vim</code> niet omdat deze moeilijk is</control> en <control><code>nano</code> meer dan 
genoeg kan</control>.</p></note>

Je kan `nano` gebruiken om **bestanden te bewerken en aan te maken**.

Een **bestand openen** en deze dan bewerken:\
*Als het bestand nog niet bestaat, wordt deze automatisch aangemaakt.*
```
gebruiker@ubuntu:~$ nano test.txt

GNU nano 7.2

1
2
3
hallo




                                                       [ New File ]
^G Help  ^O Write Out  ^W Where Is  ^K Cut    ^T Execute  ^C Location   ...
^X Exit  ^R Read File  ^/ Replace   ^U Paste  ^J Justify  ^- Go To Line ...
```

Hier kan je gewoon typen wat je wilt.\
`^` betekent de <shortcut>Ctrl</shortcut> toets. `M` betekent de <shortcut>Alt</shortcut> toets.\
Er zijn **enkele belangrijke shortcuts** die je kan gebruiken:

- <shortcut>Ctrl+s</shortcut>: Bestand opslaan
- <shortcut>Ctrl+x</shortcut>: Afsluiten
- <shortcut>Ctrl+k</shortcut>: Hele regel of geselecteerde tekst knippen
- <shortcut>Ctrl+u</shortcut>: Plakken
- <shortcut>Alt+u</shortcut>: Ongedaan maken
- <shortcut>Alt+e</shortcut>: Opnieuw doen
- <shortcut>Ctrl+g</shortcut>: Help
- <shortcut>Alt+m</shortcut>: Maakt het mogelijk om de muis te gebruiken

## Output aanpassen

Er zijn **veel commando's** die de **output** van een bestand **aanpassen**.

Om de **volledige onaangepaste output van een bestand** te zien kan je `cat` gebruiken.\
Een variant van `cat` is `tac`:

```
gebruiker@ubuntu:~$ tac test.txt
hallo
3
2
1
```

`tac` is `cat` maar dan **van onder naar boven**.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

<tabs>
<tab title="head">
<p><code>head</code> <control>toont de eerste 10 regels</control> van een bestand.</p>
<code-block>
gebruiker@ubuntu:~$ head lange_tekst.txt
1
2
3
4
...
</code-block>
<p>Je kan een <control>nummer als argument</control> geven om <control>dat aantal regels te tonen</control>.</p>
<code-block>
gebruiker@ubuntu:~$ head -2 lange_tekst.txt
1
2
</code-block>
</tab>
<tab title="tail">
<p><code>tail</code> <control>toont de laatste 10 regels</control> van een bestand.</p>
<code-block>
gebruiker@ubuntu:~$ tail lange_tekst.txt
45
46
47
48
...
</code-block>
<p>Je kan een <control>nummer als argument</control> geven om <control>dat aantal regels te tonen</control>.</p>
<code-block>
gebruiker@ubuntu:~$ tail -2 lange_tekst.txt
53
54
</code-block>
<p>Je kan ook <code>tail -f</code> gebruiken om de <control>laatste regels van een bestand</control> te zien 
<control>en nieuwe regels die toegevoegd worden</control>. Dit is handig voor bijvoorbeeld een <control>log bestand live
te volgen</control>.</p>
<code-block>
gebruiker@ubuntu:~$ tail -f lange_tekst.txt
</code-block>
</tab>
<tab title="less">
<p><code>less</code> <control>toont de inhoud van een bestand deel per deel.</control></p>
<p>Dit is wat er <control>gebruikt wordt als je een man page bekijkt</control>. Zo wordt <control>niet alle tekst
tegelijk op je scherm</control> gezet, kan je scrollen en woorden zoeken zoals bij de man pages.</p>
<code-block>
gebruiker@ubuntu:~$ less lange_tekst.txt
</code-block>
</tab>
<tab title="more">
<p><code>more</code> <control>toont de inhoud van een bestand deel per deel.</control></p>
<p>Dit is <control>soortgelijk aan <code>less</code></control>, maar <control>meer beperkt</control>.</p>
<p>Je kan <control>niet terug scrollen</control> en <control>deze is minder krachtig</control>.</p>
<code-block>
gebruiker@ubuntu:~$ more lange_tekst.txt
</code-block>
</tab>
</tabs>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### grep

Er zijn **verschillende commando's en technieken** om de **output** van een bestand te **filteren**.

Het commando `grep` is een van de bekendsten.\
<code>grep</code> <control>filtert de output</control> en <control>toont alleen de regels die overeenkomen
met de zoekterm</control>.

<code-block>
gebruiker@ubuntu:~$ grep "zoekterm" boek.txt
De zoekterm die hij gebruikte toen hij zijn vraag opzocht...
</code-block>
<p>Je <control>kan</control> het <control>ook gebruiken met een pipe</control>.</p>
<code-block>
gebruiker@ubuntu:~$ ls | grep "f"
file.txt
folder
</code-block>

Een aantal handige opties zijn:
- <code>-v</code>: <control>Toont de regels die niet overeenkomen met de zoekterm.</control>
- <code>-n</code>: <control>Toont het regelnummer van de gevonden regels.</control>
- <code>-c</code>: <control>Toont het aantal gevonden regels.</control>
- <code>-e</code>: <control>Kan meerdere keren gebruikt worden om extra zoektermen toe te voegen.</control>
- <code>-A1,B1,C1</code>: After, Before, Context. <control>Toont extra regels rond de gevonden regels.</control>
- <code>-E</code>: <control>Maakt het mogelijk om uitgebreide regex te gebruiken.</control>

<note><p>Zoals andere dingen in Linux is <code>grep</code> hoofdlettergevoelig.</p>
<p>Om dit te vermijden kan je <code>-i</code> gebruiken.</p></note>

### regex

Je kan ook <control>regex gebruiken</control> om <control>complexere zoekopdrachten te doen</control>.\
Regex is een <control>manier om patronen te zoeken in tekst</control>.

Regex werkt met **karakters die een specifieke betekenis** hebben.\
Hier zijn enkele **voorbeelden** van regex karakters:
- `*`: Matcht 0 of meer karakters.
- `+`: Matcht 1 of meer van het vorige karakter.
- `?`: Matcht 0 of 1 van het vorige karakter.
- `.`: Matcht elk karakter één keer.
- `|`: Of. Matcht het ene of het andere.
- `()`: Groepering. Matcht de tekst tussen de haakjes.
- `{n}`: Matcht precies n keer het vorige karakter.
- `[a-z]`: Matcht één karakter uit de opgegeven reeks (in dit geval een kleine letter in het alfabet).
- `^[0-9]`: Matcht een regel die begint met een cijfer.

**Voorbeelden:**
```
gebruiker@ubuntu:~$ grep -E "^[0-9]" boek.txt
# Toont regels die beginnen met een cijfer
gebruiker@ubuntu:~$ grep -E "[a-zA-Z]" boek.txt
# Toont regels die een kleine letter en daarna een hoofdletter bevatten
gebruiker@ubuntu:~$ grep "Hall*" boek.txt
# Toont regels waar "Hal" in staat en daarna 0 of meer "l" karakters staan
gebruiker@ubuntu:~$ grep "H." boek.txt
# Toont regels waar "H" in staat en daarna 1 willekeurig karakter
gebruiker@ubuntu:~$ grep -E "Hallo|Heyo" boek.txt
# Toont regels waar "Hallo" of "Heyo" in staat
gebruiker@ubuntu:~$ grep "H[a-z]?" boek.txt
# Toont regels waar "H" in staat en daarna 0 of 1 kleine letter
gebruiker@ubuntu:~$ grep "P{3}" boek.txt
# Toont regels waar "P" precies 3 keer in staat
gebruiker@ubuntu:~$ grep -E "H(allo|eyo)" boek.txt
# Toont regels waar "H" in staat en daarna "allo" of "eyo"
```

### Output filteren

<tabs>
<tab title="tee">
<p><code>tee</code> <control>leest de input en schrijft deze naar de output</control>.</p>
<p>Het is <control>anders</control> dan andere manieren om input te schrijven, want het <control>stuurt de 
<code>stdin</code> verder naar de <code>stdout</code>, waardoor je het kan gebruiken met pipes</control>.</p>
<code-block>
gebruiker@ubuntu:~$ tail -5 lange_tekst.txt | tee laatste_regels.txt | tail -2
53
54
gebruiker@ubuntu:~$ cat laatste_regels.txt
50
51
52
53
54
</code-block>
<p>Het is <control>ook handig als je <code>sudo</code> nodig hebt</control> voor naar een bestand te schrijven.</p>
<code-block>
gebruiker@ubuntu:~$ echo "Dit is een test" | tee /testfile
tee: /testfile: Permission denied
gebruiker@ubuntu:~$ echo "Dit is een test" | sudo tee /testfile
Dit is een test
gebruiker@ubuntu:~$ cat /testfile
Dit is een test
</code-block>
<p>Om <control>toe te voegen aan een bestand</control> in de plaats van te overschrijven kan je 
<control><code>-a</code> gebruiken</control>.</p>
</tab>
<tab title="cut">
<p>Het commando <code>cut</code> kan <control>output scheiden</control>.</p>
<code-block>
gebruiker@ubuntu:~$ cat tekst
1,2,3,4,5
6,7,8,9,10
11,12,13,14,15
gebruiker@ubuntu:~$ cut -d ',' -f1 tekst
1
6
11
</code-block>
<p>Hier is <code>-d ','</code> de "delimiter". Dat is het <control>punt waar de tekst opgesplitst wordt</control>.</p>
<p><code>-f1</code> zegt welk veld het moet tonen. In dit geval het eerste.</p>
</tab>
<tab title="sort">
<p>Het commando <code>sort</code> <control>kan output sorteren</control>.</p>
<code-block>
gebruiker@ubuntu:~$ cat tekst
3
1
2
4
5
gebruiker@ubuntu:~$ sort tekst
1
2
3
4
5
</code-block>
<p>Je kan het <control>ook met pipes</control> gebruiken.</p>
<code-block>
gebruiker@ubuntu:~$ ls | sort
file.txt
folder
test.txt
</code-block>
</tab>
<tab title="uniq">
<p>Het commando <code>uniq</code> <control>filtert dubbele regels uit de output</control>.</p>
<code-block>
gebruiker@ubuntu:~$ cat tekst
1
2
2
3
4
4
5
gebruiker@ubuntu:~$ uniq tekst
1
2
3
4
5
</code-block>
<p>Als de <control>dubbele regels niet naast elkaar</control> staan moet je eerst <code>sort</code> gebruiken.</p>
<code-block>
gebruiker@ubuntu:~$ cat tekst
1
2
3
2
4
5
4
gebruiker@ubuntu:~$ sort tekst | uniq
1
2
3
4
5
</code-block>
</tab>
<tab title="wc">
<p>Het commando <code>wc</code> <control>telt het aantal regels, woorden en karakters</control> in de output.</p>
<code-block>
gebruiker@ubuntu:~$ wc tekst
        7      10     40 tekst
gebruiker@ubuntu:~$ wc -l tekst
7 tekst
gebruiker@ubuntu:~$ wc -w tekst
10 tekst
gebruiker@ubuntu:~$ wc -c tekst
40 tekst
</code-block>
<p><code>-l</code> staat voor "lines", <code>-w</code> betekent "words" en <code>-c</code> is "characters".</p>
<p><control>Dit werkt natuurlijk ook met pipes.</control></p>
<code-block>
gebruiker@ubuntu:~$ ls | wc -l
3
</code-block>
<p>Zo kan je bijvoorbeeld het aantal bestanden en folders zien.</p>
</tab>
</tabs>

### Output veranderen

Het commando `tr` kan gebruikt worden om de **output te veranderen**.\
Het staat voor **"translate"** en kan gebruikt worden om **karakters te vervangen of te verwijderen**.

```
gebruiker@ubuntu:~$ echo "hallo wereld" | tr 'a' 'x'
hxllo wereld
```

Het werkt ook met **regex**.

```
gebruiker@ubuntu:~$ echo "hallo wereld" | tr 'a-z' 'A-Z'
HALLO WERELD
```

Je kan ook **meerdere karakters tegelijk vervangen**.

```
gebruiker@ubuntu:~$ echo "hallo wereld" | tr 'aeiou' 'AEIOU'
hAllO wErEld
```

Er zijn een paar handige argumenten die je kan gebruiken:
- `-d`: Verwijdert de opgegeven karakters.
- `-s`: Vervangt opeenvolgende karakters door één karakter.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Een ander commando dat je kan gebruiken is `sed`.\
Dit staat voor **"stream editor"** en kan gebruikt worden om **tekst te vervangen, toe te voegen of te verwijderen**.

```
gebruiker@ubuntu:~$ echo "hallo wereld" | sed 's/hallo/hey/'
hey wereld
```

Alleen het eerste voorkomen van "hallo" wordt vervangen.
Je kan ook alle voorkomen van "hallo" vervangen met de `g` optie:

```
gebruiker@ubuntu:~$ echo "hallo hallo wereld" | sed 's/hallo/hey/g'
hey hey wereld
```

Om `sed` hoofdletter ongevoelig te maken kan je de `i` optie toevoegen:

```
gebruiker@ubuntu:~$ echo "Hallo wereld" | sed 's/hallo/hey/i'
hey wereld
```
Je kan ook meerdere commando's tegelijk uitvoeren met `sed`:

```
gebruiker@ubuntu:~$ echo "hallo wereld" | sed -e 's/hallo/hey/' -e 's/wereld/aarde/'
hey aarde
```

De `d` optie kan gebruikt worden om regels te verwijderen:

```
gebruiker@ubuntu:~$ echo -e "hallo\nwereld" | sed '/wereld/d'
hallo
```

## Commando's & Terminologie

<table>
<tr>
    <td>Commando</td>
    <td>Uitleg</td>
</tr>
<tr>
    <td>nano</td>
    <td>Tekstverwerker voor de CLI.</td>
</tr>
<tr>
    <td>tac</td>
    <td>Toont de inhoud van een bestand van onder naar boven.</td>
</tr>
<tr>
    <td>head</td>
    <td>Toont de eerste 10 regels van een bestand.</td>
</tr>
<tr>
    <td>tail</td>
    <td>Toont de laatste 10 regels van een bestand.</td>
</tr>
<tr>
    <td>less</td>
    <td>Toont de inhoud van een bestand deel per deel.</td>
</tr>
<tr>
    <td>more</td>
    <td>Toont de inhoud van een bestand deel per deel, maar is minder krachtig dan less.</td>
</tr>
<tr>
    <td>grep</td>
    <td>Zoekt naar tekst in een bestand en toont de regels die overeenkomen.</td>
</tr>
<tr>
    <td>tee</td>
    <td>Leest de input en schrijft deze naar de output, kan gebruikt worden met pipes.</td>
</tr>
<tr>
    <td>cut</td>
    <td>Scheidt output op basis van een delimiter.</td>
</tr>
<tr>
    <td>sort</td>
    <td>Sorteert de output.</td>
</tr>
<tr>
    <td>uniq</td>
    <td>Filtert dubbele regels uit de output.</td>
</tr>
<tr>
    <td>wc</td>
    <td>Telt het aantal regels, woorden en karakters in de output.</td>
</tr>
<tr>
    <td>tr</td>
    <td>Vervangt of verwijdert karakters in de output.</td>
</tr>
<tr>
    <td>sed</td>
    <td>Vervangt, voegt toe of verwijdert tekst in de output.</td>
</tr>
</table>

<table>
<tr>
    <td>Term</td>
    <td>Uitleg</td>
</tr>
<tr>
    <td>Regex</td>
    <td>Een manier om patronen te zoeken in tekst.</td>
</tr>
<tr>
    <td>Delimiter</td>
    <td>Het punt waar de tekst opgesplitst wordt.</td>
</tr>
</table>

## Studeren {collapsible="true"}

<deflist collapsible="true">
<def title="Hoe sla je een bestand op in nano?">
    Met de shortcut <shortcut>Ctrl+s</shortcut>.
</def>

<def title="Hoe sluit je nano af?">
    Met de shortcut <shortcut>Ctrl+x</shortcut>.
</def>

<def title="Hoe bekijk je de inhoud van een bestand van onder naar boven?">
    Via het commando <code>tac</code>.
</def>

<def title="Welk commando toont de eerste 10 regels van een bestand?">
    Het commando <code>head</code>.
</def>

<def title="Welk commando wordt gebruikt als je een manpage opent?">
    Het commando <code>less</code>.
</def>

<def title="Hoe zoek je naar een specifiek woord in een bestand of output?">
    Met het commando <code>grep</code>.
</def>

<def title="Wat betekent [a-z] in regex?">
    Het matcht één karakter uit de opgegeven reeks (in dit geval een kleine letter in het alfabet).
</def>

<def title="Wat doet + in regex?">
    Het matcht 1 of meer van het vorige karakter.
</def>

<def title="Wat is het nut van het commando tee?">
    Het leest de input en schrijft deze naar de output, waardoor je het kan gebruiken met pipes en sudo.
</def>

<def title="Wat doet het commando cut?">
    Het scheidt output op basis van een delimiter.
</def>

<def title="Wat doet het commando sort?">
    Het sorteert de output.
</def>

<def title="Wat doet het commando uniq?">
    Het filtert dubbele regels uit de output.
</def>

<def title="Wat doet het commando wc?">
    Het telt het aantal regels, woorden en karakters in de output of in een bestand.
</def>

<def title="Wat doet het commando tr?">
    Het vervangt of verwijdert karakters in de output.
</def>

<def title="Wat doet het commando sed?">
    Het vervangt, voegt toe of verwijdert tekst in de output.
</def>

<def title="Wat doet sed met s/w/p/?">
    Het vervangt de eerste "w" in de regel met "p".
</def>
</deflist>
