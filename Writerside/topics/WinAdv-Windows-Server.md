# Windows Server

## Domein

**Een computer kan lid zijn van een workgroup of een domain.**

- **Workgroup:**
    - Niet centraal beheerd.
    - Bestaat uit gelijke clients (computers).
    - Policies moeten per toestel apart geconfigureerd worden.
- **Domain:**
    - Centraal beheerd
    - Bestaat uit één of meerdere servers die clients beheren.
        - Domain controllers
        - Extra controllers heten: ADC (Additional Domain Controller)
    - Policies kunnen voor meerdere of enkele toestellen geconfigureerd worden.

## Server core & Nano server

**Server Core:**\
Minimale Windows installatie zonder GUI.\
Zorgt voor betere beveiliging en prestaties.

**Nano server:**\
Nog lichter dan Server Core. Is geoptimaliseerd voor cloudomgevingen en containers.\
Ontworpen voor gebruik in specifieke scenario's. Je kan niet lokaal inloggen, wel op afstand.

## Azure & AWS

### Azure

**Hybride mogelijkheden**
- Azure biedt de mogelijkheid om **on-premise en cloud te mixen**

**Kosten besparing**
- Via Azure Hybrid Benefit kunnen klanten **bestaande licenties gebruiken**

**Beveiliging**
- Azure biedt **geavanceerde beveiligingsfuncties** om gevoelige workloads te beschermen.

### AWS

**Brede ondersteuning**
- AWS **ondersteunt** een **breed scala** aan Windows Server-versies en -toepassingen

**Licentiebeheer**
- Met AWS License Manager kunnen organisaties hun **softwarelicenties gemakkelijk beheren**.

**Prestatie**
- AWS biedt een **scalable** infrastructuur die is **geoptimaliseerd** voor het uitvoeren van veeleisende Windows-workloads.

## Windows server versies

### Windows Server 2022

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

### Windows Server 2025

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

## CAL's

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
