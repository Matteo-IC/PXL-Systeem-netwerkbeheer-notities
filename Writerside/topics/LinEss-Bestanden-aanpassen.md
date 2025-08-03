# Bestanden aanpassen

Soms is de inhoud van een bestand niet helemaal hoe je het wilt.\
In dat geval kan je de inhoud of de output van een bestand aanpassen.

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
gebruiker@ubuntu:~$ grep -E "Hall*" boek.txt
# Toont regels waar "Hal" in staat en daarna 0 of meer "l" karakters staan
gebruiker@ubuntu:~$ grep -E "H." boek.txt
# Toont regels waar "H" in staat en daarna 1 willekeurig karakter
gebruiker@ubuntu:~$ grep -E "Hallo|Heyo" boek.txt
# Toont regels waar "Hallo" of "Heyo" in staat
gebruiker@ubuntu:~$ grep -E "H[a-z]?" boek.txt
# Toont regels waar "H" in staat en daarna 0 of 1 kleine letter
gebruiker@ubuntu:~$ grep -E "P{3}" boek.txt
# Toont regels waar "P" precies 3 keer in staat
gebruiker@ubuntu:~$ grep -E "H(allo|eyo)" boek.txt
# Toont regels waar "H" in staat en daarna "allo" of "eyo"
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

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
<tab title="">

</tab>
</tabs>