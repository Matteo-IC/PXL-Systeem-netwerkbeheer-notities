# Studeren

## 1. Introductie & Installatie

<deflist collapsible="true">
<def title="Wat zijn 4 categorieën van besturingssystemen?">
<p><control>Desktop</control></p>
<p><control>Server</control></p>
<p><control>Mobile</control></p>
<p><control>Embedded</control></p>
</def>

<def title="Wat zijn de meest voorkomende Windows edities?">
<p><control>Home</control></p>
<p><control>Pro</control></p>
<p><control>Enterprise</control></p>
<p><control>Education</control></p>
</def>

<def title="Noem de belangrijkste 4 verschillen tussen de Pro en Home editie.">
<p><control>Remote Desktop</control></p>
<p><control>Hyper-V</control></p>
<p><control>Bitlocker</control></p>
<p><control>Active Directory</control></p>
</def>

<def title="Waarom gebruikt men de Enterprise of Education editie?">
<p>Computers met deze edities kunnen beheerd worden via <control>Microsoft 365</control></p>
<p>Extra beveiligingsfuncties.</p>
</def>

<def title="Wat zijn nog overige minder gebruikte edities en voor wat zijn ze?">
<p><control>1. Pro for Workstation:</control></p>
Hetzelfde als Pro maar met het <control>ReFS bestandssysteem</control>.
<p><control>2. IoT Enterprise:</control></p>
Editie voor <control>embedded systemen</control>.
<p><control>3. Enterprise Multi-Session:</control></p>
<control>Meerdere mensen kunnen tegelijk op deze computer</control> via Azure Virtual Desktop.
<p><control>4. SE:</control></p>
Editie voor <control>zwakke toestellen in het onderwijs</control>.
</def>

<def title="Wat zijn N edities?">
Varianten van alle <control>Windows edities die aan Europese wetgeving voldoen</control>. Zo kunnen gebruikers <control>zelf kiezen welke multimedia-applicaties</control> ze willen gebruiken.
</def>

<def title="Wat is een groepsbeleid en hoe open je de beheer console?">
Een <control>centraal beheerde instelling</control>, de instelling <control>beperkt of verbreedt wat gebruikers en computers mogen</control>.

<p>1. Windows toets + r -> gpmc.msc</p>
<p>2. Start menu zoekbalk -> Group Policy Management Console</p>
</def>

<def title="Wat is: secure boot, Windows Hello en Hyper-V?">
<p><control>1. Secure boot:</control></p>
Beveiligingsfunctie die het <control>starten voorkomt van niet geauthentiseerde software</control> bij het opstarten van Windows.
<p><control>2. Windows Hello:</control></p>
<control>Alternatieve manieren voor authenticatie</control> zoals vingerafdruk.
<p><control>3. Hyper-V:</control></p>
<control>Virtualisatie platform van Microsoft</control> voor virtuele machines aan te maken en te beheren
</def>

<def title="Wat is S-Mode &amp; Windows Sandbox?">
<p><control>1. S-Mode:</control></p>
Beperkt Windows zodat het <control>alleen applicaties van de Microsoft Store kan installeren</control>.
<p><control>2. Windows Sandbox:</control></p>
Een <control>lichtgewicht virtuele machine</control> waar je applicaties in isolatie kan gebruiken.
</def>

<def title="Wat zijn de 4 types van gebruikers?">
<p><control>1. Lokaal account</control></p>
<p><control>2. Microsoft persoonlijk account</control></p>
<p><control>3. Active Directory account</control></p>
<p><control>4. Microsoft 365 werk of school account</control></p>
</def>

<def title="Wat is Active Directory?">
Een <control>systeem om gebruikers en computers te beheren</control> op het netwerk van je bedrijf.
</def>

<def title="Wat is LTSC, GAC &amp; Insider Preview?">
Dit zijn <control>release channels</control>, elk krijgt andere updates / updates op andere momenten.

<p><control>LTSC (Long Term Service Channel):</control></p>
Voor embedded devices die niet veel veranderen maar lang moeten blijven werken.
<p><control>GAC (General Availability Channel):</control></p>
De standaard voor Windows 10 & 11, updates zijn beschikbaar zodra ze bestaan.
<p><control>Insider Preview:</control></p>
Release channel waar de <control>nieuwste functies kunnen worden gebruikt</control>.
</def>

<def title="Uit welke delen bestaat een versie en een build number?">
<p><control>Versienummer:</control></p> 
De hoofdversie van het systeem. Bijvoorbeeld 24H2 of 1903. 24 voor het jaar (2024) en H2 voor welke helft van het jaar
<p><control>KB nummer:</control></p>
Unieke code voor de specifieke update. Bijvoorbeeld 22621.4037, 22621 voor de versie en 4037 voor de update
</def>

<def title="Wat is RISC, CISC &amp; ARM?">
<control>RISC & CISC</control> zijn verschillende architecturen voor processoren.
<p><control>ARM</control> is een versie van RISC.</p>
</def>

<def title="Wat is de kernel &amp; wat is een stuurprogramma / driver?">
<p><control>Kernel:</control></p>
Het centrale onderdeel van een besturingssysteem. Regelt de <control>communicatie tussen software en hardware</control>.
<p><control>Stuurprogramma / driver:</control></p>
Windows ondersteunt niet alle hardware, deze software <control>maakt communicate tussen software en niet standaard ondersteunde hardware mogelijk</control>.
</def>

<def title="Welke types gebruikers kan je gebruiken in de meest voorkomende Windows edities?">
<p><control>Windows Home:</control></p>
<p>- Microsoft 365 persoonlijk account</p>

<p><control>Windows Pro:</control></p>
<p>- Microsoft 365 persoonlijk account</p>
<p>- Microsoft 365 werk-of schoolaccount</p>
<p>- Lokaal Account</p>
<p>- Active Directory</p>

<p><control>Windows Enterprise en Education:</control></p>
<p>- Microsoft 365 werk-of schoolaccount</p>
<p>- Lokaal account</p>
<p>- Active Directory</p>

<p><control>Windows SE:</control></p>
<p>- Microsoft 365 schoolaccount</p>
</def>
</deflist>

## 2. Lokaal beheer

<deflist collapsible="true">
<def title="Wat is MMC en hoe open je het?">
<control>Microsoft Management Console</control> is een centrale plaats waar je in één plaats alle administratieve tools kan gebruiken.

<control>Windows toets + r -> mmc.msc</control>
</def>

<def title="Wat is een SID?">
Een <control>Security Identifier</control> is een <control>unieke code</control> dat gebruikt wordt om <control>gebruikers, groepen en processen te identificeren</control>.
</def>

<def title="Wat zijn de 3 meest gebruikte groepen?">
<p><control>Administrators</control></p>
<p><control>Gebruikers</control></p>
<p><control>Gasten</control></p>
</def>

<def title="Wat is het verschil tussen een applicatie en een service?">
<p><control>Applicatie:</control></p>
<p>- Wordt gestart door de gebruiker</p>
<p>- Heeft meestal een GUI</p>
<p>- Doet dingen voor de gebruiker</p>

<p><control>Service:</control></p>
<p>- Start automatisch</p>
<p>- Draait op de achtergrond</p>
<p>- Doet dingen voor applicaties of systemen</p>
</def>

<def title="Wat zijn de drie ingebouwde gebruikers die door services gebruikt worden en wat doen ze?">
<p><control>Local Service:</control></p>
Heeft minimale privileges die gelimiteerd zijn tot de lokale computer en zeer beperkte netwerkcommunicatie
<p><control>Network Service:</control></p>
Heeft minimale lokale privileges, presenteert de inloggegevens van de computer aan andere netwerken
<p><control>Local System:</control></p>
Heeft uitgebreide privileges, is deel van de groep administrators
</def>

<def title="Wat is een proces en wat is een thread?">
<p><control>Proces:</control></p>
Een <control>groep van threads</control> die een gereserveerd deel hebben in het geheugen, dezelfde rechten hebben en dezelfde resources delen.
<p><control>Thread:</control></p>
Dit voert echt code uit, een soort "mini" proces. Het deelt geheugen en andere resources met threads binnen hetzelfde proces. Dit is wat <control>een core op een CPU uitvoert</control>.
</def>

<def title="Wat is multitasking, multiprocessing en Hyper-Threading?">
<p><control>Multitasking:</control></p>
Dit betekent dat een core super <control>snel tussen processen schakelt</control>.
<p><control>Multiprocessing:</control></p>
Dit betekent dat een CPU <control>meerdere cores heeft waardoor die meerdere processen tegelijk</control> kan doen.
<p><control>Hyper-Threading:</control></p>
<control>Deelt 1 fysieke core op in 2 "logische cores"</control> door de resources van 1 core te splitten
</def>

<def title="Wat is Master Boot Record &amp; GUID Partitie Tabel?">
<p><control>MBR (Master Boot Record):</control></p>
Een verouderd partitieschema.
<p><control>GPT (GUID Partitie Tabel):</control></p>
Een modern partitieschema. Dit is een standaard voor de indeling van een partitie tabel.
</def>

<def title="Noem 4 bestandssystemen en door welk OS ze gebruikt worden.">
<p><control>FAT32:</control></p>
Oud maar ondersteunt veel.
<p><control>NTFS:</control></p>
Microsoft's bestandssysteem, Windows.
<p><control>EXT4:</control></p>
Standaard Linux bestandssysteem.
<p><control>APFS:</control></p>
Standaard MAC bestandssysteem
</def>

<def title="Wat is het verschil tussen een volume en een partitie?">
<p><control>Partitie:</control></p>
Één afgebakend deel op een schijf.
<p><control>Volume:</control></p>
Een opslaggebied dat zich over meerdere partities of schijven kan strekken. Een volume krijgt ook altijd een letter toegekend.
</def>

<def title="Uit welke 4 partities bestaat een Windows installatie?">
<p><control>System:</control></p>
FAT32, Opstartbestanden en bootloader.
<p><control>Reserved/MSR:</control></p>
Niet geformatteerd. Microsoft Reserved Partition, bevat metadata.
<p><control>Primair:</control></p>
NTFS, Partitie waar alle applicatie en gebruikersdata wordt opgeslagen
<p><control>Recovery:</control></p> 
NTFS, Gegevens voor Windows Recovery Environment
</def>

<def title="Wat is spanning?">
Een techniek waarbij een <control>volume over meerdere fysieke schijven</control> strekt.
</def>

<def title="Wat is &#37;appdata&#37;">
Een <control>omgevingsvariabele</control>. Windows heeft variabelen die dingen zoals paden bevatten.
</def>
</deflist>

## 3. Instellingen

<deflist collapsible="true">
<def title="Wat is een ADMX bestand &amp; wat is een ADML bestand?">
<p><control>ADMX:</control></p>
Een bestand met de settings voor de Group Policy Editor. <control>ADMX bestanden linken de settings van de GPE aan key value pairs van het Registry</control>
<p><control>ADML:</control></p>
Het <control>bestand dat de namen van de settings in de GPE bevat</control>. ADML bestanden bestaan in meerdere talen
</def>

<def title="Welke soorten updates zijn er?">
<p><control>Feature updates:</control> Jaarlijkse update die nieuwe functionaliteiten en meer toevoegt</p>
<p><control>Quality updates:</control> Verschijnen om de ~1-2 weken, bugfixes en beveiligingsupdates</p>
<p><control>Driver updates:</control> Update voor hardware</p>
<p><control>Definition updates:</control> Updates van virus definities voor Windows Defender</p>
<p><control>Other updates:</control> Alle andere updates</p>
<p><control>Optional updates:</control> Optionele updates die niet automatisch geïnstalleerd worden</p>
</def>

<def title="Hoe kom je in het System Recovery Environment?">
<p><control>Via instellingen:</control></p>
Systeem -> Systeemherstel -> Geavanceerde startopties
<p><control>Via het login scherm:</control></p>
Rechtsonder op opnieuw herstarten drukken terwijl je shift inhoudt
</def>

<def title="Wat is het Windows register?">
Een <control>database waarin bijna alle configuratie gegevens voor Windows, toepassingen en hardware staat</control>.
</def>

<def title="Over welke dingen gaan HKEY_CLASSES_ROOT &amp; HKEY_CURRENT_CONFIG?">
<p><control>HKEY_CLASSES_ROOT:</control></p>
Een registry hive / <control>groep waar informatie staat over de geregistreerde bestandstypen en welke programma's daar bij horen</control> voor de huidige gebruiker.
<p><control>HKEY_CURRENT_CONFIG:</control></p>
Een registry hive / <control>groep waar informatie staat over de hardware configuratie van het huidige systeem profiel</control>.
</def>

<def title="Wat doet het command ipconfig?">
<control>Toont IP info.</control>
</def>

<def title="Wat is een .bat bestand?">
Een <control>Batch file is een script</control> met een reeks van Windows cmd commands.
</def>
</deflist>

## 4. Powershell

<deflist collapsible="true">
<def title="Wat is een parameter?">
Een <control>extra waarde die je aan een cmdlet kan geven</control> om de uitvoering the beïnvloeden of om specifieke opties mee te geven.
</def>

<def title="Welke parameters zijn er om te vergelijken?">
<p><control>-gt:</control> Groter dan</p>
<p><control>-lt:</control> Kleiner dan</p>
<p><control>-ge:</control> Groter of gelijk aan</p>
<p><control>-le:</control> Kleiner of gelijk aan</p>
<p><control>-eq:</control> Gelijk</p>
</def>

<def title="Wat doet dit cmdlet: Get-Command *proces?">
<control>Toont alle cmdlets waar "proces" op het einde staat</control>
</def>

<def title="Wat doet dit cmdlet: Get-Alias -Definition Stop-Process?">
<control>Toont de aliassen van het cmdlet "Stop-Process"</control>
</def>

<def title="Wat doet dit cmdlet: Get-Help Get-Service -Parameter *?">
<control>Toont de parameters van "Get-Service" en geeft extra informatie over deze</control>
</def>

<def title="Wat doet dit cmdlet: Get-Process explorer | Select-Object id, Name, CPU, WorkingSet?">
<p><control>1. Vraagt de info op van het proces "explorer"</control></p>
<p><control>2. Weergeeft enkel: id, Name, CPU & Workingset.</control></p>
</def>

<def title="Wat doet dit cmdlet: Get-Service | Where-Object status -eq Running?">
<p>1. Opvragen van alle services.</p>
<p>2. Filtert die services zodat alleen de actieve getoond worden.</p>
</def>

<def title="Welke slash moet in paden gebruikt worden: / of \?">
<p>Paden in Windows gebruiken \.</p>
</def>

<def title="Leg uit wat elk Powershell scripting recht betekent: Restricted, AllSigned, RemoteSigned, Unrestricted &amp; Bypass.">
<p><control>1. Restricted:</control></p>
<control>Voorkomt</control> dat Powershell scripts worden uitgevoerd.
<p><control>2. AllSigned:</control></p>
Enkel Powershell scripts die <control>ondertekend zijn door een vertrouwde uitgever</control> kunnen uitgevoerd worden.
<p><control>3. RemoteSigned:</control></p>
Al de scripts die bij <control>AllSigned werken en zelf gemaakte scripts</control>.
<p><control>4. Unrestricted:</control></p>
<control>Alle scripts</control> mogen uitgevoerd worden maar <control>bij gedownloade scripts komt er een waarschuwing</control>.
<p><control>5. Bypass</control></p>
<control>Alles</control> mag uitgevoerd worden, <control>zonder waarschuwingen</control>.
</def>

<def title="Welke opties zijn er bij de parameter -Scope voor het cmdlet Set-ExecutionPolicy en wat betekenen ze?">
<p>1. LocalMachine: Zet de scope voor de <control>execution policy voor alle gebruikers</control>.</p>
<p>2. CurrentUser: Zet de scope voor de execution policy voor <control>alleen de huidige gebruiker</control>.</p>
<p>3. Process: Zet de scope voor de execution policy voor <control>enkel deze Powershell sessie</control>.</p>
</def>

<def title="Wat is Powershell ISE?">
Een <control>script editor</control> die standaard aanwezig is in Windows. Het wordt <control>niet meer actief ontwikkeld</control>.
</def>
</deflist>