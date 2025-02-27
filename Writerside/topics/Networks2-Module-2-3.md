# Module 2 &amp; 3

## Switching in Networking

**Flooding:** Wanneer een **unicast naar alle poorten** wordt gestoord behalve naar de ontvangst poort. Wordt gebruikt als
een switch een MAC adres niet kent.

**Ingress:** De **poort** waar een frame **binnenkomt**.\
**Egress:** De **poort** waar een frame **verstuurd wordt**.

**Collision domain:** De **area** (in een logische topology) **waar, als een collision gebeurt** alle **apparaten tijdelijk
moeten wachten met communicatie**. Dit kan meerdere apparaten bevatten, maar is ook bij elke kabel. Als er dus een aantal
apparaten via één kabel ergens mee verbonden zijn, dan zitten ze in een collision domain.

## VLAN's

**VLAN:** Een groep van apparaten die **fysiek verbonden** zijn, maar **virtueel gescheiden** zijn.

**Waarom:**
- **Betere beveiliging**
    - Je kan verschillende beveiligingsregels zetten op elke VLAN.
- **Minder broadcast verkeer**
    - Broadcasts worden niet naar andere VLAN's verstuurd.
- **Geen kosten om fysiek te scheiden**
    - Moet niet extra hardware aankopen

**Frames krijgen een tag om de VLAN te identificeren.**

### VLAN type's

- **Default VLAN**
    - Standaard wordt VLAN 1 voor alles gebruikt
    - Extra VLAN's die worden toegevoegd nemen een deel van VLAN 1 over
    - Kan geen andere naam krijgen, kan niet verwijderen
    - VLAN ID 1
- **Data VLAN**
    - Om netwerk verkeer van gebruikers te scheiden
    - Scheid het netwerk in groepen van gebruikers of apparaten
- **Native VLAN**
    - Untagged frame
    - Voor netwerk verkeer dat geen tag heeft
- **Management VLAN**
    - VLAN specifiek voor beheer van het netwerk.
    - SSH, Telnet, HTTPS, HTTP & SNMP
- **Voice VLAN**
    - VLAN voor VoIP
    - Bandbreedte belangrijk

## VLAN configuratie

**Normal range VLAN's:**
- Gebruikt in klein tot middelgrote bedrijven
- Configuratie wordt opgeslagen in flash memory
- VLAN ID 1 - 1005
- ID 1002 - 1005 zijn gereserveerd voor oude technologieën
- ID 1 & 1002 - 1005 kunnen niet verwijderd worden

**Extended range VLAN's:**
- VLAN ID 1006 - 4094
- Gebruikt door grote bedrijven
- Configuratie wordt opgeslagen in running-config

## VLAN trunks

Een VLAN kan niet over een andere VLAN.\
Stel dat er één poort is die maar één VLAN mag gebruiken, maar andere nodig hebben.

In dat scenario wordt een **trunk** gebruikt. Een trunk **laat meer dan één VLAN op een poort toe**.\
Dit gebruikt het **IEEE 802.1Q** protocol (uitgesproken als "dot one q").

## Dynamic Trunking Protocol

Werkt alleen op switches van Cisco. 

**DTP (Dynamic Trunking Protocol)** zorgt dat sommige Cisco **switches automatisch trunking** kunnen **onderhandelen** met de
**switch die** er **naast staat**.

Dit werkt zoals Auto-MDIX, de switch kiest automatisch welke modus de poort op staat.

<table style="both">
    <tr>
      <td>Switch 1 ↓ 2 →</td>
      <td>Dynamic Auto</td>
      <td>Dynamic Desirable</td>
      <td>Trunk</td>
      <td>Access</td>
    </tr>
    <tr>
      <td>Dynamic Auto</td>
      <td>Access</td>
      <td>Trunk</td>
      <td>Trunk</td>
      <td>Access</td>
    </tr>
    <tr>
      <td>Dynamic Desirable</td>
      <td>Trunk</td>
      <td>Trunk</td>
      <td>Trunk</td>
      <td>Access</td>
    </tr>
    <tr>
      <td>Trunk</td>
      <td>Trunk</td>
      <td>Trunk</td>
      <td>Trunk</td>
      <td>Limited connectivity</td>
    </tr>
    <tr>
      <td>Access</td>
      <td>Access</td>
      <td>Access</td>
      <td>Limited connectivity</td>
      <td>Access</td>
    </tr>
</table>

