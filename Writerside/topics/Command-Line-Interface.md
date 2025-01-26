# Command Line Interface

## Wat is een CLI?

Een <tooltip term="cli">**CLI**</tooltip> wordt gebruikt door Linux servers.
Dit is een omgeving zonder een <tooltip term="gui">**GUI**</tooltip>.

Een **CLI** vraagt een stuk minder kracht van een computer en is ook **beter voor bepaalde taken als je het goed beheerst**.

## Structuur van een CLI

Een CLI is opgebouwd uit een aantal dingen:

De **username** van de gebruiker waar je mee ingelogd bent:
```bash
gebruiker@ubuntu:~$
^^^^^^^^^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format switcher-key="" color="#19191c" style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **computer** waarop je bent ingelogd:
```bash
gebruiker@ubuntu:~$
          ^^^^^^
```
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format switcher-key="" color="#19191c" style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Waar je bent** in het bestandssysteem:
```bash
gebruiker@ubuntu:~$
                 ^
```
<note>~ is de standaard locatie waar je na het inloggen terechtkomt.</note>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format switcher-key="" color="#19191c" style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Toont **welke rechten** je hebt. $ is voor standaard gebruiker rechten, # is voor de <tooltip term="root">root gebruiker</tooltip> rechten:
```bash
gebruiker@ubuntu:~$
                  ^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format switcher-key="" color="#19191c" style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**_Samengevat is het dus:_**
````plain text
Gebruiker op ubuntu in het home directory zonder root permissies.
^^^^^^^^^ ^^ ^^^^^^ ^^^^^^^^^^^^^^^^^^^^^ ^^^^^^^^^^^^^^^^^^^^^^
gebruiker  @ ubuntu:          ~                      $
````

## Commando's

**Commando's zijn stukjes tekst die je aan het systeem geeft**.\
Het systeem kijkt of die tekst overeenkomt met een commando dat het kent en voert dat commando uit.
````Bash
gebruiker@ubuntu:~$ ls
                    ^^
````

Het `ls` commando toont de bestanden en mappen die aanwezig zijn in de gegeven locatie, de huidige locatie tenzij anders aangegeven.
````Bash
gebruiker@ubuntu:~$ ls
bestand  map
````

Commando's hebben bijna altijd <tooltip term="argument">**argumenten**</tooltip> die je kan gebruiken om het gedrag van
het commando te beïnvloeden.\
Het argument `-a` toont *alles* in de gegeven locatie.
````Bash
gebruiker@ubuntu:~$ ls -a
.  ..  bestand  map  .verborgen_bestand
````

Argumenten kunnen er ook anders uit zien.\
Het commando `echo` herhaalt de tekst die het als argument mee krijgt.
````Bash
gebruiker@ubuntu:~$ echo hello world
hello world
````

**Soms heb je extra permissies nodig** om een commando uit te voeren. *Normaal mag je niet in de map `/root`.*
````Bash
gebruiker@ubuntu:~$ ls /root
ls: cannot ​open directory '/root': Permission denied
````

**In Linux gebruik je `sudo` om iets als administrator uit te voeren.**

````Bash
gebruiker@ubuntu:~$ sudo ls /root
[sudo] password ​for gebruiker: 
snap
````

**Je moet je eigen wachtwoord typen, je zal zien dat er niks op je scherm verandert. Dit is voor beveiliging,
je bent wel aan het typen**.

*Het commando `sudo` werkt alleen als je in de lijst staat van gebruikers die het mogen gebruiken.*

## Manpages

Nog een ander commando is `shutdown`.\
Dit commando zet de computer een minuut nadat het uitgevoerd is uit.\
**Om meer informatie te krijgen over het `shutdown` commando gebruik je `man`**.
````bash
gebruiker@ubuntu:~$ man shutdown
````

Door het commando `man` met het argument `shutdown` te gebruiken open je de **manual van het `shutdown` commando. 
Dit is de <tooltip term="manpage">manpage</tooltip>.**
````Plain Text
SHUTDOWN(8)                        shutdown                        SHUTDOWN(8)

NAME
       shutdown - Halt, power off or reboot the machine

SYNOPSIS

       shutdown [OPTIONS...] [TIME] [WALL...]

DESCRIPTION
       shutdown may be used to halt, power off, or reboot the machine.

       The first argument may be a time string (which is usually "now").
       ...
````

<tip>
    <p>Je kan de manpage navigeren via scrollen, pijltjestoetsen of de spatiebalk.</p>
    <p>
        Als je iets specifiek wilt zoeken kan je <shortcut>/</shortcut> typen gevolgd door wat je wilt vinden.
        Druk daarna op <shortcut>N</shortcut> voor het volgende resultaat, voor het vorige resultaat: <shortcut>Shift+N</shortcut>.
        <control>Om de manpage te sluiten druk je op <shortcut>q</shortcut>.</control>
    </p>
</tip>

In de tekst zie je dat je het argument `now` kan gebruiken bij `shutdown`.

Het commando `shutdown now` werkt als je rechtstreeks op de computer ingelogd bent, maar **wanneer je van afstand
ingelogd bent moet je sudo gebruiken**.

Er zijn **9 secties van manpages**, elk voor een andere categorie. **Sommige woorden kunnen meerdere keren voorkomen**,
maar zijn dan elk in een andere sectie.

Een voorbeeld van een woord dat meerdere keren voorkomt, is `passwd`:

````Bash
gebruiker@ubuntu:~$ apropos passwd
...
passwd (1)           - change user password
passwd (1ssl)        - OpenSSL application commands
passwd (5)           - the password ​file
...
````

**Om de juiste sectie te openen gebruik je `man 5 passwd`**, vervang het nummer met de juiste sectie.

## Handige commando's & shortcuts

<tabs>
    <tab title="whatis">
        Als je een <control>korte beschrijving van een commando</control> wilt kan je <code>whatis</code> gebruiken:
        <code-block lang="Bash">
            gebruiker@ubuntu:~$ whatis ls
            ls (1)               - list directory contents
        </code-block>
    </tab>
    <tab title="whereis">
        Als je wilt weten <control>waar een commando en de manpage er van is</control> kan je <code>whereis</code> gebruiken:
        <code-block lang="Bash">
            gebruiker@ubuntu:~$ whereis ls
            ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz
        </code-block>
    </tab>
    <tab title="history">
        Om de <control>commando's te zien die je vroeger hebt gebruikt</control> kan je <code>history 5</code> gebruiken, 5 kan je weglaten
        of vervangen door het aantal commando's dat je wilt zien.
        <code-block lang="Bash">
            gebruiker@ubuntu:~$ history 5
                47  man man
                48  clear
                49  ls
                50  whereis ls
                51  history 5
        </code-block>
    </tab>
    <tab title="!!">
    <p>
    Als je het <control>vorige commando opnieuw wilt gebruiken en iets wilt toevoegen</control> kan je <code>!!</code> typen:
    </p>
    <code-block lang="Bash">
        gebruiker@ubuntu:~$ ls /root
        ls: cannot ​open directory '/root': Permission denied
        gebruiker@ubuntu:~$ sudo !!
        sudo ls /root
        [sudo] password ​for gebruiker: 
        snap
    </code-block>
    </tab>
</tabs>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Shortcuts

<shortcut>🠕🠗</shortcut>: Pijltje omhoog of omlaag om het **vorige / volgende commando** te krijgen.

**<shortcut>Ctrl+C</shortcut>**: Vaak, maar niet altijd kan je deze gebruiken om een **commando te stoppen**.

**<shortcut>Tab</shortcut>**: Een **niet volledig getypt commando of pad vervolledigen**.

**<shortcut>Ctrl+R</shortcut>**: In de **geschiedenis van commands te zoeken**.

## Commando's & Terminologie

<table>
    <tr>
        <td>Commando</td>
        <td>Uitleg</td>
    </tr>
    <tr>
        <td>ls</td>
        <td>Toont de mappen, bestanden en andere informatie van een locatie.</td>
    </tr>
    <tr>
        <td>man</td>
        <td>Toont een handleiding van het gegeven commando, configuratiebestand...</td>
    </tr>
    <tr>
        <td>sudo</td>
        <td>Betekent officieel "substitute user, do", wordt gebruikt om een commando met root privileges uit te voeren.</td>
    </tr>
    <tr>
        <td>shutdown</td>
        <td>Sluit of herstart het systeem.</td>
    </tr>
    <tr>
        <td>apropos</td>
        <td>Zoekt in de manpages naar referenties van het argument en toont dan welke deze bevatten.</td>
    </tr>
    <tr>
        <td>whatis</td>
        <td>Toont een beschrijving van een manpage in één lijn.</td>
    </tr>
    <tr>
        <td>whereis</td>
        <td>Toont de locatie van een commando en de locatie van de manpage.</td>
    </tr>
    <tr>
        <td>history</td>
        <td>Toont een lijst van de commando's die hiervoor gebruikt werden.</td>
    </tr>
    <tr>
        <td>clear</td>
        <td>Haalt al de tekst van het scherm af.</td>
    </tr>
</table>

<table>
    <tr>
        <td>Term</td>
        <td>Uitleg</td>
    </tr>
    <tr>
        <td>CLI</td>
        <td>Command Line Interface, een manier om een computer of programma te gebruiken via alleen tekst.</td>
    </tr>
    <tr>
        <td>GUI</td>
        <td>Graphical User Interface, een manier om een computer of programma te gebruiken in een visuele omgeving.</td>
    </tr>
    <tr>
        <td>Argument</td>
        <td>Een argument geeft een waarde aan een commando waar dit commando iets mee kan doen.</td>
    </tr>
    <tr>
        <td>Manpage</td>
        <td>Een manual / handleiding van een commando, configuratie bestand... er zijn 9 secties met verschillende soorten manpages.</td>
    </tr>
</table>

## Studeren {collapsible="true"}

<deflist collapsible="true">
    <def title="Wat is een CLI?">
        <control>Command Line Interface</control>, een manier om een computer of programma te gebruiken via tekst.
    </def>
    <def title="Wat betekenen $ en # in een Linux CLI?">
        Het <control>$ teken betekent</control> dat je je <control>normale rechten</control> hebt, <control># betekent</control> 
        dat je de <control>rechten hebt van de root gebruiker</control>.
    </def>
    <def title="Wat betekent ~?">
        Het symbool ~ staat voor de <control>locatie van je home map</control>.
    </def>
    <def title="Wat doet ls -a?">
        <control>Toont alle mappen en bestanden</control> in de gegeven locatie.
    </def>
    <def title="Hoe open je de handleiding van passwd op sectie 5?">
        <code>man 5 passwd</code>
    </def>
    <def title="Met welk commando zie je de locatie van een commando?">
        Met het <code>whereis</code> commando.
    </def>
    <def title="Hoe sluit je het systeem onmiddellijk af als je van afstand ingelogd bent?">
        Met <code>sudo shutdown now</code>. Als je op de computer zelf bezig bent kan het zonder <code>sudo</code>.
    </def>
    <def title="Hoe zoek je naar een vorig gebruikt commando?">
        <shortcut>Ctrl+R</shortcut>, opnieuw drukken om naar het volgende resultaat te gaan.
    </def>
    <def title="Hoe vind je een specifiek woord in een manpage?">
        Door <shortcut>/</shortcut> te typen gevolgd door wat je zoekt. <shortcut>N</shortcut> gaat naar het volgende resultaat.
    </def>
    <def title="Wat doet het echo commando?">
        Het commando <code>echo</code> print de gegeven tekst op het scherm.
    </def>
</deflist>