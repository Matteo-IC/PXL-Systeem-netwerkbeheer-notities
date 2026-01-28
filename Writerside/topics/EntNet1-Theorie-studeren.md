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
    <p>Alle routers hebben dezelfde LSDB.</p>
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

