# Module 4

**VLANs kunnen niet met elkaar communiceren** zonder extra hulp. Dit is waar **inter-VLAN routing helpt**.

## Inter-VLAN routing

Inter-VLAN routing is het proces van **netwerk verkeer van één VLAN naar een andere VLAN** te sturen.

Er zijn **2 opties** voor inter-VLAN routing:
- **Router-on-a-stick**
- **Layer 3 switch met Switched Virtual Interfaces (SVIs)**

## Router-on-a-stick

Een **interface** op een **router** is geconfigureerd als een **802.1Q trunk**.\
Die is **verbonden met** een **trunk poort op** een **layer 2 switch**.\
De **interface** gebruikt **subinterfaces** om verkeer van **verschillende VLANs** te routeren.

### Subinterfaces

Een **subinterface is** een **virtueel interface** op een ander interface.\
Elk subinterface heeft een **uniek VLAN ID** en een **IP-adres**.

Wanneer een **frame** van een VLAN **naar** de **router wordt gestuurd**, wordt het **VLAN ID gebruikt** om het juiste
**subinterface** te **identificeren**.\
De router **verandert** de **VLAN tag naar** de **nieuwe VLAN** en **stuurt het door** naar de **juiste VLAN**.

```
VLAN 10 ──┐           
VLAN 20 ──┤ ←→ Switch ←→ Router (G0/0/0.10 → G0/0/0.20)
VLAN 30 ──┘
```

## Layer 3 switch met SVIs

Dit is de **meest efficiënte** manier om **inter-VLAN routing** te doen.\
**Per VLAN** wordt een **SVI geconfigureerd**, de routering is sneller omdat de frames niet nog naar een router moeten en omdat
de switch efficiëntere hardware gebruikt.

```
VLAN 10 ──┐
VLAN 20 ──┤ ←→ Layer 3 Switch (SVI 10 → SVI 20)
VLAN 30 ──┘
```

## Configuratie

### Router-on-a-stick Configuratie

```
Topologie:
      ┌───────┐
      │Router │
      └───┬───┘
          │
      ┌───┴───┐  
      │Switch │
      └───┬───┘
          │
     ╭────┼────╮
     │    │    │
    PC1  PC2  PC3
VLAN10 VLAN20 VLAN30
```

<tabs>
<tab title="1. VLANs switch">
    <code-block>
        Switch(config)# vlan 10
        Switch(config-vlan)# name VLAN10
        Switch(config)# vlan 20
        Switch(config-vlan)# name VLAN20
        Switch(config)# vlan 30
        Switch(config-vlan)# name VLAN30
    </code-block>
</tab>
<tab title="2. Trunk router">
    <code-block>
        Switch(config)# int g0/1
        Switch(config-if)# sw mo tr
        Switch(config-if)# sw tr allowed vlan 10,20,30
    </code-block>
</tab>
<tab title="3. Access ports PCs">
    <code-block>
        Switch(config)# int f0/1
        Switch(config-if)# sw mo acc
        Switch(config-if)# sw acc vlan 10
        Switch(config)# int f0/2
        Switch(config-if)# sw mo acc
        Switch(config-if)# sw acc vlan 20
        Switch(config)# int f0/3
        Switch(config-if)# sw mo acc
        Switch(config-if)# sw acc vlan 30
    </code-block>
</tab>
<tab title="4. Router subinterfaces">
    <code-block>
        Router(config)# int g0/0/0
        Router(config-if)# no sh
        Router(config)# int g0/0/0.10
        Router(config-subif)# encapsulation dot1Q 10
        Router(config-subif)# ip address 192.168.10.1 255.255.255.0
        Router(config)# int g0/0/0.20
        Router(config-subif)# encapsulation dot1Q 20
        Router(config-subif)# ip address 192.168.20.1 255.255.255.0
        Router(config)# int g0/0/0.30
        Router(config-subif)# encapsulation dot1Q 30
        Router(config-subif)# ip address 192.168.30.1 255.255.255.0
    </code-block>
</tab>
<tab title="5. PC configuratie">
    <code-block>
        PC1 (VLAN 10):
        - IP: 192.168.10.10
        - Gateway: 192.168.10.1
        PC2 (VLAN 20):
        - IP: 192.168.20.10
          - Gateway: 192.168.20.1
        PC3 (VLAN 30):
        - IP: 192.168.30.10
          - Gateway: 192.168.30.1
    </code-block>
</tab>
</tabs>

### Layer 3 Switch Configuratie

```
Topologie:
   ┌──────────────┐
   │Layer 3 Switch│
   └──────┬───────┘
          │
     ╭────┼────╮
     │    │    │
    PC1  PC2  PC3
VLAN10 VLAN20 VLAN30
```

<tabs>
<tab title="1. IP routing">
    <code-block>
        Switch(config)# ip routing
    </code-block>
</tab>
<tab title="2. VLANs switch">
    <code-block>
        Switch(config)# vlan 10
        Switch(config-vlan)# name VLAN10
        Switch(config)# vlan 20
        Switch(config-vlan)# name VLAN20
        Switch(config)# vlan 30
        Switch(config-vlan)# name VLAN30
    </code-block>
</tab>
<tab title="3. SVIs">
    <code-block>
        Switch(config)# int vlan 10
        Switch(config-if)# ip address 192.168.10.1 255.255.255.0
        Switch(config)# int vlan 20
        Switch(config-if)# ip address 192.168.20.1 255.255.255.0
        Switch(config)# int vlan 30
        Switch(config-if)# ip address 192.168.30.1 255.255.255.0
    </code-block>
</tab>
<tab title="4. Access ports PCs">
    <code-block>
        Switch(config)# int f0/1
        Switch(config-if)# sw mo acc
        Switch(config-if)# sw acc vlan 10
        Switch(config)# int f0/2
        Switch(config-if)# sw mo acc
        Switch(config-if)# sw acc vlan 20
        Switch(config)# int f0/3
        Switch(config-if)# sw mo acc
        Switch(config-if)# sw acc vlan 30
    </code-block>
</tab>
<tab title="5. PC configuratie">
    <code-block>
        PC1 (VLAN 10):
        - IP: 192.168.10.10
        - Gateway: 192.168.10.1
        PC2 (VLAN 20):
        - IP: 192.168.20.10
          - Gateway: 192.168.20.1
        PC3 (VLAN 30):
        - IP: 192.168.30.10
          - Gateway: 192.168.30.1
    </code-block>
</tab>
</tabs>

## Troubleshooting

<table>
    <tr>
        <td>Probleem</td>
        <td>Oplossing</td>
        <td>Checken</td>
    </tr>
    <tr>
        <td>Ontbrekende VLANs</td>
        <td>Maak ontbrekende VLANs aan.<br>
            Zorg dat de VLANs op de juiste poorten zijn.
        </td>
        <td><code>show vlan brief</code><br>
            <code>show interfaces switchport</code>
        </td>
    </tr>
    <tr>
        <td>Switch trunk poort</td>
        <td>Zorg dat trunks goed staan.</td>
        <td><code>show interfaces trunk</code></td>
    </tr>
    <tr>
        <td>Switch access poort</td>
        <td>Zet de juiste VLAN op de juiste poort<br>
            Zorg dat de poort in access mode staat.
        </td>
        <td><code>show interfaces switchport</code><br>
            <code>show running-config interface</code>
        </td>
    </tr>
</table>