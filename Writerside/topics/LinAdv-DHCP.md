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