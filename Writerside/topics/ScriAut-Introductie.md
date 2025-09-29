# Introductie

Scripting wordt gebruikt om **taken te automatiseren**.

## PowerShell

**PowerShell** is een **scripting taal** en command line shell.

### PowerShell versies

PowerShell heeft verschillende versies:
- **PowerShell 1.0**
  - Oude basis versie.
- **PowerShell 5.1**
  - Oude versie die standaard op Windows 10/11/Server 2019 staat.
- **PowerShell 6.0**
  - Eerste versie die cross-platform is.
- **PowerShell 7.x**
  - Huidige versie.
  - Cross-platform.
  - Gebaseerd op .NET Core.
  - Verbeterd.

Je kan je **versie controleren** met:
```
> $PSVersionTable
```

### Execution Policies

PowerShell heeft **execution policies** om te **bepalen of en hoe scripts uitgevoerd** mogen worden.

Deze zijn:
- **Restricted**
  - Scripts mogen niet uitgevoerd worden. Individuele commando's wel.
- **AllSigned**
  - Scripts moeten ondertekend zijn door een vertrouwde uitgever.
- **RemoteSigned**
  - Lokale scripts mogen uitgevoerd worden. Externe scripts moeten ondertekend zijn.
- **Unrestricted**
  - Scripts mogen altijd uitgevoerd worden. Waarschuwing bij externe scripts.
- **Bypass**
  - Geen beperkingen. Geen waarschuwingen.
- **Default**
  - Standaard instelling.
- **Undefined**
  - Standaard voor niet Windows systemen. Werkt zoals Unrestricted.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Execution policy wijzigen** (moet als administrator):
```
> Set-ExecutionPolicy <Policy>
```

**Huidige policy bekijken:**
```
> Get-ExecutionPolicy
```


### Windows Package Managers

Windows heeft verschillende **package managers** om **software te installeren en beheren**:
- **Chocolatey**
- **Winget**
- **Scoop**

### VSCode

**VSCode** is een **code-editor** die veel gebruikt wordt voor **scripting**.

Je kan het gemakkelijk installeren met bijvoorbeeld **Winget**:
```
> winget install Microsoft.VisualStudioCode
```

In **VSCode** kan je **PowerShell scripts schrijven en uitvoeren**.
```
Write-Output "Hello, World!"
```

