# Module 5

## Layer 2 loops

Een **layer 2 loop** is een **netwerk probleem** waarbij **frames** **oneindig** worden **doorgestuurd**.

Dit gebeurt wanneer **switches** met **redundante paden** bijvoorbeeld een **broadcast frame ontvangen** 
en deze **doorsturen naar** alle **andere poorten**.

Maar als het **broadcast frame** dan terugkomt bij een **switch** die het **broadcast frame al** heeft **ontvangen**,
komt het **frame** van een **andere poort** en wordt het **frame weer doorgestuurd door alle egress poorten**.\
Zo gaat het **frame** **oneindig** door en **vermenigvuldigt het zichzelf** in het **netwerk** tot deze **plat ligt**.

## STP

Het **Spanning Tree Protocol (STP)** is een **netwerk protocol** dat **layer 2 loops** **voorkomt**.

**STP** doet dit door bepaalde **poorten** **uit te schakelen**.

Doordat **STP poorten uitschakelt, voorkomt** het dat **frames gestuurd** worden naar **switches** die het
**frame al hebben ontvangen**.

## Hoe werkt STP?

In de volgende topologie zijn er **verschillende** mogelijkheden voor **layer 2 loops**.

Bijvoorbeeld als **Switch A** een **broadcast frame** stuurt naar **Switch B** en **Switch D**.\
**Switch B** stuurt het **frame** door naar **Switch C** en **Switch D**.\
**Switch D** stuurt het eerste frame van **Switch A** door naar **Switch C** en **Switch B**.\
**Switch D** stuurt het tweede frame van **Switch B** door naar **Switch C** en **Switch A**...\
Dat is het begin van een **broadcast storm**.

```
Topologie:
      ┌─────────┐
      │Switch A │──────╮
      └────┬────┘      │
           │           │
      ┌────┴────┐      │
      │Switch B │      │
     ╭└─────────┘╮     │
     │           │     │
     │           │     │
     │           │     │
 ┌───┴───┐   ┌───┴───┐ │
 │Switch │   │Switch │ │
 │   C   │───│   D   │─╯
 └───────┘   └───────┘
```

### Spanning Tree Algorithm

Het **algoritme** dat **STP** gebruikt om **layer 2 loops** te **voorkomen**.

<tip>
<p>Dit <control>algoritme</control> maakt gebruik van <control>BPDUs</control> (Bridge Protocol Data Units).</p>
<p>Dit zijn <control>frames</control> die <control>informatie</control> over <control>een switch</control> naar een
<control>andere switch sturen</control>.</p>
In zo een <control>BPDU</control> zit een <control>Bridge ID (BID)</control>.
<p>De <control>BID</control> bestaat uit 3 delen:</p>
<list>
<li>
    <control>Bridge Priority</control>: Een <control>cijfer</control> dat de <control>prioriteit</control> van de 
    <control>switch</control> aangeeft. Hoe <control>lager</control>, hoe <control>belangrijker</control>.
</li>
<li>
    <control>Extended System ID</control>: Dit is het <control>VLAN ID</control> van de <control>BPDU</control>.
</li>
<li>
    <control>MAC Address</control>: Het <control>MAC adres</control> van de <control>switch</control>.
    Als meerdere switches dezelfde <control>Bridge Priority</control> hebben, wordt het laagste <control>MAC adres</control> 
    gebruikt om de <control>root bridge</control> te bepalen.
</li>
</list>
</tip>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

<tabs>
<tab title="1. Root Bridge">
    <p>De <control>eerste stap</control> is het <control>selecteren</control> van de <control>root bridge</control> (root switch).</p>
    <p>Dit wordt gedaan om een <control>referentie punt</control> te hebben. <control>Zonder referentie punt</control>
    kunnen er <control>geen paden</control> berekend worden omdat de switches niet weten waar ze naartoe moeten.</p>
    <p>De <control>root bridge is</control> de <control>switch</control> met het <control>laagste Bridge ID</control>.
    Dit <control>kan worden ingesteld door een netwerkbeheerder</control>, om inefficiënte netwerken te vermijden moet 
    je het netwerk dus goed ontwerpen.</p>
    <code-block>
⠀
      ┌─────────┐
      │Switch A │──────╮ ← ROOT BRIDGE
      │ID: 100  │      │   (Laagste Bridge ID)
      └────┬────┘      │
           │           │
      ┌────┴────┐      │
      │Switch B │      │
      │ID: 200  │      │
     ╭└─────────┘╮     │
     │           │     │
 ┌───┴───┐   ┌───┴───┐ │
 │Switch │   │Switch │ │
 │   C   │───│   D   │─╯
 │ID: 300│   │ID: 400│
 └───────┘   └───────┘
    </code-block>
</tab>
<tab title="2. Root Poort">
    <p>Als de <control>root bridge gevonden</control> is moet elke switch (niet de root bridge / switch) een 
    <control>root poort selecteren</control>.</p>
    <p>De <control>root poort is</control> de poort die het <control>dichtste</control> (qua performantie, niet fysiek) 
    <control>bij de root bridge</control> is.</p>
    <p>De <control>root path cost</control> (de "prijs" om aan de root bridge te geraken) wordt 
    <control>berekend door de snelheid</control> van een link een cijfer te geven. <control>Hoe sneller, hoe kleiner</control>
    het cijfer / <control>de kost</control>.</p>
    <p>Als er <control>meerdere links</control> zijn tussen de root poort en de root bridge, wordt de 
    <control>root path cost</control> van elke link op een pad <control>opgeteld</control> en het pad met het 
    <control>laagste cijfer wordt verkozen</control>.</p>
    <code-block>
RP = Root Poort
      ┌─────────┐
      │Switch A │──────╮ ← ROOT BRIDGE
      └────┬────┘      │
           │ - 4       │
 RP - ┌────┴────┐      │
      │Switch B │      │
     ╭└─────────┘╮     │ - 4
     │           │     │
 4 - │       4 - │     │
RP - │           │     │
 ┌───┴───┐   ┌───┴───┐ │
 │Switch │   │Switch │ │
 │   C   │───│   D   │─╯ - RP
 └───────┘ │ └───────┘
           4
    </code-block>
<note>
    <control>Waarom is de root poort van Switch C niet naar Switch D?</control>
    <p>De root path cost van Switch C is voor beide poorten 8. Er moet dus gekozen worden tussen de twee.</p>
    <p>Switch C kijkt naar welke switch het laagste Bridge ID heeft en kiest dus Switch B.</p>
</note>
</tab>
<tab title="3. Designated Poort">
    <p>De <control>designated poort</control> is de <control>poort op een switch</control> (root & niet root) die een 
    <control>netwerk segment verbindt met</control> het <control>beste pad naar de root bridge</control>.</p>
    <p><emphasis>Een netwerk segment is een deel van een netwerk. Bijvoorbeeld een apparaat en kabel zijn één netwerk segment als
    die verbonden zijn met een netwerk.</emphasis></p>
    <code-block>
DP = Designated Poort
      ┌─────────┐
      │Switch A │──────╮ - DP
 DP - └────┬────┘      │
           │           │
      ┌────┴────┐      │
      │Switch B │      │
DP - ╭└─────────┘╮     │
     │           │     │
     │           │     │
     │           │     │
 ┌───┴───┐   ┌───┴───┐ │
 │Switch │   │Switch │ │
 │   C   │───│   D   │─╯
 └───────┘   └───────┘
             │
             DP
    </code-block>
</tab>
<tab title="4. Geblokkeerde Poorten">
    <p>Als een poort <control>geen designated of root poort</control> is, 
    <control>wordt</control> deze <control>geblokkeerd</control>.</p>
    <code-block>
⠀
      ┌─────────┐
      │Switch A │──────╮
      └────┬────┘      │
           │           │
      ┌────┴────┐      │
      │Switch B │      │
     ╭└─────────┘x     │
     │           │     │
     │           │     │
     │           x     │
 ┌───┴───┐   ┌───┴───┐ │
 │Switch │   │Switch │ │
 │   C   │x──│   D   │─╯
 └───────┘   └───────┘
    </code-block>
    <tip>
    Omdat Switch A de root bridge is, heeft Switch D geen optimaal pad naar B of C. Het had dus beter geweest om Switch B
    de root bridge te maken. Een netwerk goed uitdenken is dus belangrijk.
    </tip>
</tab>
</tabs>

### Poort statussen

<table>
    <tr>
        <td>Poort status</td>
        <td>Beschrijving</td>
    </tr>
    <tr>
        <td>Disabled</td>
        <td>De poort is <control>administratief uitgezet</control>. Het stuurt geen frames door en doet niet mee aan STP.</td>
    </tr>
    <tr>
        <td>Blocking</td>
        <td>De poort is <control>geblokkeerd door STP</control>. Het stuurt geen frames door, maar 
        <control>luistert wel naar BPDUs</control>. Als de poort na <control>20 seconden geen BPDU</control> heeft 
        ontvangen (Max Age timer) gaat die naar de <control>"listening" status</control>.</td>
    </tr>
    <tr>
        <td>Listening</td>
        <td>De poort <control>luistert naar BPDU frames</control> om te <control>beslissen</control> wat het 
        <control>beste pad</control> is <control>naar de root bridge</control>. Het stuurt ook zijn eigen BPDUs.</td>
    </tr>
    <tr>
        <td>Learning</td>
        <td>De poort <control>ontvangt en verwerkt BPDUs</control>. Het bereidt zich ook voor om frames door te sturen. 
        Daarnaast begint het met de MAC adres tabel in te vullen.</td>
    </tr>
    <tr>
        <td>Forwarding</td>
        <td>De poort <control>stuurt frames door</control> en <control>luistert naar BPDUs</control>. 
        Het is de <control>actieve status</control>.</td>
    </tr>
</table>

### PVST

**Per VLAN Spanning Tree (PVST)** is een **uitgebreide versie van STP** die **per VLAN** een **eigen spanning tree** heeft.\
Dit betekent dat **elke VLAN** zijn eigen **root bridge**, **root poorten** en **designated poorten** heeft.