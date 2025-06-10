# Profiles en folder redirection

Een **Windows-profiel** is een verzameling van instellingen en bestanden.\
Een gebruikersprofiel bestaat onder andere uit:
- **Gebruikersinstellingen** zoals bureaubladachtergrond, thema's, en taalvoorkeuren.
- **Bestanden en mappen** zoals documenten, afbeeldingen, en downloads.
- **Toepassingsinstellingen** zoals configuraties voor geïnstalleerde software.
- **Registerinstellingen** die specifieke voorkeuren en instellingen voor de gebruiker bevatten.
- **Alles in de map C:\Users\Gebruikersnaam**.

## Types van profielen

Verschillende versies van Windows hebben een andere structuur voor gebruikersprofielen.\
Daarom worden er versie nummers gebruikt:
- **V1 - V4**: Deze versies zijn voor oudere Windows-versies zoals Windows XP, Windows 7 en Windows 8.
- **V5**: Deze versie is voor Windows 10 en Windows Server 2016.
- **V6**: Deze versie is voor Windows 11 en Windows Server 2022.

## Soorten profielen

### Lokale profielen

Een **lokaal profiel** is een profiel dat **alleen op de lokale computer** wordt opgeslagen.\
Het is **niet beschikbaar op andere computers**, en wijzigingen worden **niet gesynchroniseerd** met andere apparaten.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Roaming profielen

Een **roaming profiel** is een profiel dat wordt **opgeslagen op** een **netwerk locatie** en **kan worden gebruikt** op
**verschillende computers** binnen een netwerk.

Het profiel wordt **gesynchroniseerd met** de **netwerkserver**, zodat gebruikers hun **instellingen en bestanden** 
kunnen **behouden** wanneer ze **inloggen op een andere computer**.\
Het **synchroniseren** van roaming profielen **kan** echter **langzaam zijn** en is **gevoelig voor netwerkproblemen**.

Je kan met **folder redirection** de **grote mappen uit** het **profiel halen** zodat deze niet elke keer moeten synchroniseren.\
Hierdoor wordt het profiel **sneller geladen**. 

Er zijn **verschillende soorten roaming profielen**:
- **Cached roaming profielen**: Deze profielen hebben lokaal een kopie van het profiel.
  - Sneller inloggen, en offline beschikbaar.
  - Kan veel ruimte in beslag nemen en synchronisatieproblemen veroorzaken.
- **Non-cached roaming profielen**: Deze profielen worden niet lokaal opgeslagen.
  - Langzamer inloggen, maar minder ruimtegebruik.
  - Gebruikers kunnen niet offline werken.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Mandatory profielen

Een **mandatory profiel** is een soort **guest profiel**. Ze kunnen **niet worden aangepast door de gebruiker** en worden
bij elke login **teruggezet naar de standaardinstellingen**.

Het wordt **centraal beheerd** en is handig voor bijvoorbeeld schoolomgevingen.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Hybride profielen

Een **hybride profiel** is een profiel dat een **combinatie** is van on-premise **AD** en de cloud **Azure AD**.\
Accounts en apparaten worden in beide geregistreerd met de hulp van **Azure AD Connect**.

Een aantal **voordelen** zijn:
- **Single sign-on (SSO)** is mogelijk waardoor gebruikers maar één keer moeten inloggen.
- **Multi factor authenticatie (MFA)** kan worden gebruikt voor extra beveiliging.
- **Migreren naar de cloud is eenvoudiger.**
- **Beheer van apparaten** is mogelijk via **Intune** of andere cloudgebaseerde beheertools.

## Folder redirection

**Folder redirection** is een **functie** die **bepaalde mappen** van een gebruikersprofiel **verplaatst naar een 
netwerklocatie**.

**Voordelen:**
- **Minder grote roaming profielen**: Gebruikersmappen kunnen worden verplaatst naar een netwerkshare wat inloggen versnelt.
- **Back-up en herstel**: Mappen kunnen worden opgeslagen op de server, wat het back-ups en beheer vergemakkelijkt.
- **Toegankelijkheid**: Gebruikers kunnen hun bestanden openen vanaf verschillende apparaten binnen het netwerk.
- **Minder opslag nodig**: Lokale machines moeten geen kopieën van deze mappen bewaren, wat opslagruimte bespaart.

**Nadelen:**
- **Netwerkafhankelijkheid**: Gebruikers hebben een netwerkverbinding nodig om toegang te krijgen tot hun up-to-date bestanden.
  - De bestanden worden gecached op de lokale computer, als er internet is worden deze gesynchroniseerd.
- **Belasting van de server**: Het kan de netwerk- en serverprestaties beïnvloeden, vooral bij grote bestanden of veel gebruikers.

### Folder redirection instellen

1. **Maak** een **gedeelde map** op de server die toegankelijk is voor de gebruikers.
2. Stel de juiste **machtigingen** in.
3. Maak een nieuwe **Group Policy Object (GPO)**.
4. Navigeer naar **User Configuration > Policies > Windows Settings > Folder Redirection**.
5. **Selecteer** de **map** die je **wilt omleiden**.
6. Kies de optie die je nodig hebt.
7. Stel de **doelmap** in.



