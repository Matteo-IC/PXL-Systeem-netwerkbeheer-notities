# Machtigingen en services

## Services

### DHCP

DHCP is een **service** die **automatisch IP-adressen** toekent aan **computers** in een **netwerk**.

Een **DHCP server** is het apparaat dat de IP-adressen toewijst.\
Een DHCP server kan ook **andere instellingen** zoals **subnetmaskers, DNS servers en standaard gateways** toewijzen.

Een **DHCP client** is het apparaat dat een IP-adres aanvraagt.\
Een **IP-adres wordt tijdelijk toegewezen**, dit heet een **lease**.
Dit IP-adres komt uit een **pool van beschikbare adressen** genaamd de **DHCP scope**.

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

Een SMB **share is toegankelijk via \\servernaam\sharenaam**.

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
