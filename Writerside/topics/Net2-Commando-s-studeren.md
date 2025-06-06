# Praktijk studeren

## Basic Device Configuration

<deflist collapsible="true">
<def title="Zet de interface g0/0/1 op full duplex en 100 Mbps.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# duplex full
    Switch(config-if)# speed 100
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon kort de IPv4 interfaces en daarna de VLANs.">
    <code-block>
    Switch# show ip interface brief
    Switch# show vlan brief
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon de MAC adres tabel.">
    <code-block>
    Switch# show mac-address-table
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon de status van de interfaces.">
    <code-block>
    Switch# show interfaces status
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet SSH aan.">
    <code-block>
    Switch(config)# ip domain-name pxl.be
    Switch(config)# crypto key generate rsa general-keys modulus 2048
    Switch(config)# username admin secret wachtwoord
    Switch(config)# line vty 0 4
    Switch(config-line)# transport input ssh
    Switch(config-line)# login local
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet de hostname van een switch.">
    <code-block>
    Switch(config)# hostname Switch1
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een wachtwoord op de console en de vty lijnen.">
    <code-block>
    Switch(config)# line con 0
    Switch(config-line)# password wachtwoord
    Switch(config-line)# login
    Switch(config-line)# exit
    Switch(config)# line vty 0 15
    Switch(config-line)# password wachtwoord
    Switch(config-line)# login
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een wachtwoord op de config modus.">
    <code-block>
    Switch(config)# enable secret wachtwoord
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Encrypteer de wachtwoorden.">
    <code-block>
    Switch(config)# service password-encryption
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een banner (motd)">
    <code-block>
    Switch(config)# banner motd #cool bericht#
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een IPv4 adres op een interface.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# ip address 192.168.10.10 255.255.255.0
    Switch(config-if)# no sh
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet IPv6 aan en zet een IPv6 adres op een interface.">
    <code-block>
    Switch(config)# ipv6 unicast-routing
    Switch(config)# int g0/0/1
    Switch(config-if)# ipv6 address 2001:db8:1::1/64
    Switch(config-if)# no sh
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon de actieve IPv4 interfaces.">
    <code-block>
    Switch# show ip interface brief | include up
    </code-block>
</def>
</deflist>

## VLANs

<deflist collapsible="true">
<def title="Maak een VLAN en geef deze een naam.">
    <code-block>
    Switch(config)# vlan 10
    Switch(config-vlan)# name Data_Users
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een interface in een VLAN.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport mode access
    Switch(config-if)# switchport access vlan 10
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een interface in trunk mode, de native VLAN moet 99 zijn.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport mode trunk
    Switch(config-if)# switchport trunk allowed vlan 10,20
    Switch(config-if)# switchport trunk native vlan 99
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet QoS op een interface voor voice VLAN 20 en Data_Users VLAN 10.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport mode access
    Switch(config-if)# switchport access vlan 10
    Switch(config-if)# switchport voice vlan 20
    Switch(config-if)# mls qos trust cos
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Maak VLAN 10,20 en native VLAN 99 ongedaan op een trunk interface.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# no switchport trunk allowed vlan
    Switch(config-if)# no switchport trunk native vlan
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een interface op de mode dynamic desirable.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport mode dynamic desirable
    </code-block>
</def>
</deflist>

## Inter-VLAN Routing

<deflist collapsible="true">
<def title="Voeg een IP toe aan een VLAN-interface.">
    <code-block>
    Switch(config)# int vlan 10
    Switch(config-if)# ip address 192.168.20.20 255.255.255.0
    Switch(config-if)# no sh
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel een default gateway in op een layer 2 switch.">
    <code-block>
    Switch(config)# ip default-gateway 192.168.20.1
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Configureer een subinterface op een router voor VLAN 10.">
    <code-block>
    Router(config)# int g0/0.10
    Router(config-subif)# encapsulation dot1Q 10
    Router(config-subif)# ip address 192.168.10.1 255.255.255.0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Wat zijn de stappen om inter-VLAN routing met router-on-a-stick te configureren? (geen commando's)">
    <code-block>
    1. Maak subinterfaces aan op de router.
    2. Zet encapsulation dot1Q aan voor de VLAN.
    3. Wijs IP-adressen toe aan de subinterfaces.
    4. Verbind de router met een trunk poort van de switch.
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Maak 2 SVI VLAN-interfaces en geef ze een IP-adres.">
    <code-block>
    Switch(config)# int vlan 10
    Switch(config-if)# ip address 192.168.10.1 255.255.255.0
    Switch(config-if)# no sh
    Switch(config-if)# exit
    Switch(config)# int vlan 20
    Switch(config-if)# ip address 192.168.20.1 255.255.255.0
    Switch(config-if)# no sh
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Configureer access poorten voor VLAN 10 en 20.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport mode access
    Switch(config-if)# switchport access vlan 10
    Switch(config-if)# exit
    Switch(config)# int g0/0/2
    Switch(config-if)# switchport mode access
    Switch(config-if)# switchport access vlan 20
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet ip routing aan.">
    <code-block>
    Switch(config)# ip routing
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Wat zijn de stappen om inter-VLAN routing op een layer 3 switch te configureren? (geen commando's)">
    <code-block>
    1. Maak VLANs aan.
    2. Maak een SVI voor elke VLAN.
    3. Wijs IP-adressen toe aan de SVI's.
    4. Configureer access poorten.
    5. Zet ip routing aan.
    </code-block>
</def>
</deflist>

## STP Concepts

<deflist collapsible="true">
<def title="Toon de samenvatting van de STP configuratie.">
    <code-block>
    Switch# show spanning-tree summary
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Verander de bridge prioriteit naar 4096.">
    <code-block>
    Switch(config)# spanning-tree vlan 1 priority 4096
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet de spanning tree mode op rapid-pvst.">
    <code-block>
    Switch(config)# spanning-tree mode rapid-pvst
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet PortFast en BPDU Guard aan op een interface.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# spanning-tree portfast
    Switch(config-if)# spanning-tree bpduguard enable
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet PortFast en BPDU Guard aan op een range van poorten.">
    <code-block>
    Switch(config)# int range g0/0/5 - 24
    Switch(config-if-range)# spanning-tree portfast
    Switch(config-if-range)# spanning-tree bpduguard enable
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet op een interface de poort priority op 64.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# spanning-tree port-priority 64
    </code-block>
</def>
</deflist>

## EtherChannel

<deflist collapsible="true">
<def title="Maak een EtherChannel aan met LACP (active) op poort g0/0/1 en g0/0/2.">
    <code-block>
    Switch(config)# int range g0/0/1 - 2
    Switch(config-if-range)# channel-group 1 mode active
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet het EtherChannel interface in trunk mode en laat vlan 10 en 20 toe + native vlan 99.">
    <code-block>
    Switch(config)# int port-channel 1
    Switch(config-if)# switchport mode trunk
    Switch(config-if)# switchport trunk allowed vlan 10,20
    Switch(config-if)# switchport trunk native vlan 99
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon de samenvatting van de EtherChannel configuratie.">
    <code-block>
    Switch# show etherchannel summary
    </code-block>
</def>
</deflist>

## DHCPv4

<deflist collapsible="true">
<def title="Stel in dat de IP-adressen van 192.168.10.1 tot en met 192.168.10.20 niet gebruikt mogen worden door DHCP.">
    <code-block>
    Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.20
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Wat zijn de stappen om DHCP op een router te configureren? (geen commando's)">
    <code-block>
    1. Sluit de IP-adressen die niet door DHCP gebruikt mogen worden uit.
    2. Maak een DHCP-pool aan.
    3. Stel het netwerk, default-router, DNS-server en lease tijd in.
    4. (Optioneel) Stel een domeinnaam in.
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="De eerste 10 IP-adressen van 192.168.10.0/24 mogen niet gebruikt worden, de rest wel. Configureer de DHCP pool volledig.">
    <code-block>
    Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.10
    Router(config)# ip dhcp pool pool_naam
    Router(dhcp-config)# network 192.168.10.0 255.255.255.0
    Router(dhcp-config)# default-router 192.168.10.1
    Router(dhcp-config)# dns-server 192.168.10.2
    Router(dhcp-config)# lease 7
    Router(dhcp-config)# domain-name pxl.be
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon de DHCP-leases.">
    <code-block>
    Router# show ip dhcp binding
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon de DHCP configuratie.">
    <code-block>
    Router# show running-config | section dhcp
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet DHCP uit.">
    <code-block>
    Router(config)# no service dhcp
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel een DHCP-relay in op een interface naar 192.168.11.2.">
    <code-block>
    Router(config)# int g0/0/1
    Router(config-if)# ip helper-address 192.168.11.2
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel een interface in zodat deze een IP krijgt via DHCP.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# ip address dhcp
    Switch(config-if)# no sh
    </code-block>
</def>
</deflist>

## FHRP Concepts

<deflist collapsible="true">
<def title="Configureer HSRP op Router1 (192.168.10.2) en Router2 (192.168.10.3) met het virtual IP 192.168.10.1.">
    <code-block>
    Router1(config)# int g0/0/1
    Router1(config-if)# ip address 192.168.10.2 255.255.255.0
    Router1(config-if)# standby 1 ip 192.168.10.1
    Router1(config-if)# standby 1 priority 110
    Router1(config-if)# standby 1 preempt
    Router2(config)# int g0/0/1
    Router2(config-if)# ip address 192.168.10.3 255.255.255.0
    Router2(config-if)# standby 1 ip 192.168.10.1
    Router2(config-if)# standby 1 priority 100
    Router2(config-if)# standby 1 preempt
    </code-block>
</def>
</deflist>

## Switch Security Configuration

<deflist collapsible="true">
<def title="Zet poort 8 tot en met 24 uit.">
    <code-block>
    Switch(config)# int range g0/0/8 - 24
    Switch(config-if-range)# shutdown
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet poort security aan op een poort.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport port-security
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet poort security aan op een poort en stel het maximum aantal MAC-adressen in op 2.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport port-security
    Switch(config-if)# switchport port-security maximum 2
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet poort security aan en zorg dat het MAC-adres dat verbonden is, vast staat.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport port-security
    Switch(config-if)# switchport port-security mac-address sticky
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet poort security aan en zorg dat de poort packets van onbekende MAC-adressen laat vallen en een syslog bericht stuurt.">
    <code-block>
    Switch(config)# int g0/0/1
    Switch(config-if)# switchport port-security
    Switch(config-if)# switchport port-security violation restrict
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon de poort security configuratie voor een specifiek interface.">
    <code-block>
    Switch# show port-security interface g0/0/1
    </code-block>
</def>
</deflist>



