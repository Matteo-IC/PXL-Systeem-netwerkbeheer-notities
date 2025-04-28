# DNS

De student(e)
- Kan een (reverse) DNS configureren
- Kan de geconfigureerde DNS testen

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**DNS (Domain Name System)** is een **systeem** dat **domeinnamen omzet** naar **IP-adressen**.\
**TLD:** Top Level Domain, bijvoorbeeld **.com**. 

## DNS Stappen

1. Je **computer zoekt in** zijn **eigen DNS-cache** voor het IP-adres.
2. Als het **IP-adres niet in** de **cache** staat **vraagt de computer** het aan de **DNS-server**.
   1. Deze server is een **recursieve DNS-server**.
3. Als de **DNS-server** het **IP-adres** niet heeft, vraagt hij het aan de **root nameserver**.
4. De **root nameserver** verwijst de **DNS-server** naar de **TLD nameserver** (Top Level Domain).
   1. Een **root nameserver** checkt het **TLD** en verwijst de **DNS-server** naar de **TLD nameserver**.
5. De **TLD nameserver** verwijst de **DNS-server** naar de **authoritative DNS-server**.
6. De **authoritative nameserver** geeft het **IP-adres** terug aan de **DNS-server**.
   1. De **authoritative nameserver** is de server die de **domeinnaam beheert**.
7. De **DNS-server** geeft het **IP-adres** terug aan de **computer**.

## Installatie & Configuratie

**Installeer** de DNS-server:
```
$ sudo dnf install bind
```

**Start** en **enable** de DNS-server:
```
$ sudo systemctl start named
$ sudo systemctl enable named
```

**Open** de **configuratie**:
```
$ sudo nano /etc/named.conf
```

**Pas** de configuratie **aan**:
```
options {
    listen-on port 53 { 127.0.0.1; 10.10.10.1; };
    # ^ De IP-adressen en poort waarop de DNS-server luistert
    allow-query     { localhost; 10.10.10.0/24; };
    # ^ De IP-adressen die DNS mogen gebruiken
    allow-recursion { localhost; 10.10.10.0/24; };
    # ^ Staat recursieve queries toe voor deze IP-adressen
    forwarders { 8.8.8.8; 8.8.4.4; };
    # ^ De DNS-servers die deze gebruikt als het niet lukt
    ...
```

**Controleer** de syntax:\
*Als er geen errors zijn, is het goed.*
```
$ sudo named-checkconf
```

**Herstart** de DNS-server:
```
$ sudo systemctl restart named
```

## DNS-zone

**Pas** de configuratie **aan**:
```
$ sudo nano /etc/named.conf
...
zone "mic.lan" {
# ^ De naam van de zone
    type master;
    # ^ Betekent dat dit de primaire DNS-server is
    file "/etc/named/mic.lan.db";
    # ^ Het bestand met de zone-informatie
    allow-query { any; };
    # ^ Wie mag de zone-informatie opvragen
    allow-transfer { none; };
    # ^ Wie mag de zone-informatie overdragen
};
```

```
$ sudo nano /etc/named/mic.lan.db

$TTL    8h
@       IN      SOA     ns1.mic.lan.    administrator.mic.lan. (
                       	2025042401      ;
                       	1d              ;
                       	3h              ;
                       	3d              ;
                       	3h )            ;
 
       	IN      NS      ns1.mic.lan.
       	IN      MX      10      mail.mic.lan.
 
www     IN      A       10.10.10.30
ns1     IN      A       10.10.10.1
mail    IN      A       10.10.10.40
webserverMIC     IN      A       10.10.10.1
```

<tabs>
<tab title="@">
   Verwijst naar deze zone.
</tab>
<tab title="IN">
    Internet.
</tab>
<tab title="SOA">
    Start of Authority. Bevat een aantal records.
</tab>
<tab title="ns1.mic.lan">
   De primaire DNS-server.
</tab>
<tab title="administrator.mic.lan">
   Mailadres van de beheerder van de zone. De eerste "." wordt gezien als "@".
</tab>
<tab title="2025042401">
   De datum van de laatste wijziging in het formaat YYYYMMDDNN. (Waar "N" het aantal aanpassingen is)
</tab>
<tab title="1d">
   Vernieuwingsperiode.
</tab>
<tab title="3h">
   Als vernieuwing faalt, tijd voor opnieuw te proberen.
</tab>
<tab title="3d">
   Tijd wanneer de 2de server de 1ste server stopt met gebruiken als die niet bereikbaar is.
</tab>
<tab title="3h">
   Hoe lang mislukte lookups worden bijgehouden in de cache.
</tab>
</tabs>

<tabs>
<tab title="NS">
   "Name Server", de nameserver die verantwoordelijk is voor het domein.
</tab>
<tab title="MX">
   De mailserver. Hoe lager het nummer achter "MX", hoe hoger de prioriteit.
</tab>
<tab title="A">
   Koppelt domeinnaam aan IPv4-adres.
</tab>
<tab title="AAAA">
   Koppelt domeinnaam aan IPv6-adres.
</tab>
</tabs>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Zet** de juiste **permissies** op de zone-bestanden:
```
$ sudo chown root:named /etc/named/mic.lan.db
$ sudo chmod 640 /etc/named/mic.lan.db
```

**Check** de **syntax**:
```
$ sudo named-checkzone mic.lan /etc/named/mic.lan.db
```

**Herstart** de DNS-server:
```
$ sudo systemctl restart named
```

## Reverse DNS

**Pas** de configuratie **aan**:
```
$ sudo nano /etc/named.conf
zone "10.10.10.in-addr.arpa" {
    type master;
    file "/var/named/10.10.10.in-addr.arpa.zone";
    allow-query { any; };
    allow-transfer { none; };
};
```

**Maak** het **zone-bestand** aan:
```
$ sudo nano /var/named/10.10.10.in-addr.arpa.zone
$TTL 8h
@ IN SOA ns1.mic.lan. administrator.mic.lan. (
    2025031901 ; serienummer
    1d         ; vernieuwingsperiode
    3h         ; herhalingsperiode
    3d         ; vervaltijd
    3h )       ; minimum TTL
 
        IN NS   ns1.mic.lan.
 
1       IN PTR  ns1.mic.lan.
30      IN PTR  www.mic.lan.
```

**PTR**: Pointer record, koppelt IP-adres aan domeinnaam. In de plaats van domeinnaam aan IP-adres.

**Zet** de juiste **permissies** op de zone-bestanden:
```
$ sudo chown root:named /var/named/10.10.10.in-addr.arpa.zone
$ sudo chmod 640 /var/named/10.10.10.in-addr.arpa.zone
```

**Check** de **syntax**:
```
$ sudo named-checkzone 10.10.10.in-addr.arpa /var/named/10.10.10.in-addr.arpa.zone
```

**Herstart** de DNS-server:
```
$ sudo systemctl restart named
```

### Client DNS

Om je client de DNS te laten gebruiken:
```
$ sudo nano /etc/dhcp/dhcpd.conf
ddns-update-style none;
authoritative;
 
subnet 10.10.10.0 netmask 255.255.255.0 {
    range 10.10.10.10 10.10.10.30;
    option domain-name-servers 10.10.10.1;
    option domain-name "mic.lan";
    option routers 10.10.10.1;
    default-lease-time 600;
    max-lease-time 7200;
}
```

## Testen

Enkele commando's:
```
$ dig www.mic.lan # Normale DNS lookup
$ dig +short -x 10.10.10.30 # Reverse DNS lookup
```

De website checken:
```
$ sudo systemctl start httpd
$ sudo firewall-cmd --add-service=http --zone=internal
```

## Oefeningen

**1.
Zorg dat enkel clients in het 10.10.10.0/24 network DNS-query’s kunnen aanvragen.**

```
$ sudo nano /etc/named.conf
options {
    listen-on port 53 { 127.0.0.1; 10.10.10.1; };
    allow-query     { localhost; 10.10.10.0/24; }; # deze lijn
    allow-recursion { localhost; 10.10.10.0/24; }; # en deze lijn
    forwarders { 8.8.8.8; 8.8.4.4; };
    ...
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2.
Forward DNS-query’s naar de dns-services van google (8.8.8.8, 8.8.4.4).**

```
$ sudo nano /etc/named.conf
options {
    listen-on port 53 { 127.0.0.1; 10.10.10.1; };
    allow-query     { localhost; 10.10.10.0/24; };
    allow-recursion { localhost; 10.10.10.0/24; };
    forwarders { 8.8.8.8; 8.8.4.4; }; # deze lijn
    ...
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3.
Zorg dat Server[JouwInitialen] en Client[JouwInitialen] door je DNS vertaald worden naar de IP adressen van jouw Server
en Client. Tip: voeg hun toe aan domein .pxl.lan (hostname)**

```
$ sudo nano /etc/named.conf
...
zone "mic.lan" {
    type master;
    file "/etc/named/mic.lan.db";
    allow-query { any; };
    allow-transfer { none; };
};

$ sudo nano /etc/named/mic.lan.db
$TTL    8h
@       IN      SOA     ns1.mic.lan.    administrator.mic.lan. (
                       	2025042401      ;
                       	1d              ;
                       	3h              ;
                       	3d              ;
                       	3h )            ;

       	IN      NS      ns1.mic.lan.
       	IN      MX      10      mail.mic.lan.

www     IN      A       10.10.10.30
ns1     IN      A       10.10.10.1
mail    IN      A       10.10.10.40
ServerMIC     IN      A       10.10.10.1
ClientMIC     IN      A       10.10.10.2

$ sudo chown root:named /etc/named/mic.lan.db
$ sudo chmod 640 /etc/named/mic.lan.db
$ sudo named-checkzone mic.lan /etc/named/mic.lan.db
$ sudo systemctl restart named
```

*Client:*
```
$ sudo nmcli connection modify "Wired Connection 1" ipv4.dns "10.10.10.1"
$ sudo nmcli connection modify "Wired Connection 1" ipv4.dns-search "mic.lan"
$ sudo nmcli connection up "Wired Connection 1"
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**4.
Zorg dat je DHCP-server jouw nieuwe DNS server deelt.**

```
$ sudo nano /etc/dhcp/dhcpd.conf
ddns-update-style none;
authoritative;
 
subnet 10.10.10.0 netmask 255.255.255.0 {
    range 10.10.10.10 10.10.10.30;
    option domain-name-servers 10.10.10.1;
    option domain-name "mic.lan";
    option routers 10.10.10.1;
    default-lease-time 600;
    max-lease-time 7200;
}
$ sudo systemctl restart dhcpd
```

*Client:*
```
$ cat /etc/resolv.conf # check of het werkt (connection eerst herstarten)
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**5.
Test met dig en door te pingen naar Server[JouwInitialen] en Client[JouwInitialen] dat je DNS via DHCP werkt.**

```
$ dig ServerMIC.mic.lan
$ dig ClientMIC.mic.lan
$ dig google.com
$ ping ServerMIC.mic.lan
$ ping ClientMIC.mic.lan
$ dig +trace google.com # toont welke dns server gebruikt wordt
```