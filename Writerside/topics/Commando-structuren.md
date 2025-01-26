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

Een alias is een **stuk tekst dat door bash als een command wordt geïnterpreteerd**.

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

## I/O redirection

**De shell heeft 3 streams.**\
Een stream is een categorie voor een bepaald soort tekst in de shell.

<img src="streams-diagram.svg" alt="streams visualized" width="500"/>

