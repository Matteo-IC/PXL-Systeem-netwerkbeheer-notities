# Filters

## Where filter

**Met het cmdlet `Where` kan je objecten filteren.**\
*`Where` is een alias voor `Where-Object`.*

```
Get-Process | Where Status -eq "stopped"
```

1. Alle **processen** worden **opgehaald** met `Get-Process`.
2. De **output** wordt **doorgegeven** aan `Where`.
3. `Where` **filtert** de processen waar de `Status` property **gelijk is aan `stopped`**.

## Vergelijkingsoperatoren

Je kan ook **andere vergelijkingsoperatoren** gebruiken:
```
-eq    # Is gelijk aan
-ceq   # Is gelijk aan (case-sensitive)
-ne    # Is niet gelijk aan
-cne   # Is niet gelijk aan (case-sensitive)
-gt    # Is groter dan
-lt    # Is kleiner dan
-ge    # Is groter dan of gelijk aan
-le    # Is kleiner dan of gelijk aan
```

Een **voorbeeld van `-gt`**:
```
Get-Process | Where CPU -gt 100
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Om te **checken** of een bepaalde **waarde in een lijst voorkomt**:
```
-contains     # <lijst> bevat <waarde>, geeft true/false terug
-ccontains    # <lijst> bevat <waarde> (case-sensitive)

-notcontains  # <lijst> bevat niet <waarde>, geeft true/false terug
-cnotcontains # <lijst> bevat niet <waarde> (case-sensitive)

-in           # <waarde> is in <lijst>, geeft true/false terug
-cin          # <waarde> is in <lijst> (case-sensitive)

-notin        # <waarde> is niet in <lijst>, geeft true/false terug
-cnotin       # <waarde> is niet in <lijst> (case-sensitive)
```

**Voorbeeld van `-contains` & `-in`:**
```
"abc", "def" -contains "abc"
True

"abc" -in "def", "abc"
True
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Er zijn ook **matching operatoren**:
```
-like      # Geeft de waarde(s) die overeenkomen met wildcard
-clike     # Geeft de waarde(s) die overeenkomen met wildcard (case-sensitive)

-notlike   # Geeft de waarde(s) die niet overeenkomen met wildcard
-cnotlike  # Geeft de waarde(s) die niet overeenkomen met wildcard (case-sensitive)

-match     # Geeft de waarde(s) die overeenkomen met regex patroon
-cmatch    # Geeft de waarde(s) die overeenkomen met regex patroon (case-sensitive)

-notmatch  # Geeft de waarde(s) die niet overeenkomen met regex patroon
-cnotmatch # Geeft de waarde(s) die niet overeenkomen met regex patroon (case-sensitive)
```

**Voorbeeld van `-like` & `-match`:**
```
Get-Process | Where ProcessName -like "a*"
Get-Process | Where ProcessName -match "^a"
```

## True en false

Veel van deze operatoren **geven `true` of `false` terug**.\
Dat zijn boolean waarden, het is oftewel waar of niet waar.

**Voorbeeld:**
```
Get-Service | Where CanStop -eq $true
```

Dat werkt omdat de **property `CanStop` als waarde een boolean heeft** (`true` of `false`).

## Script blokken

Een script blok is een stukje code dat waar of niet waar kan teruggeven.\
Je kan een **script blok maken met `{}`**.

In een script blok kan je **gebruik maken van `$_`**.\
`$_` verwijst naar het **huidige object** dat door de pipeline gaat.

**Voorbeeld:**
```
Get-Service | Where { $_.Status -eq "running" }
```

Door gebruik te maken van haakjes () kan je **complexere voorwaarden maken**.

## Logische operatoren

**Logische operatoren** kan je gebruiken om **meerdere voorwaarden te combineren**:
```
-and   # En
-or    # Of
-not   # Niet
```

**Voorbeelden:**
```
Get-Service | Where { ($_.Status -eq "running") -and ($_.CanStop -eq $true) }
^
Toon de services die aan beide voorwaarden voldoen: de status is "running" EN ze kunnen gestopt worden.

Get-Service | Where { ($_.Status -eq "running") -or ($_.StartType -eq "Automatic") }
^
Toon de services die aan minstens één van de voorwaarden voldoen: de status is "running" OF de starttype is "Automatic".

Get-Service | Where { -not ($_.Status -eq "stopped") }
^
Toon de services waarvan de status NIET "stopped" is.
```

Met haakjes in script blokken kan je voorwaarden aan elkaar koppelen.
