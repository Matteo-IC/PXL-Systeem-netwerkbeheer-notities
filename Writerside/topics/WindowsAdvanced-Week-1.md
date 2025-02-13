# Week 1

## Windows Server

### Domein

**Een computer kan lid van een workgroup of een domain.**

- **Workgroup:**
  - Niet centraal managed.
  - Bestaat uit gelijke clients (computers).
  - Policies moeten per toestel apart geconfigureerd worden.
- **Domain:**
  - Centraal managed
  - Bestaat uit één of meerdere servers die clients beheren.
    - Domain controllers
    - Extra controllers heten: ADC (Additional Domain Controller)
  - Policies kunnen voor meerdere of enkele toestellen geconfigureerd worden.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Server core & Nano server

**Server Core:**\
Minimale Windows installatie zonder GUI.\
Zorgt voor betere beveiliging en prestaties.

**Nano server:**\
Nog lichter dan Server Core die geoptimaliseerd is voor cloudomgevingen en containers.\
Ontworpen voor specifieke scenario's. Je kan niet lokaal inloggen, wel op afstand.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Azure & AWS

#### Azure

**Hybride mogelijkheden**
- Azure biedt de mogelijkheid om on-premise en cloud te mixen

**Kosten besparing**
- Via Azure Hybrid Benefit kunnen klanten bestaande licenties gebruiken 

**Beveiliging**
- Azure biedt geavanceerde beveiligingsfuncties om gevoelige workloads te beschermen.

#### AWS

**Brede ondersteuning**
- AWS ondersteunt een breed scala aan Windows Server-versies en -toepassingen

**Licentiebeheer**
- Met AWS License Manager kunnen organisaties hun softwarelicenties gemakkelijk beheren.

**Prestatie**
- AWS biedt een scalable infrastructuur die is geoptimaliseerd voor het uitvoeren van veeleisende Windows-workloads.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Windows server versies

#### Windows Server 2022

**Standard Edition:**
- Doelgroep
  - Kleine tot middelgrote bedrijven met beperkte virtualisatie noden
- Virtualisatie
  - Maximaal 2 VM's & 1 Hyper-V host
- Kenmerken
  - Basisfunctionaliteiten voor bestand en printservices
  - Ondersteund Windows Containers
  - Beperkte opslag-replica mogelijkheden

**Datacenter Edition:**
- Doelgroep
  - Grote ondernemingen met uitgebreide virtualisatie behoeften
- Virtualisatie
  - Onbeperkt aantal VM's & Hyper-V containers
- Kenmerken
  - Alles van Standard Edition
  - Geavanceerde functies zoals Storage Spaces Direct en Software-Defined Networking
  - Onbeperkte opslag-replica mogelijkheden

**Datacenter: Azure Edition:**
- Doelgroep
  - Organisaties die hybride on-premise datacenters en Microsoft Azure willen
- Kenmerken
  - Alles van Datacenter Edition
  - Specifieke Azure-integratiefuncties

#### Windows Server 2025

**Essentials Edition:**
- Doelgroep
  - Kleine bedrijven
- Kenmerken
  - Maximaal 25 gebruikers en 50 apparaten
  - Geen vereiste voor Client Access Licenses (CALs)
  - Beperkte functionaliteiten zonder ondersteuning voor virtualisatie of geavanceerde serverapplicaties

**Standard Edition:**
- Doelgroep
  - Middelgrote bedrijven met matige virtualisatie noden
- Virtualisatie
  - Maximaal twee virtuele machines en één Hyper-V-host
- Kenmerken
  - Basisfunctionaliteiten voor bestands- en printservices
  - Ondersteuning voor Windows Containers
  - Beperkte opslagreplica-mogelijkheden

**Datacenter Edition:**
- Doelgroep
  - Grote ondernemingen met uitgebreide virtualisatie noden
- Virtualisatie
  - Onbeperkt aantal VM's & Hyper-V containers
- Kenmerken
  - Alles van Standard Edition
  - Geavanceerde functies zoals Storage Spaces Direct en Software-Defined Networking
  - Onbeperkte opslag-replica mogelijkheden
  - Ondersteuning voor gecodeerde virtuele machines

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### CAL's

Een **Client Access License** (CAL) is een licentie die **vereist is voor gebruikers of apparaten** om **toegang te krijgen tot
een Windows Server**.

CAL's zijn **geen software**, maar **rechten** die **bepalen hoeveel gebruikers of apparaten legaal verbinding mogen maken**
met de server.

**Soorten:**
- **User CAL**
  - Gebonden aan specifieke gebruiker
  - Maakt niet uit welk apparaat, wel wat account
- **Device CAL**
  - Gebonden aan specifiek apparaat
  - Maakt niet uit welk account, wel wat apparaat
- **Remote Desktop Services (RDS) CAL**
  - Vereist als gebruikers of apparaten gebruik maken van Remote Desktop Services (RDS)
  - Bovenop de standaard User of Device CAL nodig
  - External Connector License
  - Voor externe gebruikers die toegang tot de server nodig hebben

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Active Directory (AD) en LDAP

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

#### In een zin

**AD databases bevinden zich op** één of meer servers genaamd de **Domain Controller** (DC). Elke extra DC krijgt de naam
ADC (Additional Domain Controller), deze synchroniseren met elkaar zodat ze identiek zijn.\
**De DC kan werk met andere delen, dit heet load balancing.**\
De **DC kan users authenticeren**, scripts doorsturen, policies aansturen, en security instellingen uitvoeren **via LDAP**.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Basisservices

#### DHCP

Een DHCP service deelt ip configuraties uit aan toestellen.

#### DNS

DNS is een service die Fully Qualified Domain Names (fqdn) omzet naar ip adressen.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Domein creatie

#### Tree

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

#### Forest

