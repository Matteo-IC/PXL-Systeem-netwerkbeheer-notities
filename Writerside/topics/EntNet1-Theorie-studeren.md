# Theorie studeren

## OSPF

<deflist collapsible="true">
<def title="De afkorting OSPF staat voor?">
    Open Shortest Path First
</def>
<def title="Waar wordt OSPF voor gebruikt?">
    Om de meest efficiënte routes voor packets te vinden binnen een IP-netwerk.
</def>
<def title="OSPF is een ... routing protocol.">
    Link-state
</def>
<def title="OSPF maakt gebruik van ... om routing update netwerkverkeer te beperken.">
    Areas
</def>
<def title="Wat is het verschil tussen multiaccess en point-to-point OSPF?">
    <p>Multiaccess: Meerdere routers zijn verbonden met elkaar met bijvoorbeeld een switch er tussen. DR en BDR worden gekozen.</p>
    <p>Point-to-point: Twee routers zijn direct met elkaar verbonden zonder andere routers op hetzelfde segment. Geen DR of BDR nodig.</p>
</def>
<def title="Wat zijn de 5 soorten OSPF packets?">
    <p>1. Hello packet</p>
    <p>2. Database Description (DBD) packet</p>
    <p>3. Link State Request (LSR) packet</p>
    <p>4. Link State Update (LSU) packet</p>
    <p>5. Link State Acknowledgment (LSAck) packet</p>
</def>
<def title="Wat zijn de 3 OSPF data structures?">
    <p>Adjacency database: neighbor table</p>
    <p>Link-state database (LSDB): topology table</p>
    <p>Forwarding database: routing table</p>
</def>
<def title="Welk algoritme gebruikt OSPF?">
    Dijkstra's Shortest Path First (SPF) algoritme.
</def>
<def title="Wat staat er in de adjacency database?">
    Informatie over direct verbonden OSPF-routers.
</def>
<def title="Wat staat er in de link-state database?">
    <p>Informatie over al de andere routers in het netwerk.</p>
    <p>Het representeert de netwerktopologie.</p>
</def>
<def title="Wat staat er in de forwarding database?">
    De beste routes naar alle bekende routers.
</def>
<def title="Wat doet een Hello packet?">
    <p>Wordt gebruikt om OSPF-neighbors te ontdekken en de connectie te onderhouden.</p>
    <p>DR en BDR verkiezen.</p>
</def>
<def title="Wat doet een DBD packet?">
    Het bevat een korte versie van de LSDB en wordt gebruikt om de LSDB tussen routers te synchroniseren.
</def>
<def title="Wat doet een LSR packet?">
    Wordt gebruikt door een router om specifieke link-state informatie op te vragen van een andere router.
</def>
<def title="Wat doet een LSU packet?">
    Wordt gebruikt als antwoord op een LSR packet en om link-state informatie te verzenden naar andere OSPF-routers.
</def>
<def title="Wat doet een LSAck packet?">
    Wordt gebruikt om de ontvangst van een LSU packet te bevestigen.
</def>
<def title="Welke database is hetzelfde op alle routers?">
    De link-state database (LSDB).
</def>
<def title="Wat zijn de 5 stappen van OSPF link-state operation?">
    <p>1. Establish neighbor adjacency: OSPF routers sturen Hello packets om neighbors te vinden.</p>
    <p>2. Exchange Link-State Advertisements: Routers delen LSA's die de status en kost van elke direct verbonden link bevatten.</p>
    <p>3. Build Link-State Database: Elke router bouwt een LSDB op basis van ontvangen LSA's.</p>
    <p>4. Run Shortest Path First (SPF) Algorithm: Elke router gebruikt Dijkstra's algoritme om de beste routes te bepalen.</p>
    <p>5. Update Routing Table: De beste routes worden toegevoegd aan de routing table.</p>
</def>
<def title="Wat is het verschil tussen single-area en multiarea OSPF?">
    <p>Single-area OSPF: Alle routers bevinden zich in dezelfde OSPF-area (area 0). Eenvoudiger te beheren, maar minder schaalbaar.</p>
    <p>Multiarea OSPF: Het netwerk is verdeeld in meerdere areas, met area 0 als backbone. Beter schaalbaar en efficiënter voor grote netwerken.</p>
</def>
<def title="Wat zit er in een LSU packet?">
    <p>Link-State Advertisements (LSA's).</p>
</def>
<def title="Wat zijn de 7 OSPF Operational states?">
    <p>1. Down state: Geen Hello packets ontvangen, maar verstuurt er wel.</p>
    <p>2. Init state: Hello packet ontvangen die de router ID van de neighbor bevatten.</p>
    <p>3. Two-way state: Hello packets zijn uitgewisseld en de bidirectionele communicatie is bevestigd. DR en BDR worden gekozen.</p>
    <p>4. ExStart state: In point-to-point netwerken bepalen de twee routers wie begint met het uitwisselen van DBD packets.</p>
    <p>5. Exchange state: Routers wisselen DBD packets uit.</p>
    <p>6. Loading state: Als meer router informatie nodig is worden er LSR's en LSU's gestuurd. Als dat niet zo is, wordt deze overgeslagen.</p>
    <p>7. Full state: De routers zijn volledig gesynchroniseerd en kunnen routes berekenen.</p>
</def>
<def title="Wat zijn de gereserveerde multicast IP-adressen voor OSPF?">
    <p>Alle OSPF routers: <code>224.0.0.5</code></p>
    <p>Alle DR's: <code>224.0.0.6</code></p>
</def>
<def title="Wat is het nut van de BDR?">
    Als de DR uitvalt, neemt de BDR de plaats in van de DR.
</def>
<def title="Wat is OSPFv3?">
    OSPF versie 3, ontworpen voor IPv6 netwerken.
</def>
<def title="Wat is een router ID?">
    Een uniek 32-bit ID dat een OSPF-router identificeert binnen een OSPF-netwerk.
</def>
<def title="Hoe wordt het router ID gekozen?">
    <p>1. Handmatig configureren.</p>
    <p>2. Hoogste IPv4-adres van een actieve loopback interface.</p>
    <p>3. Hoogste IPv4-adres van een actieve fysieke interface.</p>
</def>
<def title="Hoe worden de DR en BDR gekozen?">
    <p>1. Router met de hoogste OSPF-prioriteit.</p>
    <p>2. Bij gelijke prioriteit, router met het hoogste router ID.</p>
</def>
<def title="Wat is de standaard OSPF-prioriteit?">
    1
</def>
<def title="Wat is de standaard OSPF-timer interval voor Hello packets?">
    10 seconden.
</def>
<def title="Wat is de standaard OSPF dead interval?">
    40 seconden.
</def>
<def title="Hoe vaak worden LSU packets naar neighbors gestuurd wanneer het OSPF-netwerk volledig is?">
    Elke 30 minuten.
</def>
</deflist>

## ACL

<deflist collapsible="true">
<def title="Wat is een Access Control List (ACL)?">
    Een set regels die bepaalt welk netwerkverkeer is toegestaan.
</def>
<def title="Wat is het verschil tussen standard en extended ACL's?">
    <p>Standaard ACL's filteren verkeer op basis van bron IP-adres.</p>
    <p>Uitgebreide ACL's kunnen filteren op basis van bron- en bestemmings-IP-adressen, protocollen en poorten.</p>
</def>
<def title="Op welke lagen van het OSI-model werken standard en extended ACL's?">
    <p>Standaard ACL's werken op laag 3 (netwerklaag).</p>
    <p>Uitgebreide ACL's werken op laag 3 (netwerklaag) en laag 4 (transportlaag).</p>
</def>
<def title="Wat is het verschil tussen inbound en outbound ACL's?">
    <p>Inbound ACL's worden toegepast op verkeer dat een interface binnenkomt.</p>
    <p>Outbound ACL's worden toegepast op verkeer dat een interface verlaat.</p>
</def>
<def title="Wat staat standaard en verborgen in een ACL?">
    Aan het einde van elke ACL staat standaard een verborgen 'deny all' regel die al het overige verkeer blokkeert.
</def>
<def title="Wat is het nut van een wildcard mask in een ACL?">
    Het specificeert welk deel van het IP-adres moet worden gecheckt bij het toepassen van de ACL-regel.
</def>
<def title="Wat doen 'host' en 'any' in een ACL?">
    <p>'host': Is hetzelfde als het wildcard mask <code>0.0.0.0</code>.</p>
    <p>'any': Is hetzelfde als <code>0.0.0.0 255.255.255.255</code>.</p>
</def>
<def title="Wat is het verschil tussen een standard en een extended ACL in termen van nummering?">
    <p>Standard ACL's gebruiken nummers van 1-99 en 1300-1999.</p>
    <p>Extended ACL's gebruiken nummers van 100-199 en 2000-2699.</p>
</def>
<def title="Waar worden standard ACL's meestal toegepast?">
    Zo dicht mogelijk bij de bestemming.
</def>
<def title="Waar worden extended ACL's meestal toegepast?">
    Zo dicht mogelijk bij de bron.
</def>
</deflist>

## NAT

<deflist collapsible="true">
<def title="Wat is Network Address Translation (NAT)?">
    Een techniek die meerdere privé-IP-adressen een enkel openbaar IP-adres laat delen.
</def>
<def title="Welke 4 soorten adressen bestaan er binnen NAT?">
    <p>Inside local address</p>
    <p>Inside global address</p>
    <p>Outside local address</p>
    <p>Outside global address</p>
</def>
<def title="Welk soort adres is het adres dat door de buitenkant als het bron adres wordt gezien?">
    Inside global address
</def>
<def title="Welk soort adres is het adres dat door de binnenkant als het bron adres wordt gezien?">
    Inside local address
</def>
<def title="Welke soorten NAT bestaan er?">
    <p>Static NAT</p>
    <p>Dynamic NAT</p>
    <p>PAT (NAT overload)</p>
</def>
<def title="Welk soort adres is het adres dat door de binnenkant als het bestemmingsadres wordt gezien?">
    Outside global address
</def>
<def title="Wat is Static NAT?">
    Static NAT maakt een permanente link tussen een privé-IP-adres en een openbaar IP-adres.
</def>
<def title="Wat is Dynamic NAT?">
    Dynamic NAT maakt gebruik van een pool van openbare IP-adressen die dynamisch worden toegewezen aan privé-IP-adressen.
</def>
<def title="Wat is PAT (NAT overload)?">
    PAT maakt gebruik van één of meer openbare IP-adressen en verschillende poortnummers om meerdere privé-IP-adressen te vertalen.
</def>
<def title="Wat gebeurt er als PAT geen beschikbare poorten meer heeft?">
    Het probeert het volgende beschikbare openbare IP-adres in de pool te gebruiken, als er geen zijn, werkt PAT niet.
</def>
<def title="Wat gebruikt PAT als een packet geen layer 4 poort nummer heeft, specifiek voor een ICMPv4 echo request?">
    PAT gebruikt het Query ID-veld om een echo request te identificeren met de bijbehorende echo reply.
</def>
</deflist>

## WAN concepts

<deflist collapsible="true">
<def title="Wat is het verschil tussen een Single-carrier en Dual-carrier WAN verbinding?">
    <p>Single-carrier: Eén enkele provider levert de WAN-dienst.</p>
    <p>Dual-carrier: Twee verschillende providers leveren de WAN-dienst, wat zorgt voor redundantie en betrouwbaarheid.</p>
</def>
<def title="Wat betekent de term POP?">
    POP staat voor Point of Presence. Het is het fysieke punt waar een WAN-provider verbinding maakt met het netwerk van de klant.
</def>
<def title="Wat is een demarcation point?">
    Het is het fysieke punt waar de verantwoordelijkheid van de WAN-provider eindigt en de verantwoordelijkheid van de klant begint.
</def>
<def title="Wat is DTE?">
    Data Terminal Equipment, het apparaat (meestal een router) dat de LAN van de klant verbindt met het WAN.
</def>
<def title="Wat is DCE?">
    Data Communications Equipment, het apparaat (meestal een modem) dat de data verstuurt en ontvangt over het WAN.
</def>
<def title="Wat is CPE?">
    Customer Premises Equipment, de DTE en DCE-apparaten die zich bevinden op het terrein van de klant.
</def>
<def title="Wat is een local loop / last mile?">
    De fysieke kabel die de CPE verbindt met de WAN-provider's netwerk.
</def>
<def title="Wat is een DSL-modem en een Cable modem?">
    <p>Dit zijn DCE-apparaten.</p>
    <p>DSL-modem: Gebruikt telefoonlijnen voor dataoverdracht.</p>
    <p>Cable modem: Gebruikt coaxiale kabels voor dataoverdracht.</p>
</def>
<def title="Wat is een CSU/DSU?">
    <p>Channel Service Unit/Data Service Unit, een DCE-apparaat of interface op een DCE-apparaat.</p>
    <p>CSU: Zorgt voor verbinding integriteit via error correction en line monitoring.</p>
    <p>DSU: Zet digitale signalen van de DTE om naar signalen die geschikt zijn voor de WAN-verbinding en vice versa.</p>
</def>
<def title="Waarom wordt parallel communicatie niet gebruikt in een WAN?">
    Omdat het voor lange afstanden slecht werkt vanwege synchronisatieproblemen.
</def>
<def title="Wat is MPLS?">
    Multiprotocol Label Switching, een technologie die data in een WAN kan versturen zonder dat er rekening hoeft te worden gehouden met het onderliggende protocol of payload.
</def>
<def title="Wat is een CE, PE en P router?">
    <p>CE: Customer Edge router</p>
    <p>PE: Provider Edge router</p>
    <p>P: Provider router</p>
</def>
<def title="MPLS routers zijn LSR's. Wat betekent LSR?">
    Label Switched Router
</def>
</deflist>

