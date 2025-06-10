# Domein Uitbreidingen

## Global catalog server

Een Global Catalog server (**GC**) is een **domeincontroller** die een gedeeltelijke **read only kopie**
**van alle objecten** in het **forest** bevat.

De **GC** bevat **informatie over alle objecten** in het **forest** en **niet enkel** de objecten in zijn **eigen domain**.

## Trust

Een **trust** is een **relatie tussen 2 domeinen** die **toelaat om resources te delen**.

**Transitieve trusts** zijn trusts die **automatisch gecreëerd worden**,
als **domein A domein B vertrouwt** en **domein B domein C vertrouwt**, dan **vertrouwt domein A domein C** automatisch.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Trusts** kunnen worden **gecategoriseerd** aan de hand van:
- **Richting**
  - **One-way trust**
    - Als het ene domein het andere vertrouwt, maar niet omgekeerd.
  - **Two-way trust**
    - Als beide domeinen elkaar vertrouwen.
- **Bereik**
  - **Intra forest trust**
    - Trusts **binnen hetzelfde forest**.
    - **Parent-child trust**
      - Automatisch aangemaakt tussen **parent en child domain**.
    - **Tree-root trust**
      - Automatisch aangemaakt tussen **root domain en child domain**.
  - **Inter forest trust**
    - Trusts **tussen verschillende forests**.
    - **External trust**
      - Handmatig geconfigureerde trust tussen **domeinen uit 2 forests**.
    - **Forest trust**
      - Handmatig geconfigureerde trust tussen **2 volledige forests**.
    - **Shortcut trust**
      - **Versnelt verificatie** tussen domeinen die anders meerdere trust hops zouden moeten maken.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Type authenticatie:**
- NTLM trust (oud en onveilig)
- Kerberos trust (nieuw en veilig)


## Additional domain controllers

Een **extra domain controller** zorgt voor **redundantie**, extra **performantie** en **load balancing**.

**Voordat** je een **extra DC kan toevoegen** moet je een paar dingen **controleren**:
- **Gebruik de commando's:**
  - `dcdiag /v` om de gezondheid van de DC te controleren.
  - `repadmin /replsummary` om de replicatie status te controleren.
- De nieuwe DC moet een **vast IP-adres** hebben.
- De **versie** van de **nieuwe DC** moet **gelijk** zijn aan **of hoger** dan de **bestaande DC**.

**Na het toevoegen** van de nieuwe DC moet je **controleren** of die goed werkt:
- **Gebruik de commando's:**
  - `dcdiag /c` om de gezondheid van de nieuwe DC te controleren.
  - `repadmin /showrepl` om de replicatie status te controleren.
- Controleer of alle **AD-objecten** ook op de **nieuwe DC aanwezig** zijn.

## Multi master replication

Multi master replication betekent dat **alle domeincontrollers** in een domein de **AD-database kunnen wijzigen**.\
Deze wijzigingen worden automatisch **gerepliceerd naar** alle **andere domeincontrollers**.\
Dit wordt **gebruikt door Windows Server 2022**.

Single master replication betekent dat **slechts één domeincontroller** de **AD-database kan wijzigen**.

### Stappen van multi master replication

1. **Wijziging aanbrengen** op een domeincontroller.
2. **Wijziging wordt opgeslagen** in de **lokale AD-database** (NTDS.dit).
3. **Replicatie** van de wijziging naar **andere domeincontrollers**.
   1. Dit maakt gebruik van het **pull-model**.
   2. Elke domeincontroller **vraagt actief** voor de laatste wijzigingen.

**AD** gebruikt **Update Sequence Numbers (USN)** en **tombstone timestamps** om te bepalen **welke wijzigingen** zijn 
**doorgevoerd** en om **conflicten te detecteren**.

**USN** is een **uniek nummer** dat elke **wijziging** in de AD-database **identificeert**.\
Als er een **conflict** optreedt, wordt de wijziging met het **hoogste USN** of **recentste timestamp behouden**.

Zo worden **verouderde wijzigingen** en **conflicten** tussen domeincontrollers **voorkomen**.

## SID en GUID

### SID

Een **SID (Security Identifier)** is een **unieke identifier** die aan **elk beveiligingsobject** in Windows wordt gegeven.\
Dat kan een **gebruiker, groep, computer, proces...** zijn.\
Als een **object** bijvoorbeeld van **naam verandert**, blijft de **SID hetzelfde**.

Een **SID** wordt gebruikt om **toegang tot resources** te **verlenen** en om **rechten toe te kennen**.\
De **SID** van bijvoorbeeld een **gebruiker** wordt **vergeleken** met de **SID's** die **toegang verlenen** tot een **resource**.

Een aantal belangrijke **SID's** zijn:
- **S-1-5-18**: Local System
- **S-1-1-0**: Everyone
- **S-1-5-32-544**: Administrators

### GUID

Een **GUID (Globally Unique Identifier)** is een **unieke identifier** die wordt gebruikt om **elk object** in Active 
Directory te **identificeren**.\
**SID's** worden gebruikt voor **beveiliging**, terwijl **GUID's** worden gebruikt voor **identificatie**.

Een **GUID verandert nooit**, zelfs niet als het object wordt verplaatst naar een ander domein.\
Een **SID kan wel veranderen** als het object van domein wordt verplaatst.

**GUID's** zijn **belangrijk** voor het **repliceren** van **objecten tussen domeinen**. 

