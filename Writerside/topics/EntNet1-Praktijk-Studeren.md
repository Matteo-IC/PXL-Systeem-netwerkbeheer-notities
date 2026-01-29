# Praktijk Studeren

## OSPF

<deflist collapsible="true">
<def title="Zet OSPF aan met PID 10.">
    <code-block>
    Router(config)# router ospf 10
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet het IP 1.1.1.1 als router ID met behulp van een loopback interface.">
    <code-block>
    Router(config)# interface Loopback 1
    Router(config-if)# ip address 1.1.1.1 255.255.255.255
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Ga in router configuratie modus en zet het router ID op 1.1.1.1.">
    <code-block>
    Router(config)# router ospf 10
    Router(config-router)# router-id 1.1.1.1
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Het router ID is fout geconfigureerd, check eerst wat het nu is en verander het daarna naar 1.1.1.1.">
    <code-block>
    Router# show ip protocols
    ...
    Router ID 1.1.1.2
    ...
    Router# configure terminal
    Router(config)# router ospf 10
    Router(config-router)# router-id 1.1.1.1
    Router(config-router)# end
    Router# clear ip ospf process
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="In een Point-to-Point OSPF netwerk, zet OSPF aan op alle interfaces die een IP hebben binnen 192.168.1.0/24.">
    <code-block>
    Router(config)# router ospf 10
    Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="In een Point-to-Point OSPF netwerk, zet OSPF aan op alle interfaces die een IP hebben binnen 192.168.1.0/30.">
    <code-block>
    Router(config)# router ospf 10
    Router(config-router)# network 192.168.1.0 0.0.0.3 area 0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="In een Point-to-Point OSPF netwerk, zet OSPF aan op enkel de interface met IP 192.168.1.12.">
    <code-block>
    Router(config)# router ospf 10
    Router(config-router)# network 192.168.1.12 0.0.0.0 area 0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet OSPF aan op de interface GigabitEthernet 0/0/0.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip ospf 10 area 0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel de interface loopback 0 in als een passive interface.">
    <code-block>
    Router(config)# router ospf 10
    Router(config-router)# passive-interface loopback 0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon informatie over de OSPF-configuratie op het huidig apparaat.">
    <code-block>
    Router# show ip protocols
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon informatie over OSPF op interface GigabitEthernet 0/0/0.">
    <code-block>
    Router# show ip ospf interface GigabitEthernet 0/0/0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet interface GigabitEthernet 0/0/0 om naar point-to-point.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip ospf network point-to-point
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Met welk commando kan je zien wie de OSPF neighbors zijn en wat hun status is?">
    <code-block>
    Router# show ip ospf neighbor
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel de OSPF-prioriteit van interface GigabitEthernet 0/0/0 in op 255.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip ospf priority 255
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel de OSPF-prioriteit van interface GigabitEthernet 0/0/0 in zodat de router nooit DR of BDR wordt.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip ospf priority 0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel de OSPF referentie bandbreedte in op 1000 Mbps.">
    <code-block>
    Router(config)# router ospf 10
    Router(config-router)# auto-cost reference-bandwidth 1000
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel de OSPF kost van interface GigabitEthernet 0/0/0 in op 10.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip ospf cost 10
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Welk commando gebruik je om de standaard OSPF Hello en Dead intervallen te bekijken op een interface?">
    <code-block>
    Router# show ip ospf interface GigabitEthernet 0/0/0
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Met welk commando kan je de timer van het Dead interval zien voor de neighbors?">
    <code-block>
    Router# show ip ospf neighbor
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel het OSPF Hello interval in op 5 seconden en het Dead interval op 20 seconden op interface GigabitEthernet 0/0/0.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip ospf hello-interval 5
    Router(config-if)# ip ospf dead-interval 20
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Stel een default static route in op interface GigabitEthernet 0/0/1 en adverteer deze in OSPF.">
    <code-block>
    Router(config)# ip route 0.0.0.0 0.0.0.0 GigabitEthernet 0/0/1
    Router(config)# router ospf 10
    Router(config-router)# default-information originate
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Check of de default route wordt geadverteerd in OSPF.">
    <code-block>
    Router# show ip route | begin Gateway
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet OSPF aan, stel een router ID in en activeer OSPF op interface GigabitEthernet 0/0/0 en 0/0/1.">
    <code-block>
    Router(config)# router ospf 10
    Router(config-router)# router-id 1.1.1.1
    Router(config-router)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip ospf 10 area 0
    Router(config-if)# interface GigabitEthernet 0/0/1
    Router(config-if)# ip ospf 10 area 0
    </code-block>
</def>
</deflist>

## IPv4 ACL's

<deflist collapsible="true">
<def title="Schrijf een standaard genummerde IPv4 ACL die verkeer van 192.168.5.0/24 blokkeert.">
    <code-block>
    Router(config)# access-list 10 deny 192.168.5.0 0.0.0.255
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Verwijder een genummerde IPv4 ACL met nummer 10.">
    <code-block>
    Router(config)# no access-list 10
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Schrijf een standaard IPv4 ACL met naam 'PERMIT-SALES' die verkeer van 192.168.4.0/25 toe staat.">
    <code-block>
    Router(config)# ip access-list standard PERMIT-SALES
    Router(config-std-nacl)# permit 192.168.4.0 0.0.0.127
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Blokkeer verkeer van het IP 192.168.8.4 en laat al het andere verkeer toe in een standaard IPv4 ACL met naam 'DENY-IP'.">
    <code-block>
    Router(config)# ip access-list standard DENY-IP
    Router(config-std-nacl)# deny 192.168.8.4
    Router(config-std-nacl)# permit any
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet de ACL 'PERMIT-SALES' op interface GigabitEthernet 0/0/0 in de inkomende richting.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip access-group PERMIT-SALES in
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon alle ACL's op het apparaat.">
    <code-block>
    Router# show access-lists
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Check of de ACL 'PERMIT-SALES' op interface GigabitEthernet 0/0/0 is toegepast.">
    <code-block>
    Router# show ip interface GigabitEthernet 0/0/0 | include access list
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Toon de ACL's, de ACL 'DENY-IP' heeft een foute ACE van sequence nummer 10, vervang deze door een ACE die 192.168.8.5 blokkeert.">
    <code-block>
    Router# show access-lists
    ...
    Router(config)# ip access-list standard DENY-IP
    Router(config-std-nacl)# no 10
    Router(config-std-nacl)# 10 deny 192.168.8.5
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Zet de ACL 'PERMIT-ADMIN' op de vty lijnen in de inkomende richting.">
    <code-block>
    Router(config)# line vty 0 4
    Router(config-line)# access-class PERMIT-ADMIN in
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Met welk commando kan je zien hoe vaak een ACE in een ACL is toegepast?">
    <code-block>
    Router# show access-lists
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Wat moet je toevoegen aan een ACL om te zien hoeveel keer de standaard deny any is toegepast?">
    <code-block>
    Router(config-std-nacl)# deny any
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Configureer een genummerde extended IPv4 ACL die HTTPS verkeer toelaat.">
    <code-block>
    Router(config)# access-list 110 permit tcp any any eq 443
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Pas de genummerde extended IPv4 ACL 110 toe op interface GigabitEthernet 0/0/1 in de inkomende richting.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/1
    Router(config-if)# ip access-group 110 in
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Schrijf een genummerde extended IPv4 ACL die al het tcp verkeer toelaat op poort 80 van het 10.1.1.0/24 subnet naar IP 10.1.2.1.">
    <code-block>
    Router(config)# access-list 120 permit tcp 10.1.1.0 0.0.0.255 10.1.2.1 eq 80
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Maak een genummerde extended IPv4 ACL die alleen tcp verkeer toelaat dat gestart is door hosts binnen het 192.168.10.0/24 subnet.">
    <code-block>
    Router(config)# access-list 120 permit tcp any 192.168.10.0 0.0.0.255 established
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Schrijf 1 extended ACL met naam 'PERMIT-WEB' die zowel HTTP als HTTPS verkeer toelaat naar subnet 192.168.1.0/24 en 1 ACL met naam 'PERMIT-ESTABLISHED' die alleen tcp verkeer toelaat dat gestart is door hosts binnen het 192.168.1.0/24 subnet.">
    <code-block>
    Router(config)# ip access-list extended PERMIT-WEB
    Router(config-ext-nacl)# permit tcp 192.168.1.0 0.0.0.255 any eq 80
    Router(config-ext-nacl)# permit tcp 192.168.1.0 0.0.0.255 any eq 443
    Router(config-ext-nacl)# exit
    Router(config)# ip access-list extended PERMIT-ESTABLISHED
    Router(config-ext-nacl)# permit tcp any 192.168.1.0 0.0.0.255 established
    </code-block>
</def>
</deflist>

<deflist collapsible="true">
<def title="Pas ACL 'PERMIT-WEB' toe op inkomend verkeer op interface GigabitEthernet 0/0/0 en ACL 'PERMIT-ESTABLISHED' op uitgaand verkeer op dezelfde interface.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip access-group PERMIT-WEB in
    Router(config-if)# ip access-group PERMIT-ESTABLISHED out
    </code-block>
</def>
</deflist>

## IPv4 NAT

<deflist collapsible="true">
<def title="Maak een static NAT mapping voor het inside local IP: 192.168.1.18 en het inside global IP: 203.85.4.71">
    <code-block>
    Router(config)# ip nat inside source static 192.168.1.18 203.85.4.71
    </code-block>
</def>
<def title="Configureer nu 2 interfaces, GigabitEthernet 0/0/0 als inside en GigabitEthernet 0/0/1 als outside.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip nat inside
    Router(config)# interface GigabitEthernet 0/0/1
    Router(config-if)# ip nat outside
    </code-block>
</def>
<def title="Check of de NAT configuratie gelukt is.">
    <code-block>
    Router# show ip nat translations
    </code-block>
</def>
<def title="Configureer een dynamische NAT pool met de naam 'NAT-POOL1' die een range van 5 IP-adressen bevat: 201.78.61.1 tot en met 201.78.61.6">
    <code-block>
    Router(config)# ip nat pool NAT-POOL1 201.78.61.1 201.78.61.6 netmask 255.255.255.248
    </code-block>
</def>
<def title="Maak een access-list die bepaalt dat alleen 192.168.0.0/16 mogen worden vertaald.">
    <code-block>
    Router(config)# access-list 20 permit 192.168.0.0 0.0.255.255
    </code-block>
</def>
<def title="Koppel de NAT pool en de access-list aan elkaar.">
    <code-block>
    Router(config)# ip nat inside source list 20 pool NAT-POOL1
    </code-block>
</def>
<def title="Configureer nu 2 interfaces, GigabitEthernet 0/0/0 als inside en GigabitEthernet 0/0/1 als outside.">
    <code-block>
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip nat inside
    Router(config)# interface GigabitEthernet 0/0/1
    Router(config-if)# ip nat outside
    </code-block>
</def>
<def title="Configureer PAT voor één enkel publiek IP-adres op GigabitEthernet 0/0/1 en het privé subnet 192.168.0.0/24">
    <code-block>
    Router(config)# ip nat inside source list 30 interface GigabitEthernet 0/0/1 overload
    Router(config)# access-list 30 permit 192.168.0.0 0.0.0.255
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip nat inside
    Router(config)# interface GigabitEthernet 0/0/1
    Router(config-if)# ip nat outside
    </code-block>
</def>
<def title="Configureer PAT voor een address pool van 201.78.61.1 tot en met 201.78.61.6 en het privé subnet 192.168.0.0/16">
    <code-block>
    Router(config)# ip nat pool NAT-POOL2 201.78.61.1 201.78.61.6 netmask 255.255.255.248
    Router(config)# access-list 40 permit 192.168.0.0 0.0.255.255
    Router(config)# ip nat inside source list 40 pool NAT-POOL2 overload
    Router(config)# interface GigabitEthernet 0/0/0
    Router(config-if)# ip nat inside
    Router(config)# interface GigabitEthernet 0/0/1
    Router(config-if)# ip nat outside
    </code-block>
</def>
</deflist>
