# Software

Om software te installeren gebruikt Linux **package managers**.

Ubuntu gebruikt standaard de **apt** package manager.

## Wat is een package manager?

Een package manager is een **programma dat het installeren, updaten en verwijderen van software automatiseert**.

### Zo werkt een package manager:

1. Je geeft het commando om een package te installeren.
   2. Je moet sudo gebruiken omdat je niet alleen voor jouw gebruiker installeert.
```bash
gebruiker@ubuntu:~$ sudo apt install cbonsai
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

2. Het **kijkt in een lijst van packages die het lokaal heeft staan**.
   1. Het haalt de lijst van online <tooltip term="repository">repositories</tooltip>.
   2. Deze **lijst kan je updaten met `sudo apt update`** om de nieuwste versies van packages te gebruiken.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

3. De package manager kijkt **wat het package nodig heeft om te werken**.
   1. Packages hebben vaak **<tooltip term="dependency">dependencies</tooltip>**.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

4. **De package manager installeert het package en de dependencies.**

```Bash
gebruiker@ubuntu:~$ sudo apt install cbonsai
[sudo] password ​for gebruiker: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  cbonsai
0 upgraded, 1 newly installed, 0 to remove and 159 not upgraded.
...
```

## Commando's

*Commando's voor de **apt** package manager.*

<tabs>
<tab title="install">
   <control>Installeer of update een package.</control>
   <code-block>
      gebruiker@ubuntu:~$ sudo apt install cbonsai
   </code-block>
</tab>
<tab title="update">
   <control>Download de nieuwste lijsten</control> van packages en hun dependencies, versies...
   <code-block>
      gebruiker@ubuntu:~$ sudo apt update
      [sudo] password ​for gebruiker: 
      Get:1 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
      Hit:2 http://be.archive.ubuntu.com/ubuntu noble InRelease
      ...
      Fetched 2,934 kB ​in 1s (1,974 kB/s)                                  
      Reading package lists... Done
      Building dependency tree... Done
      Reading state information... Done
      165 packages can be upgraded. Run 'apt list --upgradable' to see them.
   </code-block>
</tab>
<tab title="upgrade">
   <control>Installeert nieuwere versies van packages die al op je systeem staan.</control>
   <code-block>
      gebruiker@ubuntu:~$ sudo apt upgrade
   </code-block>
</tab>
<tab title="search">
   <control>Zoek naar een package.</control>
   <code-block>
      gebruiker@ubuntu:~$ apt search bonsai
      Sorting... Done
      Full Text Search... Done
      cbonsai/noble,now 1.3.1-1 amd64 [installed]
        terminal-based bonsai tree generator
      ​
      python3-bonsai/noble 1.5.0+ds-3build3 amd64
      Asyncio/gevent/tornado-compatible LDAP library
   </code-block>
</tab>
<tab title="remove">
   <control>Verwijdert een package en laat de configuratie bestanden achter.</control>
   <code-block>
      gebruiker@ubuntu:~$ sudo apt remove cbonsai
   </code-block>
</tab>
<tab title="autoremove">
   <control>Verwijdert packages die automatisch als dependency geïnstalleerd waren en niet meer nodig zijn.</control>
   <code-block>
      gebruiker@ubuntu:~$ sudo apt autoremove
   </code-block>
</tab>
<tab title="purge">
   <control>Verwijdert een package, de dependencies en de configuratie bestanden.</control>
   <code-block>
      gebruiker@ubuntu:~$ sudo apt purge cbonsai
   </code-block>
</tab>
<tab title="list">
   <control>Toont alle packages, gebruik <code>--installed</code></control> om de geïnstalleerde te zien.
   <code-block>
      gebruiker@ubuntu:~$ apt list --installed
   </code-block>
</tab>
</tabs>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

<note>
Er zijn <control>veel package managers</control>. 
Elke heeft <control>andere commando's en heeft andere packages</control>.
</note>

## Commando's & Terminologie

<table>
   <tr>
      <td>Commando</td>
      <td>Uitleg</td>
   </tr>
   <tr>
      <td>sudo apt install</td>
      <td>Installeer of update een package.</td>
   </tr>
   <tr>
      <td>sudo apt update</td>
      <td>Download de nieuwste lijsten van packages en hun dependencies, versies...</td>
   </tr>
   <tr>
      <td>sudo apt upgrade</td>
      <td>Installeert nieuwere versies van packages die al op je systeem staan.</td>
   </tr>
   <tr>
      <td>apt search</td>
      <td>Zoek naar een package.</td>
   </tr>
   <tr>
      <td>sudo apt remove</td>
      <td>Verwijdert een package en laat de configuratie bestanden achter.</td>
   </tr>
   <tr>
      <td>sudo apt autoremove</td>
      <td>Verwijdert packages die automatisch als dependency geïnstalleerd waren en niet meer nodig zijn.</td>
   </tr>
   <tr>
      <td>sudo apt purge</td>
      <td>Verwijdert een package, de dependencies en de configuratie bestanden.</td>
   </tr>
   <tr>
      <td>apt list</td>
      <td>Toont alle packages, gebruik --installed om de geïnstalleerde te zien.</td>
   </tr>
</table>

<table>
   <tr>
      <td>Term</td>
      <td>Uitleg</td>
   </tr>
   <tr>
      <td>Repository</td>
      <td>Een online locatie / server waar data op staat.</td>
   </tr>
   <tr>
      <td>Dependency</td>
      <td>Een stukje software dat een ander programma nodig heeft om te werken.</td>
   </tr>
</table>

## Studeren {collapsible="true"}

<deflist collapsible="true">
<def title="Wat is een dependency?">
   Een stukje software dat een ander programma nodig heeft om te werken.
</def>
<def title="Wat is het verschil tussen apt autoremove en apt purge?">
   <p><code>apt autoremove</code> verwijdert alle dependencies die niet meer nodig zijn.</p>
   <p><code>apt purge</code> verwijdert één package met de dependencies en de configuratie bestanden.</p>
</def>
<def title="Welk commando kan gebruikt worden om één enkel package te updaten?">
   <code>apt install</code> kan het gegeven package updaten.
</def>
</deflist>

