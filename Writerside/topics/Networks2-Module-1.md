# Module 1

## Boot

### Switch boot sequence

Als een **switch aan** wordt gezet gaat die door een **proces van 5 stappen**:
1. De switch laadt een POST (power-on self-test) programma vanuit de ROM.
    1. Het checkt en test de CPU, DRAM & het flash file system.
2. De switch laadt de boot loader software.
    1. Deze software is opgeslagen in de ROM.
3. De boot loader initialiseert de CPU
4. De boot loader initialiseert het flash file system
5. De boot loader vindt en laadt het OS een geeft deze controle


### Boot system command

De **switch** probeert **automatisch** te **booten via het BOOT environment variabele**.\
Als die geen waarde heeft probeert de switch de eerste executable die het vindt te gebruiken.

Het OS initialiseert daarna de interfaces via de commands in het startup-config bestand.

Het `show boot` commando toont welke boot files gebruikt wordt.

## Switch management access

**Standaard** wordt de switch **geconfigureerd via VLAN 1**.\
Voor **veiligheid** kan dit **veranderd** worden naar een **andere VLAN**.

De **andere VLAN** moet wel een **IP-adres en default gateway** hebben voor remote configuratie.

**SVI (Switch Virtual Interface):** Een virtueel **interface** (layer 3) dat **gekoppeld** is **aan** een **VLAN en** aan die VLAN
**layer 3 connectiviteit geeft**.

## Connectie

### Poort communicatie

Switch poorten kunnen:\
**Full duplex:** Beide eindes van de verbinding kunnen tegelijk sturen en ontvangen.\
**Half duplex:** Maar één kant kan sturen en ontvangen.\
**Auto:** Er wordt automatisch gekozen.

**speed 10/100/1000:** De snelheid van een switch in Mbps.

Deze instelling van de poorten kunnen manueel aangepast worden.

Op een interface:
```
S1(config-if)# duplex full
S1(config-if)# speed 100
```

### Auto-MDIX

Bepaalde kabels moeten gebruikt worden in specifieke scenarios:\
**Straight-through:** Verbind andere soorten apparaten met elkaar (bv. switch & computer).\
**Crossover:** Verbind gelijkaardige apparaten met elkaar (bv. computer & computer).

**Auto-MDIX** lost problemen op door **automatisch de connectie aan te passen aan de kabel**.

Commando op een interface om dit aan te zetten:
```
S1(config-if)# mdix auto
```

**Met `mdix auto` moeten de speed en duplex ook op auto staan.**

### Interface errors

Het `show interfaces <interface>` commando kan errors tonen.

<table>
    <tr>
        <td>Error type</td>
        <td>Beschrijving</td>
    </tr>
    <tr>
        <td colspan="2"><format style="bold">Input errors</format></td>
    </tr>
    <tr>
        <td>Runts</td>
        <td>Frames die weg zijn gedaan omdat ze kleiner waren dan het minimum frame size.</td>
    </tr>
    <tr>
        <td>Giants</td>
        <td>Frames die weg zijn gedaan omdat ze groter waren dan het maximum frame size.</td>
    </tr>
    <tr>
        <td>CRC</td>
        <td>Cyclic Redundancy Check, wanneer de berekende checksum niet overeenkomt met de ontvangen checksum.</td>
    </tr>
    <tr>
        <td colspan="2"><format style="bold">Output errors</format></td>
    </tr>
    <tr>
        <td>Collisions</td>
        <td>Aantal berichten die opnieuw gestuurd zijn vanwege Ethernet botsingen.</td>
    </tr>
    <tr>
        <td>Late Collisions</td>
        <td>Aantal berichten waar een botsing is gebeurd nadat er 512 bits van het frame zijn verstuurd.</td>
    </tr>
</table>

### IPv4 Loopback Interfaces

Een **loopback interface** is intern in een router. Het is **niet toegewezen aan een fysieke poort**.\
Het kan gebruikt worden om interne routering processen te testen.

Je kan meerdere loopback interfaces maken op een router om meer netwerken te simuleren.
```
R1(config)# interface loopback 0
R1(config-if)# ip address 10.0.0.1 255.255.255.0
R1(config-if)# exit
R1(config)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback0, changed state to up
```
