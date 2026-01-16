# Introductie

- Describe the cybersecurity concepts in this presentation in their own words.
- <a href="#het-is-dus-belangrijk-dat-je-wachtwoord" summary="Complex, uniek, geen persoonlijke info, veranderd wanneer gelekt.">List the criteria of a strong password and apply them in practice.</a>
- Propose a valid countermeasure for a given vulnerability.
- <a href="#wachtwoord-complexiteit" summary="Complexiteit ^ lengte.">Calculate the maximum number of password combinations given specific password requirements.</a>
- <a href="#cybersecurity-modellen" summary="CIA triad, states of data, beveiligingsmaatregelen.">Identify and provide an example for each dimension of the cybersecurity cube.</a>
- Apply multifactor authentication to an account.
- <a href="#cia-triad" summary="Authenticatie: Log in op website, Autorisatie: Blokkeren toegang tot bestand, Accounting: Firewall log.">Give an example of AAA services.</a>
- <a href="#defense-in-depth-castle-approach">Explain the Defense in Depth / Castle Approach in their own words.</a>
- <a href="#defense-in-depth-castle-approach" summary="">Provide an example for each layer of Defense in Depth.</a>
- Configure a passkey on a supported account.
- Use cvedetails.com to determine if there are known vulnerabilities in a specific software version.
- Sort vulnerabilities on cvedetails.com for a given software by EPSS.
- Sort vulnerabilities on cvedetails.com for a given software by CVSS.
- Retrieve a product dashboard for a given software on cvedetails.com, including type and categories of vulnerabilities.

## Wat is cybersecurity?

Cybersecurity is het **beveiligen van computer systemen**, netwerken en data van ongeautoriseerde toegang, aanvallen of schade door technische en organisatorische maatregelen.

Cybersecurity is een **oneindige "arms race"**, dat betekent dat er **constant nieuwe aanvallen** zijn en **constant nieuwe verdedigingen** om die aanvallen te stoppen.

## Termen

### Soorten hacking

**Hacking:** Het proces van **zwakheden te misbruiken in computer systemen**, netwerken of applicaties om ongeautoriseerde toegang te krijgen, data te manipuleren of verstoringen te veroorzaken.

**Ethical hacking:** **Hacken**, maar in een **gecontroleerde omgeving met de toestemming** van de verantwoordelijken.

**Penetration testing (pentesting):** **Ethical hacking** met het doel om bijvoorbeeld de **systemen van een organisatie te controleren op zwakheden en deze dan te rapporteren**.

### Vulnerabilities

**Vulnerability:** Een **zwakheid die misbruikt kan worden**.

**Zero-Day:** Een **zwakheid** die misbruikt kan worden en die **nog niet bekend** is bij de ontwikkelaars.

**Threat:** Het **potentiële gevaar van een zwakheid** die misbruikt kan worden.

**Exploit:** Een **methode of techniek** die gebruikt wordt om **misbruik te maken van een zwakheid**.

**Zero-Day exploit:** Een **methode of techniek** die wordt gebruikt om een **Zero-Day te misbruiken**.

### Soorten hackers

**White hat:** Hackers die **met toestemming ethical hacking doen** met het doel om zwakheden te fixen.

**Black hat:** Hackers die **zonder toestemming zwakheden misbruiken**, meestal met het doel om daar iets uit te krijgen.

**Grey hat:** Hackers die **zonder toestemming hacken**, maar **meestal zwakheden rapporteren**.

### Threat actors

Een threat actor is een **individu of groep van black hat hackers**.

**Organized crime:** Hacker **groepen met veel "resources"** die de nieuwste aanvallen gebruiken, **meestal om geld te verdienen**.

**Hacktivists:** Hackers die als **doel hebben om een "statement" te maken, zonder geld er aan te willen verdienen**.

**Nation-state hackers (Advanced Persistent Threats - APTs):** Hacker **groepen die door overheden worden ondersteund** om aanvallen uit te voeren, bijvoorbeeld op andere overheden of journalisten.

**Insider threats:** Mensen die **binnen bijvoorbeeld een bedrijf werken** en intentioneel of per ongeluk, **aanvallers toegang geven tot gevoelige informatie**.

### Andere

**Countermeasure:** Een **beveiligingsactie** die gedaan wordt om een **zwakheid te voorkomen, verminderen of te fixen**.

**Reconnaissance:** Het proces van **informatie te verzamelen over een doelwit**.

**Patch:** Een **update** voor software **die zwakheden fixt**.

**Role-based access control (RBAC):** **Limiteren van permissies** op basis van de **rol van een gebruiker**.

**Disaster recovery plan (DRP):** Een **plan** dat **beschrijft hoe** er moet worden **omgegaan** met **bvb. een storing of cyberaanval**.

## CVE

**CVE:** Common Vulnerabilities and Exposures, een **systeem om zwakheden te identificeren**.

Als er een **zwakheid wordt geïdentificeerd krijgt deze een CVE ID**, daar wordt dan informatie bij gezet zoals hoe groot de impact is van de zwakheid.

Een CVE ID ziet er zo uit:
```
CVE - 2025 - 20265
        ^       ^
    Publicatie  |
    jaar        |
             Uniek ID
             dat per CVE
             1 omhoog gaat
```

### Termen CVE

**CNA (CVE Numbering Authority):** Bedrijven of andere die **CVE's rapporteren**.

**CVSS:** Een gestandaardiseerde methode om de impact van zwakheden te beoordelen. Dit helpt om prioriteiten te stellen voor wat eerst moet opgelost worden.

| CVSS score | Rating   |
|------------|----------|
| 0.0        | None     |
| 0.1 - 3.9  | Low      |
| 4.0 - 6.9  | Medium   |
| 7.0 - 8.9  | High     |
| 9.0 - 10.0 | Critical |

**EPSS (Exploit Prediction Scoring System):** Een **score die** wordt gegeven die de **geschatte kans toont dat een zwakheid wordt misbruikt**.

## Authentication

**De meest voorkomende manieren dat accounts worden gehackt:**
1. **Gestolen** wachtwoorden
2. **Zwakke** wachtwoorden
3. **Hergebruikte** wachtwoorden
4. **Brute force aanvallen** (wachtwoorden raden)

### Wachtwoord complexiteit

Je kan **al de mogelijke combinaties** van een wachtwoord op de volgende manier **uitrekenen**:
```
Complexiteit ^ Lengte
^                ^
Aantal bruikbare |
karakters        |
             Hoeveel karakters
             er in het wachtwoord zijn

Dus: Het aantal bruikbare karakters tot de macht van de hoeveelheid
karakters in het wachtwoord.

----------------------------------------------------------------------

Pin code: 4321
Aantal bruikbare karakters: 10 (0,1,2,...,9)
Hoeveel karakters: 4

10^4 = 10000 mogelijke combinaties
```

### Het is dus belangrijk dat je wachtwoord:
- **Complex** is
- **Uniek** voor elk account is
- **Geen persoonlijke informatie** bevat
- **Veranderd** wordt **wanneer deze gelekt** is

**Password manager:** Een **programma** dat je **wachtwoorden voor je bijhoudt** en **unieke wachtwoorden genereert**.

Elk **wachtwoord kan nog steeds gelekt worden**, gebruik dus **altijd multifactor authentication**.

**Multifactor authentication:** Het **verifiëren dat iemand de juiste persoon is via meerdere verschillende opties**.
Bijvoorbeeld: Wachtwoord ingeven en daarna via een authenticator app op je telefoon nog een code ingeven.

**Iets is multifactor authentication als de opties verschillend zijn.** Als je twee keer een wachtwoord moet ingeven is dit niet multifactor authentication.

**2FA vs MFA:** 2-Factor authentication is exact twee opties, Multi-Factor Authentication is 2 of meer opties.

### Waarom MFA?

Het beschermt tegen dingen zoals:
- **Credential stuffing:** Logins van één platform gaan proberen op andere platformen met de hoop dat deze login hergebruikt is.
- **Brute force attacks:** Het proberen van alle mogelijke opties om een wachtwoord te vinden.
- **Password spraying:** Zoals een brute force maar in de plaats van alle opties te proberen, proberen ze een lijst van wachtwoorden waarvan ze denken dat je misschien één daarvan gebruikt.

### OTP vs TOTP

**OTP:** One-Time Password, bijvoorbeeld een code die via sms wordt gestuurd vanwege een poging tot inloggen.

**TOTP:** Time-Based One-Time Password, een **code die om de zoveel tijd wordt veranderd** (om de 60 seconden...). Bijvoorbeeld Microsoft authenticator.

### Authenticatie beveiligen

Je **kan inlog pogingen blokkeren gebaseerd op IP** / locatie of op bepaalde tijden het aantal toegestane login pogingen verminderen.

**Passkeys:** Een **wachtwoord loze inlog methode** die gebruikt maakt van **crypto grafische sleutels**. Het werkt een beetje zoals SSH.

## Cybersecurity modellen

### CIA triad

De CIA triad is een **model** dat **drie belangrijke doelen** bevat:

1. **Confidentiality:** Alleen geautoriseerde personen mogen toegang hebben tot data.
   - Authenticatie: Verifiëren van identiteit. Inloggen op een website.
   - Autorisatie: Dingen (niet) toestaan op basis van rechten. Toegang blokkeren tot een bestand.
   - Accounting: Bijhouden van wat er gedaan is. Logging van acties.
2. **Integrity:** Data moet beschermd zijn tegen intentionele of onbedoelde wijzigingen.
   - Input controle: Controleren of data geldig is voordat het wordt verwerkt.
   - Back-ups: Regelmatig kopieën maken van data om te herstellen bij problemen.
   - Data hashing: Checksums gebruiken om te controleren of data niet is aangepast.
3. **Availability:** Data en systemen moeten altijd beschikbaar zijn.
    - Redundantie: Meerdere systemen of componenten gebruiken om uitval te voorkomen.
    - Back-ups: Regelmatig kopieën maken van data om te herstellen bij problemen.
    - DDoS bescherming: Bescherming tegen aanvallen die systemen onbeschikbaar maken.

### States of data

**Data** kan zich in **drie staten** bevinden:
1. **Data at rest:** Data die is opgeslagen op een apparaat of server.
2. **Data in transit:** Data die wordt verzonden over een netwerk.
3. **Data in use:** Data die actief wordt verwerkt door een applicatie of systeem.

### Beveiligingsmaatregelen

Er zijn **drie soorten beveiligingsmaatregelen**:
1. **Menselijke factor:** Training en bewustwording van medewerkers.
2. **Beleid en praktijken:** Regels en procedures.
3. **Technologie:** Firewalls, antivirus software, encryptie, etc.

### Cybersecurity cube

Een **model** dat helpt met het **visualiseren van** de **aspecten van cybersecurity**.\
Het heeft drie vlakken, elk vlak is één van de modellen hierboven:
- **CIA triad**
- **States of data**
- **Beveiligingsmaatregelen**

### Defense in Depth / Castle Approach

Het idee is om **meerdere lagen van beveiliging** te hebben, zodat als **één laag faalt**, de **andere lagen** nog steeds **bescherming bieden**.
```
Defense in Depth

                 ┌───────────────────────────────────────┐
                 │   POLICIES, PROCEDURES & AWARENESS    │
                 │  ┌──────────────┐   ┌──────────────┐  │
                 │  │     MFA      │   │   Training   │  │
                 │  └──────┬───────┘   └──────┬───────┘  │
                 │  ┌──────▼───────┐   ┌──────▼───────┐  │
                 │  │    RBAC      │   │   Policies   │  │
                 │  └──────────────┘   └──────────────┘  │
                 └───────────────────┬───────────────────┘
                                     │
                 ┌───────────────────▼───────────────────┐
                 │            PHYSICAL LAYER             │
                 │  ┌──────────────┐   ┌──────────────┐  │
                 │  │Access Control│   │ Surveillance │  │
                 │  └──────┬───────┘   └──────┬───────┘  │
                 │  ┌──────▼───────┐   ┌──────▼───────┐  │
                 │  │  Locks/Keys  │   │   Security   │  │
                 │  └──────────────┘   └──────────────┘  │
                 └───────────────────┬───────────────────┘
                                     │
                 ┌───────────────────▼───────────────────┐
                 │            PERIMETER LAYER            │
                 │  ┌──────────────┐   ┌──────────────┐  │
                 │  │     VPN      │   │   Firewall   │  │
                 │  └──────┬───────┘   └──────┬───────┘  │
                 │  ┌──────▼───────┐   ┌──────▼───────┐  │
                 │  │   IDS/IPS    │   │Content Filter│  │
                 │  └──────────────┘   └──────────────┘  │
                 └───────────────────┬───────────────────┘
                                     │
                 ┌───────────────────▼───────────────────┐
                 │            NETWORK LAYER              │
                 │  ┌──────────────┐   ┌──────────────┐  │
                 │  │   Firewall   │   │    VLAN      │  │
                 │  └──────┬───────┘   └──────┬───────┘  │
                 │  ┌──────▼───────┐   ┌──────▼───────┐  │
                 │  │   IDS/IPS    │   │Safe Protocols│  │
                 │  └──────┬───────┘   └──────┬───────┘  │
                 │  ┌──────▼───────┐   ┌──────▼───────┐  │
                 │  │     ACLs     │   │    (etc.)    │  │
                 │  └──────────────┘   └──────────────┘  │
                 └───────────────────┬───────────────────┘
                                     │
                 ┌───────────────────▼───────────────────┐
                 │              HOST LAYER               │
                 │  ┌──────────────┐   ┌──────────────┐  │
                 │  │  Antivirus   │   │   Patches    │  │
                 │  └──────┬───────┘   └──────┬───────┘  │
                 │  ┌──────▼───────┐   ┌──────▼───────┐  │
                 │  │ OS Hardening │   │    (etc.)    │  │
                 │  └──────────────┘   └──────────────┘  │
                 └───────────────────┬───────────────────┘
                                     │
                 ┌───────────────────▼───────────────────┐
                 │          APPLICATION LAYER            │
                 │  ┌──────────────┐   ┌──────────────┐  │
                 │  │     SSO      │   │     MFA      │  │
                 │  └──────┬───────┘   └──────┬───────┘  │
                 │  ┌──────▼───────┐   ┌──────────────┐  │
                 │  │     AAA      │   │    (etc.)    │  │
                 │  └──────────────┘   └──────────────┘  │
                 └───────────────────┬───────────────────┘
                                     │
                 ┌───────────────────▼───────────────────┐
                 │               DATA LAYER              │
                 │            ┌──────────────┐           │
                 │            │   Database   │           │
                 │            └──────────────┘           │
                 └───────────────────────────────────────┘
```

