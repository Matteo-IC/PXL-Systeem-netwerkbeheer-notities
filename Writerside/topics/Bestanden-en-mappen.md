# Bestanden en mappen

## Bestandsstructuur

**De bestandsstructuur van Linux is anders dan in Windows.**

**Linux begint met een <shortcut>/</shortcut>.**\
Windows begint meestal met `C:\`.

**In Linux zijn hoofdletters belangrijk**, `File` is niet hetzelfde als `file`.\
In Windows maakt het niet uit of karakters hoofdletters zijn of niet.

**Bestanden in Linux moeten niet een bestandsextensie hebben** (.txt, .docx...) 
maar het **is wel goed om te gebruiken**.\
Windows heeft wel bestandsextensies nodig.

<warning>Linux gebruikt <shortcut>/</shortcut>, Windows gebruikt de andere <shortcut>\</shortcut> !</warning>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

In Linux heb je een **aantal mappen en bestanden die standaard bestaan**.\
*Een visualisatie van een aantal standaard mappen en bestanden:*

<img src="ubuntu-hierarchy(2).svg" alt="This image has light and dark versions" height="850" border-effect="rounded"/>

*Om een algemeen (niet ubuntu specifiek) overzicht te krijgen van de standaard bestandsstructuur 
kan je `man file-hierarchy` gebruiken.*

## Absolute paden

Een absoluut pad is het **volledige pad naar een map of bestand** van begin tot einde.

Het **absoluut pad naar de home map** van de gebruiker:
```Plain Text
/home/gebruiker/
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Het begin, de **eerste map** genaamd root map:
```Plain Text
/home/gebruiker/
^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **map "home"**, hier staan de home mappen van gebruikers:
```Plain Text
/home/gebruiker/
 ^^^^^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **home map van een gebruiker**, dit is `~`, waar de gebruiker staat na het inloggen:
```Plain Text
/home/gebruiker/
      ^^^^^^^^^^
```

## Relatieve paden

Een relatief pad is het **pad naar een map of bestand vanuit waar je bent**.

Het relatieve **pad vanuit de home map naar een andere map met een bestand**:
````Plain Text
gebruiker@ubuntu:~$ map/bestand
                    ^^^^^^^^^^^
````

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Het **absolute pad naar dit bestand** zou zijn:
````Plain Text
/home/gebruiker/map/bestand
````

<note>
<p>In het bestandssysteem van Linux staat er in elke map een `.` en `..`.</p>
<p><control>De `.` staat voor de huidige map en `..` staat voor de map daarboven.</control></p>
</note>


## Commando's

### Navigatie

<tabs>
<tab title="cd">
    <p>Om door het systeem te navigeren moet je je kunnen <control>verplaatsen</control>.</p>
    <p><control>Dit gaat met het <code>cd</code> commando:</control></p>
    <code-block>
    gebruiker@ubuntu:~$ cd map/
    gebruiker@ubuntu:~/map$
    </code-block>
    <p>Dit commando neemt een <control>relatief of absoluut pad als argument.</control></p>
    <p>Als <control>geen argument</control> gegeven is, ga je <control>terug naar je home map:</control></p>
    <code-block>
    gebruiker@ubuntu:~/map$ cd /usr/bin
    gebruiker@ubuntu:/usr/bin$ cd
    gebruiker@ubuntu:~$ 
    </code-block>
    <note>
    <p>Als je <code>cd ..</code> gebruikt ga je naar de map boven de huidge.</p>
    <p><code>cd -</code> brengt je terug naar de vorige map.</p>
    </note>
</tab>
<tab title="ls">
    <p>Om je te kunnen navigeren moet je <control>weten wat er is.</control></p>
    <p>Dat is wat het <code>ls</code> commando doet:</p>
    <code-block>
    gebruiker@ubuntu:~/map$ ls
    bestand  map2
    </code-block>
    <p><control>Je kan een pad geven en <code>-a</code> om alles te zien</control> in die locatie.</p>
    <code-block>
    gebruiker@ubuntu:/usr/bin$ ls -a /home/gebruiker/map/
    .  ..  bestand  map2  .verborgen_bestand
    </code-block>
</tab>
<tab title="pwd">
    <p>Het <code>pwd</code> commando <control>toont de huidige locatie</control>.</p>
    <code-block>
    gebruiker@ubuntu:~$ pwd
    /home/gebruiker
    </code-block>
</tab>
<tab title="tree">
    <p>Het commando <code>tree</code> <control>toont mappen en bestanden in en onder de huidige locatie</control>.</p>
    <code-block>
    gebruiker@ubuntu:~/map$ tree
    .
    ├── bestand
    └── map2
        └── bestand2
    </code-block>
    <p><code>tree</code> accepteert <code>-a</code> en een pad ook. <code>-L 1</code> zegt hoe ver het moet gaan.</p>
</tab>
<tab title="find">
    <p>Het commando <code>find</code> kan je gebruiken om in het <control>bestandssysteem dingen te vinden</control>.</p>
    <code-block>
    gebruiker@ubuntu:~$ find -name "bestand"
    ./map/bestand
    </code-block>
    <p>
    <control>Linux is hoofdletter gevoelig.</control> Om te zoeken zonder hoofdletter gevoeligheid gebruik je <code>find -iname</code>
    </p>
    <p>
    <control><code>find</code> begint standaard vanuit de huidige map</control> en gaat zo verder.
    Je kan het een pad geven om daar te beginnen. 
    </p>
    <p>
    Je moet hier <control>soms <code>sudo</code> gebruiken</control> als het wil zoeken in een map waar meer permissies nodig zijn.
    </p>
    <code-block>
    gebruiker@ubuntu:~$ sudo find / -iname "bestand"
    </code-block>
</tab>
<tab title="locate">
    <p>Het commando <code>locate</code> kan je ook gebruiken om <control>dingen te vinden</control>.</p>
    <p>Dit commando gebruikt een <tooltip term="database">database</tooltip> waar het in zoekt.</p>
    <p>Het is <control>sneller dan <code>find</code> maar je moet wel de database updaten om nieuwe dingen te vinden</control>.</p>
    <code-block>
    gebruiker@ubuntu:~$ sudo updatedb
    gebruiker@ubuntu:~$ locate bestand
    /home/gebruiker/map/bestand
    </code-block>
    <p><code>-i</code> maakt het niet hoofdletter gevoelig en <code>-b</code> toont geen map namen.</p>
</tab>
<tab title="file">
    <p>
    Omdat we niet altijd bestandsextensies hebben is het commando <code>file</code> 
    handig om <control>bestanden te identificeren</control>.
    </p>
    <code-block>
    gebruiker@ubuntu:~$ file map/text_bestand 
    map/text_bestand: ASCII text
    </code-block>
</tab>
<tab title="cat">
    <p>
    Als je de <control>inhoud van een bestand wilt zien</control> kan je het commando <code>cat</code> gebruiken.
    </p>
    <code-block>
    gebruiker@ubuntu:~$ cat text_bestand 
    text
    </code-block>
</tab>
</tabs>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Aanpassingen

<tabs>
<tab title="mv">
    <p>Het commando <code>mv</code> wordt gebruikt om <control>bestanden of mappen te verplaatsen</control>.</p>
    <code-block>
    gebruiker@ubuntu:~$ mv bestand2 /tmp/
    </code-block>
    <p>Het kan ook gebruikt worden om een <control>map of bestand een nieuwe naam te geven</control>.</p>
    <code-block>
    gebruiker@ubuntu:~$ mv betsand2 bestand2
    </code-block>
</tab>
<tab title="cp">
    <p>Het commando <code>cp</code> <control>kopieert een bestand of map</control> naar een locatie.</p>
    <code-block>
    gebruiker@ubuntu:~$ cp bestand /tmp/
    </code-block>
    <p><control>Standaard kopieert <code>cp</code> niet de mappen die in de gekopieerde map zitten.</control></p>
    <p>Om dit toch te doen kan je het argument <code>-r</code> gebruiken.
    Dit staat voor <tooltip term="recursief">recursief</tooltip>.
    </p>
    <code-block>
    gebruiker@ubuntu:~$ cp -r map/ /tmp/
    </code-block>
</tab>
<tab title="rename">
    <p>
    Als je meerdere <control>bestanden of mappen tegelijk wilt hernoemen</control> kan je het <code>rename</code> commando gebruiken.
    </p>
    <code-block>
    gebruiker@ubuntu:~$ rename 's/bestand/file/' *
    </code-block>
    <p>
    Het gedeelte <control><code>'s/bestand/file/'</code> is een argument.</control>
    </p>
    <p>
    Het <code>'</code> gedeelte zegt dat het als <tooltip term="string">string</tooltip> geïnterpreteerd moet worden.
    </p>
    <p><code>s/</code> staat voor substitutie.</p>
    <p><code>bestand/</code> is de tekst die hernoemd wordt.</p>
    <p><code>file/</code> is wat het moet worden.</p>
    <p><control><code>*</code> is het tweede argument</control>, het betekent dat alles hernoemd kan worden.</p>
    <note>
    <p>Dit maakt gebruik van regex, een manier om patronen te beschrijven met tekst.</p>
    <p><code>*</code> betekent <control>niks of alles</control>.</p>
    <p>
    In deze context betekent het dus dat alles hernoemd kan worden.
    Niet alles wordt hernoemd want niet alles heeft "bestand" in de naam.
    Hier komt in volgende hoofdstukken meer uitleg over.
    </p>
    </note>
</tab>
<tab title="rm">
    <p>Om <control>bestanden of mappen te verwijderen</control> kan je het <code>rm</code> commando gebruiken.</p>
    <code-block>
    gebruiker@ubuntu:~$ rm bestand
    </code-block>
    <p><code>-d</code> moet je gebruiken om lege mappen te verwijderen.</p>
    <p><code>-r</code> moet je gebruiken om mappen en hun inhoud te verwijderen.</p>
    <p><code>-f</code> moet je gebruiken als het vraagt voor bevestiging of als je niet de juiste rechten hebt.</p>
</tab>
<tab title="touch">
    <p>Om één of meer <control>bestanden te maken</control> kan je het <code>touch</code> commando gebruiken.</p>
    <code-block>
    gebruiker@ubuntu:~$ touch bestand bestand2
    </code-block>
    <p>Als er een spatie in de bestandsnaam is moet je de naam tussen '' zetten. Zo wordt het als één stuk tekst gezien.</p>
</tab>
<tab title="mkdir">
    <p>Om <control>een map te maken</control> kan je het <code>mkdir</code> commando gebruiken.</p>
    <code-block>
    gebruiker@ubuntu:~$ mkdir map
    </code-block>
    <p>Je kan ook een pad maken met meerdere mappen. Dan moet je <code>-p</code> gebruiken.</p>
</tab>
</tabs>

## Commando's & Terminologie

<table>
    <tr>
        <td>Commando</td>
        <td colspan="6">Argumenten</td>
        <td>Uitleg</td>
    </tr>
    <tr>
        <td>cd</td>
        <td colspan="2" href="#commando-s" summary="">
            <a href="#commando-s" summary="Brengt je terug naar de vorige locatie.">-</a>
        </td>
        <td colspan="2">
            <a href="#commando-s" summary="Ga één folder omhoog.">..</a>
        </td>
        <td colspan="2"><a href="#commando-s" summary="Geef een pad om naar toe te gaan.">Pad naar map</a></td>
        <td>Verandert je locatie in het bestandssysteem. Gaat naar de home map als geen argument gegeven is.</td>
    </tr>
    <tr>
        <td>ls</td>
        <td colspan="3"><a href="#commando-s" summary="Toont alles, zoals verborgen bestanden.">-a</a></td>
        <td colspan="3"><a href="#commando-s" summary="Geef een pad om de inhoud te tonen.">Pad naar map</a></td>
        <td>Toont wat er in de gegeven locatie is. Zonder pad toont het de dingen in de huidige locatie.</td>
    </tr>
    <tr>
        <td>pwd</td>
        <td colspan="6"></td>
        <td>Toont het pad naar de huidige locatie.</td>
    </tr>
    <tr>
        <td>tree</td>
        <td colspan="2"><a href="#commando-s" summary="Toont alles, zoals verborgen bestanden.">-a</a></td>
        <td colspan="2"><a href="#commando-s" summary="Zegt hoe ver het moet tonen, -L 2 om 2 mappen ver te gaan.">-L</a></td>
        <td colspan="2"><a href="#commando-s" summary="Geef een pad om van te beginnen.">Pad naar map</a></td>
        <td>Toont de bestanden en mappen in de gegeven locatie.</td>
    </tr>
    <tr>
        <td>find</td>
        <td colspan="2"><a href="#commando-s" summary="Zegt wat het moet zoeken.">-name</a></td>
        <td colspan="2"><a href="#commando-s" summary="Zegt dat hoofdletters niet uitmaken tijdens het zoeken.">-iname</a></td>
        <td><a href="#commando-s" summary="Een stuk tekst dat definieert wat het moet vinden.">Patroon</a></td>
        <td><a href="#commando-s" summary="Zegt waar het moet beginnen met zoeken.">Pad naar map</a></td>
        <td>Vindt dingen in het bestandssysteem.</td>
    </tr>
    <tr>
        <td>locate</td>
        <td colspan="3"><a href="#commando-s" summary="Maakt het zoeken niet hoofdletter gevoelig.">-i</a></td>
        <td colspan="3"><a href="#commando-s" summary="Toont mappen niet als resultaat.">-b</a></td>
        <td>Vindt dingen in het bestandssysteem via een <tooltip term="database">database</tooltip>.</td>
    </tr>
    <tr>
        <td>file</td>
        <td colspan="6"><a href="#commando-s" summary="Toont het type bestand van die locatie.">Pad naar bestand</a></td>
        <td>Toont wat voor een soort bestand het is.</td>
    </tr>
    <tr>
        <td>cat</td>
        <td colspan="6"><a href="#commando-s" summary="Toont de inhoud van het bestand op die locatie.">Pad naar bestand</a></td>
        <td>Toont de inhoud van een bestand.</td>
    </tr>
    <tr>
        <td>mv</td>
        <td colspan="6">
        <a href="#commando-s" summary="Paden naar waar het bestand of map verplaatst of hernoemd moet worden.">
        Paden naar bestanden of mappen</a>
        </td>
        <td>Verplaatst of hernoemd een bestand of map.</td>
    </tr>
    <tr>
        <td>cp</td>
        <td colspan="3"><a href="#commando-s" summary="Kopieer ook de mappen in de gegeven map.">-r</a></td>
        <td colspan="3">
        <a href="#commando-s" summary="Van waar en waarnaartoe het bestand of map moet.">
        Paden naar bestanden of mappen</a>
        </td>
        <td>Kopieert een bestand of map naar een locatie.</td>
    </tr>
    <tr>
        <td>rename</td>
        <td colspan="3"><a href="#commando-s" summary="Definieert het patroon dat het moet vervangen en met wat.">Regex</a></td>
        <td colspan="3"><a href="#commando-s" summary="Zegt welke mappen en bestanden het kan hernoemen.">Regex</a></td>
        <td>Verandert de naam van meerdere mappen en / of bestanden.</td>
    </tr>
    <tr>
        <td>rm</td>
        <td colspan="2"><a href="#commando-s" summary="Om een map te verwijderen als die leeg is.">-d</a></td>
        <td colspan="2"><a href="#commando-s" summary="Om mappen met inhoud te verwijderen.">-r</a></td>
        <td colspan="2"><a href="#commando-s" summary="Forceer het verwijderen.">-f</a></td>
        <td>Verwijder mappen en bestanden.</td>
    </tr>
    <tr>
        <td>touch</td>
        <td colspan="6"><a href="#commando-s" summary="Het bestand om te maken.">Bestand</a></td>
        <td>Maakt één of meerdere bestanden aan.</td>
    </tr>
    <tr>
        <td>mkdir</td>
        <td colspan="6"><a href="#commando-s" summary="Maakt hele paden aan.">-p</a></td>
        <td>Maakt een map.</td>
    </tr>
</table>

## Studeren {collapsible="true"}

<deflist collapsible="true">
<def title="Zijn hoofdletters in Linux belangrijk?">
    Ja, in Linux zijn <control>hoofdletters anders dan gewone letters</control>.
</def>
<def title="Is /home een relatief pad?">
    Nee, dit is een absoluut pad.
</def>
<def title="Wat doet pwd?">
    Toont de huidige locatie.
</def>
<def title="Wat doet het file commando?">
    Identificeert bestanden.
</def>
<def title="Wat doet: rename s/bestand/file/ *.txt">
    Verandert de naam van alle bestanden die op .txt eindigen en "bestand" in hun naam hebben.
</def>
<def title="Wat doet mkdir map/anderemap/nogeenmap?">
    Het geeft een error, dit gaat niet zonder het -p argument.
</def>
</deflist>