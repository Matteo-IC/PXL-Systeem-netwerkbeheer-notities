# Active Directory

## Active Directory (AD) en LDAP

De **gebruikersnaam, wachtwoord** en andere instellingen worden **opgeslagen in een database genaamd NTDS**.\
Dit is deel van AD.

**Active Directory is het geheel** dat Microsoft gebruikt **om alle informatie**, instellingen, beperkingen en configuraties
binnen een domein **op te slaan op 1 locatie**.

**LDAP (Lightweight Directory Access Protocol):**\
Het **protocol dat de verbinding vormt** om **gegevens uit AD databases te halen**,
en de **gegevens leest vanuit de database**.

*LDAP vind je ook terug op andere toepassingen:*\
*Een NAS-storage die LDAP ondersteunt, kan gegevens uitlezen uit een AD database, en kan dus ervoor zorgen dat je met je
account automatisch toegang hebt tot de bestanden waar je de rechten voor hebt.*\
*Een WIFI-accesspoint met LDAP kan met standaard Windows gebruikers het wachtwoord uitlezen uit een AD database om te
zien of het wachtwoord hetzelfde is als bij de Windows server en je toegang verlenen tot het netwerk.*\
\
\
**AD databases bevatten alle gegevens van het domein. We noemen deze gegevens objecten**.
- Usernames, wachtwoorden, policies, computernamen...

### In een zin

**AD databases bevinden zich op** één of meer servers genaamd de **Domain Controller** (DC). Elke **extra DC** krijgt de
**naam ADC** (Additional Domain Controller), deze synchroniseren met elkaar zodat ze identiek zijn.\
**De DC kan werk met andere delen, dit heet load balancing.**\
De **DC kan users authenticeren**, scripts doorsturen, policies aansturen, en security instellingen uitvoeren **via LDAP**.

## Domein creatie

### Tree

Een **domain** bestaat uit een **AD Database die identiek & gesynchroniseerd is tussen alle servers**.\
**Gebruikers kunnen dus op elke server / domain controller inloggen.** Zo wordt de load verdeelt.\
\
\
De **AD Database kan snel groeien**. Hoe groter, hoe trager. Je scheid ook best accounts op in verschillende groepen.

Om te **voorkomen dat de AD Database te groot en te moeilijk te beheren wordt** kan je deze
**opsplitsen in kleinere databases**.\
Een nieuwe kleinere database is een **child database**. Deze wordt **gemaakt via een child domain**.

**Child domain:** Een **afgesplitst domein van het originele domein**. Als naam wordt er een **prefix toegevoegd** aan
de naam van het parent domain. Dit domain heeft een **aparte AD en AD Database**.

Standaard hebben de parent en het child domain een "**two way trust**", dit betekent dat de **login gegevens van een
account** in één AD Database ook **werken bij een parent of child AD Database**.\
\
\
De **verzameling van** alle **parent en child domains** is een **tree**.

### Forest

Als **2 aparte domeinen** / trees **gekoppeld** worden, noemt men dat een **forest**.\
Je **zet** een **forest op** door een **trust verbinding** op te zetten tussen **beide domeinen**.

*Het kan ingesteld worden dat users van 1 domein kunnen inloggen op het andere, maar niet omgekeerd.*\
*Het kan ook dat alle users bij elk domein kunnen inloggen.*

### Rollen - Features

Een **rol is een functie die aan een server wordt gegeven**.

Bijvoorbeeld:
- Domain controller
- File server
- DNS server
- Web server

Elke **rol moet eerst geïnstalleerd** worden en kan **daarna geconfigureerd** worden vie Server Manager.

**Feature:** Een uitbreiding die door rollen kan gebruikt worden of als stand alone.

Bijvoorbeeld:
- Bitlocker
- .Net framework
- Backup

## AGDLP

AGDLP staat voor Accounts, Global groups, Domain Local groups, Permissions.

Voorbeeld stappen volgens AGDLP:
1. **Accounts** maken
2. **Global groups** 1_GL & 2_GL maken
3. Deze toevoegen aan de nieuwe **Domain Local groups** 1_DL & 2_DL
4. Domain Local group 1_2_DL maken
    - Om alle gebruikers in beide groepen te beheren via 1 groep
5. Groepen **rechten** geven

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Users moeten aangemaakt worden via het "Active Directory Users & Computers" tool.

**User group:** Verzameling van users die dezelfde instellingen en beveiliging hebben.

2 soorten van groepen:
- **Security group**
    - Voor groepen **gebruikers toegang** te **geven tot resources**: websites, folders...
    - Onderverdeeld in:
        - **Global groups**: Groepen die in het heel forest zichtbaar zijn (dus zichtbaar voor andere domeinen)
        - **Domain local groups**: Groepen die enkel zichtbaar zijn voor het eigen domein
- **Distribution group**
    - Hoofdzakelijk voor **gebruikers** in **mailing groepen** te **verzamelen**

## Organizational units

Een **organizational unit (OU)** is een map waarin je **objecten** zoals
**computers, gebruikers en groepen** kan plaatsen.

Op die OU kunnen **beperkingen en instellingen worden toegepast**. Die beperkingen en instellingen **heten policies**.

## Termen

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