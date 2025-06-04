# Security Enhanced Linux

De student(e) kan:
- SELinux fouten vinden in de logs.
- SELinux contexten en booleans aanpassen met de gepaste commando's

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**SELinux** (Security Enhanced Linux) is een **beveiligingssysteem** dat **toegang beheert** voor **bestanden, processen, 
netwerk poorten...**

**SELinux gebruikt MAC** (Mandatory Access Control). Dit betekent dat de **toegang tot bestanden en processen**
wordt **beheerd door** het **systeem**, **niet** door **de gebruiker**.

## DAC, ACL en MAC

**DAC** (Discretionary Access Control) is het **standaard beveiligingsmodel** in **Linux**. De **eigenaar van** een **bestand of map**
**bepaalt wie wat kan** doen met het bestand of de map. Dit gebeurt met behulp van de **lees**, **schrijf** en **uitvoer** rechten.

Commando's zoals `chmod` en `chown` worden gebruikt om deze rechten te beheren.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**ACL** (Access Control List) is een **uitbreiding van DAC**. Het stelt de gebruiker in staat om **meer gedetailleerde rechten**
toe te kennen **aan bestanden en mappen**. 

ACL's kunnen worden beheerd met de commando's `getfacl` en `setfacl`.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**MAC** (Mandatory Access Control) is een **beveiligingsmodel** dat beheerd wordt door het **systeem**.

- Het **systeem bepaalt** wie wat kan doen met bestanden, processen, netwerk poorten...
  - *In SELinux kan de gebruiker wel bepaalde instellingen aanpassen, maar niet alles.*

## Hoe werkt SELinux?

### Modi en types

Er zijn **drie manieren** waarop SELinux kan werken:
1. **Disabled**: SELinux is **uitgeschakeld**.
2. **Permissive**: SELinux is **ingeschakeld, maar blokkeert niets**. Het **logt wel gebeurtenissen**.
3. **Enforcing**: SELinux is **ingeschakeld**. Het **logt en blokkeert gebeurtenissen**.

Daarnaast zijn er **drie soorten types**:
1. **Targeted**: **Services** met **hoge risico's** worden **beveiligd**. Het **standaard type**.
2. **Minimum**: **Minimale beveiliging**. Bijna alles wordt **toegestaan**.
3. **MLS** (Multi-Level Security): **Beveiliging op basis van niveaus**. Wordt **niet vaak gebruikt**.

De **status** van SELinux kan worden bekeken met het commando `sestatus`.
<code-block collapsible="true">
$ sestatus
SELinux status:                 enabled ---------> SELinux is actief
SELinuxfs mount:                /sys/fs/selinux -> Het mount punt
SELinux root directory:         /etc/selinux ----> De configuratiemap
Loaded policy name:             targeted --------> Het actieve type
Current mode:                   enforcing -------> De huidige modus
Mode from config file:          enforcing ------¬
                                                ↓
De modus uit het configuratiebestand, die wordt gebruikt bij het opstarten.

Policy MLS status:              enabled ---------> MLS is actief
Policy deny_unknown status:     allowed --------¬
                                                ↓
                           Onbekende gebeurtenissen worden toegestaan
                        
Memory protection checking:     actual (secure) -> RAM wordt beschermd
Max kernel policy version:      33 --------------> Hoogst ondersteunde versie
</code-block>

Om **permanent** de **modus en** het **type** van SELinux te **veranderen**, kan je het **configuratiebestand**
`/etc/selinux/config` aanpassen.
<code-block collapsible="true">
$ sudo nano /etc/selinux/config
...
SELINUX=enforcing
...
SELINUXTYPE=targeted
</code-block>

### Contexten

**SELinux** maakt gebruik van **contexten**. Een **context** is een **set van attributen** die aan een **object**
worden **toegekend**. Deze attributen **bepalen hoe** het **object kan worden gebruikt**.

Een **voorbeeld** van een context is:
```
system_u : object_r : httpd_sys_content_t : s0
    ↓         ↓              ↓              ↓
Gebruiker    Rol           Type        MLS Level
                                       (Optioneel)
```

<tabs>
<tab title="Gebruiker">
  <p>Een <control>SELinux gebruiker</control> is <control>niet hetzelfde</control> als een <control>Linux gebruiker</control>.</p>
  <p><control>SELinux gebruikt</control> dit om te <control>bepalen</control> welke <control>SELinux rollen</control> de
  gebruiker kan hebben. Bepaalde <control>gebruikers</control> hebben ook <control>restricties</control> op bijvoorbeeld
  gebruik van sudo.</p>
  <list>
  <li>
    <code>system_u</code> is een <control>systeemgebruiker</control>. Dit is <control>niet geassocieerd met een gebruiker
    </control> maar met een <control>systeemproces</control> zoals ssh.
  </li>
  <li>
    <code>unconfined_u</code> is de standaard <control>SELinux gebruiker</control> voor Linux gebruikers. Deze gebruiker
    heeft <control>bijna geen restricties</control>.
  </li>
  <li>
    <code>user_u</code> is een <control>beperkte SELinux gebruiker</control>. Deze gebruiker heeft 
    <control>geen administrator rechten</control>.
  </li>
  <li>
    <code>sysadm_u</code> is een <control>administratieve gebruiker</control> die alleen bedoeld is 
    <control>voor administratieve commando's</control>.
  </li>
  <li>
    <code>staff_u</code> is een <control>administratieve gebruiker</control> die bedoeld is voor 
    <control>administratieve en niet administratieve commando's</control>.
  </li>
  <li>
    <code>root</code> is de <control>root gebruiker</control> van het systeem.
  </li>
  <li>
    <code>guest_u</code> is een <control>beperkte SELinux gebruiker</control> die bedoeld is voor 
    <control>gastgebruikers</control>.
  </li>
  </list>
</tab>
<tab title="Rol">
  Een <control>SELinux rol</control> bepaalt welke <control>types</control> de gebruiker permissie heeft om te gebruiken.
</tab>
<tab title="Type">
</tab>
<tab title="MLS Level">
</tab>
</tabs>


## Oefeningen

**1. Maak een bestand test.html aan in je homedirectory. Pas de context van dit bestand aan zodanig dat httpd deze 
context kan lezen.**
```
$ > test.html
$ sudo chcon -t httpd_user_content_t test.html
$ sudo restorecon test.html
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2. Pas SELinux zodanig aan dat het httpd bestanden uit je homedirectory permanent kan lezen.**
```
$ sudo setsebool -P httpd_enable_homedirs on
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3. Zorg ervoor dat httpd mails kan versturen.**
```
$ sudo setsebool -P httpd_can_sendmail on
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**4. Stel dat je een website hebt geïnstalleerd waarbij er lees/schijfrechten nodig zijn voor de directory
/var/www/html/platform. Hoe wijzig je SELinux zodanig dat er lees/schijfrechten zijn voor de directory platform?**
```
$ sudo semanage fcontext -a -t httpd_sys_rw_content_t "/var/www/html/platform(/.*)?"
$ sudo restorecon -Rv /var/www/html/platform
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**5. Je wil SELinux alleen in loggende modus gebruiken. Hoe stel je dit in?**
```
$ sudo setenforce 0
```
```
$ sudo nano /etc/selinux/config
...
SELINUX=permissive
```
