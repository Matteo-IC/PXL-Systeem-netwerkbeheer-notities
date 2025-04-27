# Netwerkbeheer

## Netwerktools

**NetworkManager** is een **daemon** van het systeem die **netwerk verbinding beheert**.

Om **NetworkManager** te **gebruiken** kan je **nmcli** gebruiken. Dit is een **command line tool**.

Enkele **nmcli commando's**:
```
$ nmcli connection show ----------> Toont alle netwerkverbindingen
                   show <naam> ---> Details van een netwerkverbinding
                   up <naam> -----> Activeer een netwerkverbinding
                   down <naam> ---> Deactiveer een netwerkverbinding
                   delete <naam> -> Verwijder een netwerkverbinding
                   edit <naam> ---> Bewerk interactief een netwerkverbinding
                   modify <naam> -> Bewerk een netwerkverbinding
```

Het **ip route** commando toont de **routing tabel** en kan deze bewerken.
```
$ ip route -----------------------------> Toon de routing tabel
           get <ip> --------------------> Toon de route naar een ip
           add <ip/mask> via <gateway> -> Voeg een route toe
           add <ip/mask> dev <device> --> Voeg een route toe
           add default via <gateway> ---> Voeg een default route toe
           del <ip/mask> ---------------> Verwijder een route
           replace <ip/mask> via <ip> --> Vervang een route
```

## Netwerk bonding

Het **samenvoegen** van **netwerkinterfaces** tot **één logische interface** wordt **bonding** genoemd.

### Instellen

1. **Bonding interface maken**:
```
$ ... type bond con-name bond0 ifname bond-if mode active-backup
   |
   ↓
nmcli connection add
```

2. **Interfaces toevoegen** aan de bonding interface:
```
$ ... type ethernet con-name ens160 ifname ens160 master bond-if
$ ... type ethernet con-name ens224 ifname ens224 master bond-if
```

3. **IP configureren**:
```
$ nmcli connection modify bond0 ipv4.addresses 192.168.112.100/24
$ nmcli connection modify bond0 ipv4.gateway 192.168.112.2
$ nmcli connection modify bond0 ipv4.dns 192.168.112.2
$ nmcli connection modify bond0 ipv4.method manual
```

4. **Activeer** de bonding interface:
```
$ nmcli connection up bond0
```

5. **Controleer** de **bonding interface**:
```
$ cat /proc/net/bonding/bond0
```

In `/proc/` staat informatie over **processen, hardware en systeem configuratie**.

#### 1. Bonding interface maken uitleg {collapsible="true"}

Het **bond interface** aanmaken met `nmcli connection add`:
```
$ ... type bond con-name bond0 ifname bond-if mode active-backup
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Het **type** van de **verbinding**, in dit geval **bond**.
```
$ ... type bond con-name bond0 ifname bond-if mode active-backup
      ^^^^^^^^^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **naam** van de **verbinding**.
```
$ ... type bond con-name bond0 ifname bond-if mode active-backup
                ^^^^^^^^^^^^^^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **interface naam**.
```
$ ... type bond con-name bond0 ifname bond-if mode active-backup
                               ^^^^^^^^^^^^^^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **bonding opties**. In dit geval **active-backup**, hierdoor wordt er maar **één interface** gebruikt
en **andere interfaces** worden **gebruikt** als de **eerste interface** **uitvalt**.
```
$ ... type bond con-name bond0 ifname bond-if mode active-backup
                                              ^^^^^^^^^^^^^^^^^^
```

#### 2. Interfaces toevoegen uitleg {collapsible="true"}

Interfaces toevoegen aan de **bonding interface**:
```
$ ... type ethernet con-name ens160 ifname ens160 master bond-if
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Het **type** van de **verbinding**, in dit geval **ethernet**.
```
$ ... type ethernet con-name ens160 ifname ens160 master bond-if
      ^^^^^^^^^^^^^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **naam** van de **verbinding** die toegevoegd wordt.
```
$ ... type ethernet con-name ens160 ifname ens160 master bond-if
                    ^^^^^^^^^^^^^^^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **naam** van het **interface** dat **gebruikt** wordt.
```
$ ... type ethernet con-name ens160 ifname ens160 master bond-if
                                    ^^^^^^^^^^^^^
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

De **master** van de **interface**. Dit is de **bonding interface**.
```
$ ... type ethernet con-name ens160 ifname ens160 master bond-if
                                                  ^^^^^^^^^^^^^^
```

Herhaal voor de 2de verbinding.

## Oefeningen

**1.
Zoek uit hoe je met “ip addr” het ip-address 192.168.1.1 met als subnetmasker 255.255.255.0 kan toevoegen aan je
netwerkkaart. Check dit ook met “ip addr”.**
```
$ sudo ip a add 192.168.1.1/24 dev ens160
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2.
Zoek hoe je “ip address show” met zo weinig mogelijk karakters kan uitvoeren. Je blijft het commando “ip” gebruiken.**
```
$ ip a
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3.
Via het commando nmcli: Maak een nieuwe connectie genaamd “Verbinding” voor je eerste netwerkkaart aan. Het IP-nummer is
192.168.112.50/24 en de gateway is 192.168.112.2. Zet ook de DNS-servers voor“Verbinding” op 8.8.8.8 en 8.8.4.4.
Zorg ervoor dat deze connective geactiveerd wordt via het commando nmcli.**
```
$ nmcli connection add type ethernet con-name "Verbinding" ifname ens160
$ nmcli connection modify Verbinding ipv4.addresses 192.168.112.50/24
$ nmcli connection modify Verbinding ipv4.gateway 192.168.112.2
$ nmcli connection modify Verbinding ipv4.dns "8.8.8.8 8.8.4.4"
$ nmcli connection modify Verbinding ipv4.method manual
$ nmcli connection up Verbinding
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**4.
Stel in dat er automatisch verbinding wordt gemaakt met “Verbinding” en dat er niet automatisch verbinding wordt gemaakt
met je eerste connectienaam.**
```
$ nmcli connection modify Verbinding connection.autoconnect yes
$ nmcli connection modify ens160 connection.autoconnect no
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**5.
Voeg een aangepaste route toe voor het netwerk 10.0.100.0/255.255.255.0 via de computer 192.168.112.200 in je eigen
network. Gebruik hiervoor het commando nmcli.**
```
$ nmcli connection modify Verbinding +ipv4.routes "10.0.100.0/24 192.168.112.200"
$ nmcli connection up "Verbinding"
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Oefening 6:**\
Teaming moeten we niet meer kennen.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**7.
Gebruik nmcli om een bond-interface genaamd bond0 aan te maken met de modus active-backup. Voeg twee netwerkinterfaces
toe (ens160 en ens224). Zorg ervoor dat bond0 een statisch IP-adres van 192.168.112.50/24 krijgt met een gateway
192.168.112.2.**
```
$ nmcli connection add type bond con-name bond0 ifname bond0 mode active-backup
$ nmcli connection add type ethernet con-name ens160 ifname ens160 master bond0
$ nmcli connection add type ethernet con-name ens224 ifname ens224 master bond0
$ nmcli connection modify bond0 ipv4.addresses 192.168.112.50/24
$ nmcli connection modify bond0 ipv4.gateway 192.168.112.2
$ nmcli connection modify bond0 ipv4.method manual
$ nmcli connection up bond0
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**8.
Stel een bond-interface bond1 in met lacp (IEEE 802.3ad). Zorg ervoor dat de bond correct geconfigureerd is en check de
status met cat /proc/net/bonding/bond1.**
```
$ nmcli connection add type bond con-name bond1 ifname bond1 mode 802.3ad
$ nmcli connection add type ethernet con-name ens160 ifname ens160 master bond1
$ nmcli connection add type ethernet con-name ens224 ifname ens224 master bond1
Optionele IP configuratie
$ cat /proc/net/bonding/bond1
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**9.
Je hebt de volgende configuratie gemaakt voor een bond-interface (bond0), maar je krijgt geen netwerkverbinding: ...**

Er is niet `con-name bond0` in het eerste commando gezet, het heet nu eigenlijk `bond-bond0`.\
Het staat ook niet in de commando's om de verbindingen aan de bond toe te voegen.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**10.
Stel een active-backup bonding in via nmcli, maar zorg ervoor dat deze behouden blijft na een reboot.
Test dit door de machine opnieuw op te starten en te controleren of de configuratie blijft bestaan.**

```
$ sudo nmcli connection add type bond con-name bond2 ifname bond2 mode active-backup
... # Interfaces toevoegen & IP adres etc.
$ sudo nmcli connection up bond2
# Zou moeten werken na reboot maar niet getest
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**11.
Je hebt een werkende active-backup bond (bond0). Zorg ervoor dat het systeem altijd 8.8.8.8 en 8.8.4.4 als DNS-servers 
gebruikt, ongeacht welke netwerkinterface actief is. Test of de instellingen persistent blijven na een reboot.**

```
$ sudo nmcli connection modify bond0 ipv4.dns "8.8.8.8 8.8.4.4"
$ sudo nmcli connection modify bond0 ipv4.ignore-auto-dns yes
$ sudo nmcli connection down bond0
$ sudo nmcli connection up bond0
$ sudo nmcli connection modify bond0 ipv4.dns-priority 10 # Misschien nodig?
```