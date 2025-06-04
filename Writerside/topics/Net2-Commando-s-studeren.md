# Praktijk studeren

## Basic Device Configuration

<deflist collapsible="true">
<def title="Zet de interface g0/0/1 op full duplex en 100 Mbps.">
    <code-block>
    Switch(config)# interface g0/0/1
    Switch(config-if)# duplex full
    Switch(config-if)# speed 100
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon kort de IPv4 interfaces en de VLANs.">
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
    Switch(config)# crypto key generate rsa
    How many bits in the modulus [512]: 1024
    Switch(config)# username admin secret wachtwoord
    Switch(config)# line vty 0 15
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
    Switch(config)# interface g0/0/1
    Switch(config-if)# ip address 192.168.10.10 255.255.255.0
    Switch(config-if)# no sh
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet IPv6 aan en zet een IPv6 adres op een interface.">
    <code-block>
    Switch(config)# ipv6 unicast-routing
    Switch(config)# interface g0/0/1
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

## Switching Concepts

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
    Switch(config)# interface g0/0/1
    Switch(config-if)# switchport mode access
    Switch(config-if)# switchport access vlan 10
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een interface in trunk mode, de native VLAN moet 99 zijn.">
    <code-block>
    Switch(config)# interface g0/0/1
    Switch(config-if)# switchport mode trunk
    Switch(config-if)# switchport trunk allowed vlan 10,20
    Switch(config-if)# switchport trunk native vlan 99
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet QoS op een interface voor voice VLAN 20 en Data_Users VLAN 10.">
    <code-block>
    Switch(config)# interface g0/0/1
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
    Switch(config)# interface g0/0/1
    Switch(config-if)# no switchport trunk allowed vlan
    Switch(config-if)# no switchport trunk native vlan
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet een interface op de mode dynamic desirable.">
    <code-block>
    Switch(config)# interface g0/0/1
    Switch(config-if)# switchport mode dynamic desirable
    </code-block>
</def>
</deflist>

## Inter-VLAN Routing

<deflist collapsible="true">
<def title="Voeg een IP toe aan een VLAN-interface.">
    <code-block>
    Switch(config)# interface vlan 10
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
    Router(config)# interface g0/0.10
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
    Switch(config)# interface vlan 10
    Switch(config-if)# ip address 192.168.10.1 255.255.255.0
    Switch(config-if)# no sh
    Switch(config-if)# exit
    Switch(config)# interface vlan 20
    Switch(config-if)# ip address 192.168.20.1 255.255.255.0
    Switch(config-if)# no sh
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Configureer access poorten voor VLAN 10 en 20.">
    <code-block>
    Switch(config)# interface g0/0/1
    Switch(config-if)# switchport mode access
    Switch(config-if)# switchport access vlan 10
    Switch(config-if)# exit
    Switch(config)# interface g0/0/2
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

