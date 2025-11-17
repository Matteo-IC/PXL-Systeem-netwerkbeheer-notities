# Objecten

## Hulp zoeken

### Get-Help

Je kan **hulp krijgen voor cmdlets met `Get-Help`**:

```
> Get-Help Get-Process
...
```

Om een **uitgebreidere uitleg** te krijgen, kan je **`Update-Help` uitvoeren**.

Dan kan je `-Detailed`, `-Full` of `-Examples` toevoegen aan `Get-Help` voor meer of specifieke informatie.

```
> Get-Help Get-Process -Detailed
...
```

### Cmdlets vinden

Je kan gemakkelijk cmdlets vinden met **`Help <command>`**.

```
> Help Process

Name                              Category  Module                    Synopsis
----                              --------  ------                    --------
Enter-PSHostProcess               Cmdlet
...
```

Dit is **ongeveer hetzelfde als `Get-Command *Process*`**.

```
> Get-Command *Process*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          ConvertTo-ProcessMitigationPolicy
...
Application     WinProcessListHelper.exe                           0.0.0.0    C:\Program Files\...
...
```

Hier worden nog andere dingen getoond, zoals applicaties.

### Windows services

Een **service** is een **programma** dat op de **achtergrond draait**.\
Deze zijn **gelijkaardig aan daemons in Linux**.

Deze services worden beheerd door de service controller, bv. `services.msc`.\
Werken zonder dat je bent ingelogd.

De services draaien in de context van één van de 3 standaard accounts:
- **Local System**
  - Heeft veel rechten, is deel van de Administrators groep.
- **Network Service**
  - Heeft minder rechten dan Local System, maar kan het netwerk gebruiken.
- **Local Service**
  - Heeft beperkte rechten en enkel op de lokale machine.

## Objecten

Een `.NET` **object is een stukje data in het geheugen** van de computer.\
Deze **objecten hebben eigenschappen** (properties) en **methodes** (functions).\
Objecten zijn van een bepaald **type** (class).

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Properties
Dit zijn **attributen** van het object.\
Bijvoorbeeld: een **`Process` object heeft** een **`Name` property die de naam van het proces bevat**.

Je kan de **properties van een object opvragen** met `Get-Service -Name w32time | Select-Object -Property *`.

Je kan ook de **waarde van een property opvragen** met de **`.` notatie**.
```
$service = Get-Service -Name W32Time

Write-Output $service.Status
```

Als je dat uitvoert, krijg je de status van W32Time service:
```
Stopped
```

### Methods

Dit zijn **functies** die je kan **uitvoeren op het object**.\
Bijvoorbeeld: een `Process` object heeft een `Stop()` method die het proces beëindigt.

Je kan de **methods van een object opvragen** met `Get-Service -Name w32time | Get-Member -Type Method`.

Je kan een method aanroepen met de **`.` notatie** gevolgd door haakjes.
```
$service = Get-Service -Name W32Time

$service.Start()

(Get-Service -Name W32Time).Start()
```

## Services beheren

Je hebt een aantal cmdlets om services te beheren:
```
Get-Service -Name <service_naam>     # Haalt de status op
Start-Service -Name <service_naam>   # Start de service
Stop-Service -Name <service_naam>    # Stopt de service
Restart-Service -Name <service_naam> # Herstart de service
Suspend-Service -Name <service_naam> # Pauzeert de service
```
