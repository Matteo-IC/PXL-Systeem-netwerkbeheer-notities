# Machtigingen en services

## Services

### DHCP

DHCP is een **service** die **automatisch IP-adressen** toekent aan **computers** in een **netwerk**.

Een **DHCP server** is het apparaat dat de IP-adressen toewijst.\
Een DHCP server kan ook **andere instellingen** zoals **subnetmaskers, DNS servers en standaard gateways** toewijzen.

Een **DHCP client** is het apparaat dat een IP-adres aanvraagt.\
Een **IP-adres wordt tijdelijk toegewezen**, dit heet een **lease**.
Dit IP-adres komt uit een **pool van beschikbare adressen** genaamd de **DHCP scope**.

### DNS

DNS is een **service** die **domeinnamen vertaalt naar IP-adressen**.

**Soorten DNS-records**:
- **SOA** (Start of Authority):
    - Bevat **informatie over de DNS-zone**, zoals de **primaire DNS-server** en de **e-mail van de beheerder**.
    - Bevat ook een **serienummer** dat aangeeft wanneer de zone voor het laatst is bijgewerkt.
    - **Refresh time** en **retry time** geven aan hoe vaak de secundaire DNS-servers de zone moeten controleren op updates en hoe lang 
ze moeten wachten als het mislukt.
    - **Expire time** geeft aan hoe lang de secundaire DNS-servers moeten wachten als ze geen updates ontvangen voordat
ze het als ongeldig zien.
    - **TTL** (Time to Live) geeft aan hoe lang een record geldig is voordat het opnieuw moet worden opgehaald.
- **A record**:
    - Verbindt een **domeinnaam met een IPv4-adres**.
- **CNAME record**:
    - Is een **alias** voor een ander DNS-record, verwijst dus naar een ander A record.
- **PTR record**:
    - Verbindt een IP-adres met een domeinnaam, het omgekeerde van een A record.
- **MX record**:
    - Verbindt een domeinnaam met een **mailserver**.
- **NS record**:
    - Geeft weer wat de name servers zijn voor een bepaald domein.
- **SRV record**:
    - Geeft informatie over **services** die beschikbaar zijn op een domein, zoals **locatie en poort** van een service.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### DNS zones

Een **DNS-zone** is een **gedeelte van de DNS namespace** dat beheerd wordt door een specifieke organizatie of administrator.

**Soorten DNS-zones**:
- **Primaire zone**:
    - Bevat de **master kopie van de DNS-records**.
- **Secundaire zone**:
    - Een **read-only kopie van de primaire zone**.
    - Wordt gebruikt voor **load balancing** en **redundantie**.
- **Stub zone**:
    - Bevat alleen de **minimale informatie** die nodig is om DNS-queries te beantwoorden.
- **Reverse lookup zone**:
    - Wordt gebruikt om **IP-adressen naar domeinnamen te vertalen**.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Zone transfer

Een **zone transfer** is het proces waarbij een **secundaire DNS-server** een kopie van de DNS-records van een 
**primaire DNS-server** ophaalt.\
Wordt gebruikt voor **redundantie** en **load balancing**.

Er zijn twee soorten zone transfers:
- **Full zone transfer (AXFR)**:
    - De **hele zone** wordt overgedragen.
    - Gebruikt wanneer de secundaire server voor het eerst wordt ingesteld.
- **Incremental zone transfer (IXFR)**:
    - Alleen de **wijzigingen** sinds de laatste transfer **worden overgedragen**.
    - Bespaart bandbreedte en tijd.

Een zone transfer gebeurt altijd volgens deze stappen:
1. De **secundaire server vraagt het SOA-record** van de primaire server op.
2. Als het **serienummer** in het SOA-record **hoger** is dan die van de secundaire server, weet de secundaire server
dat er **wijzigingen** zijn.
3. De secundaire server vraagt een **AXFR** of **IXFR** transfer aan.
4. De primaire server stuurt de gevraagde gegevens naar de secundaire server.



## Machtigingen en file services

### NTFS-machtigingen

NTFS-machtigingen zijn **rechten** die worden **toegekend** aan **gebruikers en groepen** voor
**bestanden en mappen**.

Dit zijn **machtigingen zoals**:
- **Read**
- **Write**
- **Execute**
- ...

Deze kunnen toegestaan of geweigerd worden.

Er zijn ook **speciale machtigingen** zoals:
- **Change permissions**
- **Read permissions**
- **Create folders**
- **Delete**
- ...

**Machtigingen** worden **overgenomen** van de **bovenliggende map**.\
Dit **kan uitgeschakeld worden** om voor die map aparte machtigingen in te stellen.


### Shares & sharing

SMB is een **protocol** dat Windows Server gebruikt om **mappen, bestanden en printers te delen
via het netwerk.**

Bij het instellen van een SMB share zijn er 2 lagen van toegangsbeheer:
- **Share permissions**
    - **Toegangsrechten voor de share**.
    - Worden **toegepast voor NTFS-machtigingen** worden toegepast.
- **NTFS-machtigingen**
    - **Toegangsrechten** die **specifiek** zijn **voor de bestanden en mappen binnen de share**.

Een SMB **share is toegankelijk via \\\servernaam\sharenaam**.

### Administratieve shares

**Administrative shares** zijn **standaard shares** die **automatisch worden gemaakt** voor
**beheer en onderhoudstaken** door een Windows Server.

Ze zijn **niet zichtbaar voor gebruikers**, maar **toegankelijk voor beheerders via het netwerk**.

Standaard shares:
- **C$** (en andere: D\$, E\$):
    - Verborgen shares van lokale schijven.
- **ADMIN$**:
    - Share van de `C:\Windows` map.
- **IPC$**:
    - Inter-Process Communication share.
    - Tijdelijke share voor communicatie tussen processen en netwerkservices.
- **PRINT$**:
    - Share voor beheer van printers.
