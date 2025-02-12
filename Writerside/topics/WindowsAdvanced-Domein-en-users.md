# Domein en users

<table>
    <tr>
        <td>Term</td>
        <td>Uitleg</td>
    </tr>
    <tr>
        <td>vSwitch</td>
        <td>
        Virtual Switch, zoals een fysieke switch maar via software. Beheert netwerk verkeer tussen VMs, dit kan alleen
        op dezelfde host zijn of op andere manieren afhankelijk van de adapter settings.        
        </td>
    </tr>
    <tr>
        <td>Netwerkadapter / NIC</td>
        <td>Hardware in een computer dat de computer verbindt met het netwerk.</td>
    </tr>
    <tr>
        <td>NIC setting: Host-only</td>
        <td>Netwerk verkeer kan enkel tussen de host en VMs, niet met externe netwerken.</td>
    </tr>
    <tr>
        <td>NIC setting: Bridged</td>
        <td>
        Verbind VMs met het fysieke netwerk via de netwerkadapter van de host. De VM wordt als een aparte machine gezien
        op het netwerk en krijgt een eigen IP.
        </td>
    </tr>
    <tr>
        <td>NIC setting: NAT</td>
        <td>
        Maakt een privénetwerk tussen de host en VM, de VM deelt het IP van de host. VMs kunnen verbinden met externe
        systemen maar externe systemen verbinden met de host.
        </td>
    </tr>
    <tr>
        <td>NIC setting: LAN Segment</td>
        <td>Verbind specifieke VMs met elkaar, kan tussen meerdere hosts.</td>
    </tr>
    <tr>
        <td>Promote</td>
        <td>Van een server een domein controller maken.</td>
    </tr>
    <tr>
        <td>AD DS</td>
        <td>Active Directory Domain Services</td>
    </tr>
    <tr>
        <td>OU</td>
        <td>
        Organizational Unit, container object dat in AD gebruikt wordt om gebruikers, computers, groepen... 
        te structureren in een folder structuur.
        </td>
    </tr>
    <tr>
        <td>Functional level</td>
        <td>
        Het level van de slechtste domein controller. Als een nieuw domein controller toegevoegd wordt moet deze op dat
        level zijn.
        </td>
    </tr>
</table>