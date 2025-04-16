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
$ sudo apt install bind
```

**Start** en **enable** de DNS-server:
```
$ sudo systemctl start bind
$ sudo systemctl enable bind
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
zone "pxl.lan" {
# ^ De naam van de zone
    type master;
    # ^ Betekent dat dit de primaire DNS-server is
    file "/etc/named/pxl.lan.db";
    # ^ Het bestand met de zone-informatie
    allow-query { any; };
    # ^ Wie mag de zone-informatie opvragen
    allow-transfer { none; };
    # ^ Wie mag de zone-informatie overdragen
};
```

```
$ sudo nano /etc/named/pxl.lan.db

$TTL    8h
@       IN      SOA     ns1.pxl.lan.    administrator.pxl.lan. (
                       	2025031701      ;
                       	1d              ;
                       	3h              ;
                       	3d              ;
                       	3h )            ;
 
       	IN      NS      ns1.pxl.lan.
       	IN      MX      10      mail.pxl.lan.
 
www     IN      A       10.10.10.30
ns1     IN      A       10.10.10.1
mail    IN      A       10.10.10.40
webserverGF     IN      A       10.10.10.1
 
pxl.lan.  IN  TXT    "Dit is een test tekst."
```

<tabs>
<tab title="@">
   Verwijst naar deze zone.
</tab>
<tab title="IN">
    Internet.
</tab>
<tab title="SOA">
    Start of Authority. Geeft de primaire zone aan.
</tab>
<tab title="ns1.pxl.lan">
   De primaire DNS-server.
</tab>
<tab title="administrator.pxl.lan">
   Mailadres van de beheerder van de zone.
</tab>
<tab title="2025031701">
   De datum van de laatste wijziging in het formaat YYYYMMDDNN.
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
<tab title="MX 10">
   De prioriteit van de mailserver. Hoe lager het nummer, hoe hoger de prioriteit.
</tab>
<tab title="A">
   Koppelt domeinnaam aan IP-adres.
</tab>
<tab title="AAAA">
   Koppelt domeinnaam aan IPv6-adres.
</tab>
<tab title="TXT">
   Text record.
</tab>
</tabs>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Zet** de juiste **permissies** op de zone-bestanden:
```
$ sudo chown root:named /etc/named/pxl.lan.db
$ sudo chmod 640 /etc/named/pxl.lan.db
```

**Check** de **syntax**:
```
$ sudo named-checkzone pxl.lan /etc/named/pxl.lan.db
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
@ IN SOA ns1.pxl.lan. administrator.pxl.lan. (
    2025031901 ; serienummer
    1d         ; vernieuwingsperiode
    3h         ; herhalingsperiode
    3d         ; vervaltijd
    3h )       ; minimum TTL
 
        IN NS   ns1.pxl.lan.
 
1       IN PTR  ns1.pxl.lan.
30      IN PTR  www.pxl.lan.
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
    option routers 10.10.10.1;
    default-lease-time 600;
    max-lease-time 7200;
}
```

## Testen

Enkele commando's:
```
$ dig www.pxl.lan # Normale DNS lookup
$ dig +short -x 10.10.10.30 # Reverse DNS lookup
```

De website checken:
```
$ sudo systemctl start httpd
$ sudo firewall-cmd --add-service=http --zone=internal
```

