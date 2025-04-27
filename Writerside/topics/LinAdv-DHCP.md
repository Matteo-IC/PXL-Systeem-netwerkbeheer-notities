# DHCP

**DHCP** zorgt dat **apparaten** binnen een netwerk automatisch een **IP-adres** en **andere netwerkconfiguratie** krijgen.

## Configuratie

**Installeren** van de **DHCP-server**:
```
$ sudo dnf install -y dhcp-server
```

**Statisch IP-adres** instellen voor de **DHCP-server**:
```
$ sudo nano /etc/dhcp/dhcpd.conf

ddns-update-style none;
authoritative;

subnet 10.10.10.0 netmask 255.255.255.0 {
    range 10.10.10.10 10.10.10.30;
    option domain-name-servers 192.168.238.2;
    option routers 10.10.10.1;
    default-lease-time 600;
    max-lease-time 7200;
}
```

**Starten** en **activeren** van de **DHCP-server**:
```
$ sudo systemctl start dhcpd
$ sudo systemctl enable dhcpd
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Client configureren:**
```
$ sudo nmcli connection modify Connection ipv4.method auto

```

Nu moet je **automatisch** een **IP-adres** krijgen van de **DHCP-server**.

## Oefeningen

**1.
Stel een DHCP-server in op je eerste machine. Je deelt IP-adressen uit in de range 10.10.10.150 tot 10.10.10.200.
Als gateway stel je uiteraard 10.10.10.1 in en als DNS-server stel je 8.8.8.8 en 8.8.4.4 in.**

```
$ sudo nano /etc/dhcp/dhcpd.conf

ddns-update-style none;
authoritative;

subnet 10.10.10.0 netmask 255.255.255.0 {
    range 10.10.10.150 10.10.10.200;
    option routers 10.10.10.1;
    option domain-name-servers 8.8.8.8, 8.8.4.4;
    option broadcast-address 10.10.10.255;
    default-lease-time 600;
    max-lease-time 7200;
}
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2.
Stel via de command-line interface in dat je tweede machine geen vast IP-adres meer heeft maar een IP-adres bekomt van
de DHCP-server. Bepaal het MAC-adres ook via de command-line interface.**

```
$ sudo nmcli connection modify "Wired Connection 1" ipv4.method auto
$ ip link show
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3.
Stel in dat een client altijd een zelfde IP-adres van een DHCP-server. Tip: MAC-adres**

```
$ ip link show # client
$ sudo nano /etc/dhcp/dhcpd.conf # server
...
host client1 {
    hardware ethernet 00:11:22:33:44:55;
    fixed-address 10.10.10.160;
}
$ sudo systemctl restart dhcpd
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**4.
Controleer op de DHCP-server welke IP-adressen momenteel zijn uitgegeven aan clients.
Gebruik het juiste logbestand of commando om de lease-informatie op te vragen.**

```
$ cat /var/lib/dhcpd/dhcpd.leases
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**5.
Pas de DHCP-configuratie aan zodat het lease-tijdstip voor IP-adressen wordt ingesteld op 1 uur. Herstart de DHCP-server
en controleer of de wijziging is doorgevoerd.**

```
$ sudo nano /etc/dhcp/dhcpd.conf
...
subnet 10.10.10.0 netmask 255.255.255.0 {
    range 10.10.10.150 10.10.10.200;
    option routers 10.10.10.1;
    option domain-name-servers 8.8.8.8, 8.8.4.4;
    option broadcast-address 10.10.10.255;
    default-lease-time 3600;
    max-lease-time 3600;
}
$ sudo systemctl restart dhcpd
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**6.
Voeg een tweede IP-range toe aan de DHCP-server voor een ander subnet, bijvoorbeeld 192.168.50.100 - 192.168.50.200.
Test of een client uit dit subnet een IP-adres krijgt.**

```
$ sudo nmcli connection modify "Wired Connection 1" +ipv4.addresses "192.168.50.1/24"
$ sudo nano /etc/dhcp/dhcpd.conf
...
subnet 192.168.50.0 netmask 255.255.255.0 {
    range 192.168.50.100 192.168.50.200;
    option routers 192.168.50.1;
    option domain-name-servers 8.8.8.8, 8.8.4.4;
    option broadcast-address 192.168.50.255;
    default-lease-time 3600;
    max-lease-time 3600;
}
$ sudo systemctl restart dhcpd
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**7.
Stel een client in om zijn hostname door te geven aan de DHCP-server en controleer of deze correct in de lease-lijst
verschijnt.**

```
$ sudo hostnamectl set-hostname clientMIC # client
$ sudo nmcli connection modify "Wired Connection 1" ipv4.dhcp-send-hostname yes # client

$ cat /var/lib/dhcpd/dhcpd.leases | grep -i "client-hostname" # server
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**8.
Pas de DHCP-serverconfiguratie aan zodat bepaalde clients via hun MAC-adres een kortere lease-tijd krijgen dan andere
clients. Test of dit correct werkt.**

```
$ sudo nano /etc/dhcp/dhcpd.conf
...
host short-lease-client {
    hardware ethernet 00:11:22:33:44:55;
    default-lease-time 900;
    max-lease-time 900;
}

host very-short-lease-client {
    hardware ethernet AA:BB:CC:DD:EE:FF;
    default-lease-time 300;
    max-lease-time 300;
}
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**9.
Blokkeer een specifieke client (MAC-adres) van het verkrijgen van een IP-adres via DHCP. Controleer of de client
inderdaad geen IP-adres meer ontvangt.**

```
$ sudo nano /etc/dhcp/dhcpd.conf
...
host blocked-client {
    hardware ethernet 00:11:22:33:44:55;
    deny booting;
}
$ sudo systemctl restart dhcpd
```


<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**10.
Configureer een DHCP-optie zodat clients automatisch een NTP-server (tijdserver) toegewezen krijgen.
Controleer of de client deze instelling correct ontvangt en gebruikt.**

```
$ sudo nano /etc/dhcp/dhcpd.conf
subnet 10.10.10.0 netmask 255.255.255.0 {
    range 10.10.10.150 10.10.10.200;
    option routers 10.10.10.1;
    option domain-name-servers 8.8.8.8, 8.8.4.4;
    option broadcast-address 10.10.10.255;
    default-lease-time 3600;
    max-lease-time 3600;
    
    option ntp-servers 10.10.10.1;
}
$ sudo systemctl restart dhcpd
```
