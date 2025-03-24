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

**Oefening 1:**
```
$ sudo ip a add 192.168.1.1/24 dev ens160
```

**Oefening 2:**
```
$ ip a
```

**Oefening 3:**
```
$ nmcli connection add type ethernet con-name "Verbinding" ifname ens160
$ nmcli connection modify Verbinding ipv4.addresses 192.168.112.50/24
$ nmcli connection modify Verbinding ipv4.gateway 192.168.112.2
$ nmcli connection modify Verbinding ipv4.dns "8.8.8.8 8.8.4.4"
$ nmcli connection modify Verbinding ipv4.method manual
$ nmcli connection up Verbinding
```

**Oefening 4:**
```
$ nmcli connection modify Verbinding connection.autoconnect yes
$ nmcli connection modify ens160 connection.autoconnect no
```

**Oefening 5:**
```
$ nmcli connection modify Verbinding +ipv4.routes "10.0.100.0/24 192.168.112.200"
$ nmcli connection up "Verbinding"
```

**Oefening 6:**\
Teaming moeten we niet meer kennen.

**Oefening 7:**
```
$ nmcli connection add type bond con-name bond0 ifname bond0 mode active-backup
$ nmcli connection add type ethernet con-name ens160 ifname ens160 master bond0
$ nmcli connection add type ethernet con-name ens224 ifname ens224 master bond0
$ nmcli connection modify bond0 ipv4.addresses 192.168.112.50/24
$ nmcli connection modify bond0 ipv4.gateway 192.168.112.2
$ nmcli connection modify bond0 ipv4.method manual
$ nmcli connection up bond0
```

**Oefening 8:**
```
$ nmcli connection add type bond con-name bond1 ifname bond1 mode 802.3ad
$ nmcli connection add type ethernet con-name ens160 ifname ens160 master bond1
$ nmcli connection add type ethernet con-name ens224 ifname ens224 master bond1
Optionele IP configuratie
$ cat /proc/net/bonding/bond1
```

**Oefening 9:**
Er is niet `con-name bond0` in het eerste commando gezet, het heet nu eigenlijk `bond-bond0`.\
Het staat ook niet in de commando's om de verbindingen aan de bond toe te voegen.
