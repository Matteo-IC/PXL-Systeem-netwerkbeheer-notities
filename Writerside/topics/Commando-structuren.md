# Commando structuren

**Commando's** die je typt **worden geïnterpreteerd door de <tooltip term="shell">shell</tooltip>**.

De **standaard shell in Ubuntu is bash**, kort voor **Bourne Again SHell**.

## Commando interpretatie

Bash interpreteert soms tekst op een andere manier dan bedoeld is.
```
gebruiker@ubuntu:~$ echo Veel         spaties
Veel spaties
```

Om te **zorgen dat bash specifieke karakters niet fout interpreteert** hebben we **3 opties**:

1. Voor het karakter een **`\`** zetten.
   1. Een `\` **zorgt dat bash** het **karakter erna ziet als dat karakter** en niet er iets mee doet.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

2. `"` gebruiken.
   1. Als je **tekst tussen `"` zet dan wordt die tekst als <tooltip term="string">string</tooltip> gezien**.
   2. Sommige karakters worden nog steeds geïnterpreteerd.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

3. `'` gebruiken.
   1. Tekst tussen `'` wordt ook als string gezien, maar **geen enkel karakter wordt geïnterpreteerd**.

## Aliassen

Een alias is een **stuk tekst dat door Bash als een ander stuk tekst wordt geïnterpreteerd**.

Aliassen kan je zelf instellen:
```
gebruiker@ubuntu:~$ alias rm='rm -i'
gebruiker@ubuntu:~$ alias show='tree -a -L 1'
```

In het voorbeeld wordt er de optie `-i` toegevoegd om standaard altijd voor bevestiging te vragen voor het verwijderen.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Een **alias verwijderen kan via het `unalias` commando**.
```
gebruiker@ubuntu:~$ unalias rm
gebruiker@ubuntu:~$ unalias show
```

<note>
    <control>Aliassen worden niet opgeslagen</control>, als je ze wilt <control>blijven gebruiken</control>
    moet je het <control>bestand `.bash_aliases` maken in je home map en daar de aliassen in zetten</control>.
</note>

## File globbing

File globbing is **het gebruik van patronen in bestandsnamen** om zo bepaalde bestanden te verkrijgen.

Het tonen van alle bestanden waar een `l` in staat:
```
gebruiker@ubuntu:~$ ls *l*
file  file1  file4  file45  file5  file9.txt  file.txt  filexyz  fileXYZ
```
`*l*` toont **alle bestanden** waar er **iets of niks voor of na de `l`** staat.

```
gebruiker@ubuntu:~$ ls f*
file  file1  file4  file45  file5  file9.txt  file.txt  filexyz  fileXYZ
```
`f*` toont de bestanden waar er **iets of niks na de `f`** staat.

Het `*` karakter selecteert **alles of niks**, als het achter een karakter staat selecteert het alles na dat karakter.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### ?

Met het `?` karakter kan je **één karakter selecteren**.
```
gebruiker@ubuntu:~$ ls file?
file1  file4  file5
```

Dit is zoals `*` maar het **kan maar één karakter selecteren en er moet een karakter zijn**.
```
gebruiker@ubuntu:~$ ls file???
filexyz  fileXYZ
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### []

Met `[]` kan je zoals `?` één karakter selecteren. Het verschil is dat je **in `[]` karakters kan specifiëren**.
```
gebruiker@ubuntu:~$ ls file[14]
file1  file4
```

Dit betekent "**alles wat met `file` begint en dan een `1` of `4` heeft met verder niks**".

**Je kan ook een bereik gebruiken met `[]`:**
```
gebruiker@ubuntu:~$ ls file[a-z]*
filexyz
```

Dit gaat ook met nummers:
```
gebruiker@ubuntu:~/map2$ ls file[0-9]
file1  file4  file5
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### File globbing voorkomen

*Als je een bestand hebt met de naam "file\*" en dat wilt verwijderen, verwijder je alle bestanden die starten met "file".*\
**Je kan dus `"`, `'` en `\` gebruiken om dit te voorkomen.**
```
gebruiker@ubuntu:~/map2$ rm "file*"
```

## Input & Output

**De shell heeft 3 streams.**\
Een stream is een categorie voor een bepaald soort tekst in de shell.

<img src="streams-diagram(1).svg" alt="streams visualized" width="600"/>

De stream **stdin** betekent **"standard input"**, dit is de **tekst die de Bash shell als invoer neemt**.
```
gebruiker@ubuntu:~$ ls /
                    ^^ ^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De stream **stdout** betekent **"standard output"**, dit is de **tekst die op ons scherm verschijnt als iets succesvol is**.
```
gebruiker@ubuntu:~$ ls /
bin                home               mnt   sbin.usr-is-merged  usr
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
...
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De stream **stderr** betekent **"standard error"**, dit is de **tekst die op ons scherm verschijnt als er een error is**.
```
gebruiker@ubuntu:~$ ls /root
ls: cannot open directory '/root': Permission denied
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

### I/O redirection

Alle **streams hebben een nummer**. Dit kan gebruikt worden in commando's om **streams om te leiden**.

**Om streams om te leiden gebruikt men `>`** in combinatie met het juiste nummer.
```
gebruiker@ubuntu:~$ ls / 1> file
```

Zonder `1> file` zou stdout gewoon de bestanden en mappen tonen.

**Met `1> file` zeggen we dat stdout naar het bestand `file` moet.**

<note>
   <p>Je moet niet <code>1></code> gebruiken om stdout om te leiden, standaard werkt <code>></code> ook.</p>
   <p>Standaard betekent <code>></code> eigenlijk <code>1></code>.</p>
</note>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **stderr** stream kan omgeleid worden **via `2>`**.
```
gebruiker@ubuntu:~$ ls /root 2> /dev/null
```

<tip>
We kunnen naar /dev/null proberen te schrijven. Het programma dat wil schrijven krijgt een bevestiging dat het
gelukt is, maar er wordt nooit iets geschreven. Dit is wat /dev/null doet.
</tip>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Om **stderr en stdout elk** om te leiden **naar een ander bestand** kan je ze combineren:
```
gebruiker@ubuntu:~$ find / > found 2> errors
```
Om **stderr en stdout naar hetzelfde bestand** om te leiden kan je:
```
gebruiker@ubuntu:~$ find / &> found_and_errors
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Om **toe te voegen en niet te vervangen** kan je **`>>`** gebruiken.
```
gebruiker@ubuntu:~$ ls /root 2>> file
```

<note>
   Het <control><code>></code> symbool verwijdert de inhoud</control> van het bestand waar het naar gaat schrijven.
   Het <control>verwijderen gebeurt voor het uitvoeren van het commando</control> waarvan de output geschreven wordt. 
   Dit betekent dat <control>als het commando faalt er niks wordt geschreven en de inhoud van het bestand weg is</control>.
</note>

### Bestanden

Je kan **met `>` gemakkelijk bestanden maken**:
```
gebruiker@ubuntu:~$ > file
```

Om inhoud in bestanden te zetten kan je gebruik maken van `echo` en `cat`:
```
gebruiker@ubuntu:~$ echo hallo > file2
gebruiker@ubuntu:~$ cat file2
hallo
gebruiker@ubuntu:~$ cat > file2
woppa
gebruiker@ubuntu:~$ cat >> file2
hoppa
gebruiker@ubuntu:~$ cat file2
woppa
hoppa
```

Als je `cat` gebruikt kan je typen en daarna <shortcut>Ctrl+d</shortcut> gebruiken om te stoppen met typen.

## Control Operators

**Meerdere commando's kunnen op dezelfde lijn gezet worden via `;`.** Bash wacht met het uitvoeren van een commando tot het 
vorige commando voltooid is.
```
gebruiker@ubuntu:~/map$ mkdir map; cd map; > file; ls
file
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Met `;` maakt het niet uit wat er gebeurde met het vorige commando, als het gedaan is, gebeurt de volgende.\
Als je **`&&` gebruikt moet het vorige commando succesvol zijn**.
```
gebruiker@ubuntu:~/map$ > file2 && ls && cd does_not_exist && echo yep
file  file2
bash: cd: does_not_exist: No such file or directory
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Je kan met `||` het volgende commando uitvoeren als het commando ervoor faalt.
```
gebruiker@ubuntu:~/map$ cd does_not_exist || > file3 && ls
bash: cd: does_not_exist: No such file or directory
file  file2  file3
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Een `#` is een notitie, alles achter `#` wordt genegeerd door Bash.
```
gebruiker@ubuntu:~/map$ echo Hello # this text does nothing
Hello
```

## Commando's & Terminologie

<table>
   <tr>
      <td>Commando</td>
      <td>Uitleg</td>
   </tr>
   <tr>
      <td>alias</td>
      <td>Zorgt dat een stuk tekst als een ander stuk tekst wordt geïnterpreteerd.</td>
   </tr>
   <tr>
      <td>unalias</td>
      <td>Verwijdert een alias.</td>
   </tr>
</table>

<table>
   <tr>
      <td>Term</td>
      <td>Uitleg</td>
   </tr>
   <tr>
      <td>shell</td>
      <td>Een command line interface, zet commando's om naar dingen die het systeem begrijpt.</td>
   </tr>
   <tr>
      <td>Bash</td>
      <td>Afkorting voor Bourne Again SHell</td>
   </tr>
   <tr>
      <td>string</td>
      <td>Een string is een stukje tekst.</td>
   </tr>
</table>

## Studeren {collapsible="true"}

<deflist collapsible="true">
<def title="Waar staat Bash voor?">
   Bourne Again SHell
</def>

<def title="Welk karakter zorgt dat tekst als string wordt gezien zonder uitzonderingen?">
   Het <code>'</code> karakter.
</def>

<def title="In welk bestand moet je aliassen zetten als je ze wilt blijven gebruiken?">
   Het <code>.bash_aliases</code> bestand.
</def>

<def title="Waar moet dit bestand staan?">
   In de home map van de gebruiker.
</def>

<def title="Wat doet het * karakter bij file globbing?">
   Het * karakter selecteert alles of niks.
</def>

<def title="Met welk karakter kan je één karakter selecteren?">
   Met het ? karakter.
</def>

<def title="Hoe selecteer je één nummer dat in een bereik van 0 - 7 zit?">
   Via: [0-7]
</def>

<def title="Welke stream bevat al de errors?">
   De 3de, de stderr stream.
</def>

<def title="Welke stream wordt omgeleid met >?">
   De stdout stream.
</def>

<def title="Wat doet: > txt?">
   Maakt een leeg bestand genaamd txt.
</def>

<def title="Als je cat > file gebruikt, hoe stop je met typen?">
   <shortcut>Ctrl+d</shortcut>
</def>

<def title="Wat doet ||?">
   Voer het volgende commando uit als de vorige faalt.
</def>
</deflist>
