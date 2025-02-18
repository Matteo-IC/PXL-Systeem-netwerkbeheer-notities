# Services starten en stoppen

De student(e):
- Kan services aanzetten, stoppen, herladen, aanzetten bij het opstarten van het systeem.
- Kan uitleggen wat systemd is.
- Kan uitleggen wat runlevels zijn.
- Kan uitleggen wat units en targets zijn.
- Kan de default target aanpassen.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Symbolische link / symlink:** Een speciaal soort **bestand** dat naar een **folder of map verwijst**, 
een shortcut / referentie. Programma's die de symlink gebruiken worden automatisch doorverwezen.

Symlink maken:
```
[student@ServerMIC ~]$ ln -s doel_pad link_naam
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Linux kan **daemons configureren en beheren** via een **process management system genaamd systemd**.

**Systemd is** ook een **daemon**.
- Het **beheert** alle **andere daemons** en wordt **als eerste gestart**.
- Daemons die als eerste starten en andere beheren worden de **init daemon genoemd**.
- Het heeft **process ID 1**.

Het oplijsten van actieve processen:
```
[student@ServerMIC ~]$ ps -e | head -2
    PID TTY          TIME CMD
      1 ?        00:00:02 systemd
```

## Systemd

In systemd worden **daemons beheerd via units**.\
Er zijn 2 primaire unit types:
- **Service units:** Het meest voorkomend, gebruikt om **daemons te starten en te beheren**.
- **Target units:** Groepen van units.

Om bv. alle **actieve target units te tonen**:
```
[student@ServerMIC ~]$ systemctl list-units | grep .target
```

Een service-unit **stoppen** kan via:
```
[student@ServerMIC ~]$ sudo systemctl stop cups
```

Service-unit **starten**:
```
[student@ServerMIC ~]$ sudo systemctl start cups
```

Service-unit **herstarten**:
```
[student@ServerMIC ~]$ sudo systemctl restart cups
```

Service-unit **herstarten als die actief is**:
```
[student@ServerMIC ~]$ sudo systemctl condrestart cups
```

Service-unit **configuratie herladen zonder te herstarten**:
```
[student@ServerMIC ~]$ sudo systemctl reload sshd
```

Service-unit **starten als het systeem aan gaat**:
```
[student@ServerMIC ~]$ sudo systemctl enable cups
```

Service-unit **niet starten als het systeem aan gaat**:
```
[student@ServerMIC ~]$ sudo systemctl disable cups
```

## Verschillen

**Process:**
- Heeft een PID (Process ID)
- Kan kort of lang duren
- Elk actief programma
- Bijvoorbeeld:
  - Shell window / tab
  - Browser tab
  - Daemons

**Daemon:**
- Een langdurend achtergrond proces.
- Start meestal bij de start van het systeem en gaat uit als het systeem stopt
- Is niet zichtbaar
- Bijvoorbeeld:
  - sshd
  - crond
  - httpd

**Service unit:**
- Een unit van systemd dat een service beheert
- Definïeert hoe een specifieke service gestart, gestopt... moet worden
- Bijvoorbeeld:
  - sshd.service
  - nginx.service

De .service extensie wordt vaak niet getoond.\
Er zijn **11 soorten units**. Ze hebben elk **andere taken**.\
De belangrijkste unit om te kennen is de service-unit.

## Runlevels

**Systemd is compatibel met oudere systemen**. Dit komt door **speciale target units** die oude **"runlevels" nadoen**.

**Runlevels:** **Gebruikt in oude Linux** "SysVinit" systemen, **toestand** van de **init daemon** en het systeem dat
**bepaalt welke services actief zijn**.


**Vroeger** waren er **7 runlevels**:
- Runlevel 0: Systeem uitschakelen (shutdown).
- Runlevel 1: Enkelgebruikersmodus (rescue mode).
- Runlevel 2: Multi-user modus zonder netwerk.
- Runlevel 3: Multi-user modus met netwerk.
- Runlevel 4: Niet gedefinieerd, door gebruiker definieerbaar.
- Runlevel 5: Multi-user modus met netwerk en grafische gebruikersinterface.
- Runlevel 6: Systeem herstarten (reboot).

**Systemd** gebruikt **unit targets in de plaats van runlevels**:
- Runlevel 0: poweroff.target
- Runlevel 1: rescue.target
- Runlevel 2, 3, 4: multi-user.target
- Runlevel 5: graphical.target
- Runlevel 6: reboot.target

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Huidig runlevel** checken:
```
[student@ServerMIC ~]$ systemctl get-default
graphical.target
```

**Overschakelen** naar ander **target**:
```
[student@ServerMIC ~]$ sudo systemctl isolate multi-user.target
```

Standaard **target** instellen **voor opstarten** (bv. grafisch opstarten & alleen tekst opstarten):
```
[student@ServerMIC ~]$ sudo systemctl set-default graphical.target
[student@ServerMIC ~]$ sudo systemctl set-default multi-user.target
```

### Waarom?

Stel dat er een probleem is met een grafische service, het maakt het moeilijk om dat probleem op te lossen.\
Zo kan je zorgen dat die service niet start en je kan troubleshooten zonder problemen, later kan je terugschakelen.

## Oefeningen

1. Toon welke initialisatie daemon je server gebruikt.
```
[student@ServerMIC ~]$ ps -p 1
    PID TTY          TIME CMD
      1 ?        00:00:02 systemd
```
Het commando ps toont processen, `-p 1` toont het proces met PID 1.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

2. Welk commando kan je gebruiken om de status van je ssh daemon te bepalen?
```
[student@ServerMIC ~]$ sudo systemctl status sshd
[sudo] wachtwoord voor student:
● sshd.service - OpenSSH server daemon
     Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: enabled)
     Active: active (running) since Tue 2025-02-18 13:31:05 CET; 1h 56min ago
```
Via `systemctl status` kan je de status zien van een service.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

3. Bepaal de vorige en het huidige runlevel.
```
[student@ServerMIC ~]$ who -r
         run-level 5  2025-02-18 13:31
```
Toont het huidige runlevel.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

4. Hoe kan je de standaard target unit op je Linux systeem wijzigen?
```
[student@ServerMIC ~]$ sudo systemctl set-default <target>.target
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

5. Met welk commando list je welke services er runnen op je server?
```
[student@ServerMIC ~]$ systemctl list-units --type=service --state=running
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

6. Toon de status van de cups daemon op je Linux server.
```
[student@ServerMIC ~]$ sudo systemctl status cups
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

7. Herstart de cups daemon op je Linux server.
```
[student@ServerMIC ~]$ sudo systemctl restart cups
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

8. Tracht de cups daemon op je Linux server te herladen.
```
[student@ServerMIC ~]$ sudo systemctl restart cups
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

9. Zorg ervoor dat er standaard niet grafisch opgestart wordt. Hoe kan je ervoor zorgen dat je dan, na opstarten,
overgaat naar een grafische omgeving.
```
sudo systemctl set-default multi-user.target
sudo systemctl isolate graphical.target
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

10. Stel terug in dat je standaard grafisch opstart.
```
[student@ServerMIC ~]$ sudo systemctl set-default graphical.target
```
