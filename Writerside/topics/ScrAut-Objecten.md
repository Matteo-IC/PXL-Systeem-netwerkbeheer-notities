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

## Objecten

