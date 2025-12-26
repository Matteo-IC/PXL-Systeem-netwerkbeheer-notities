# Hashing

**Hashing** is een **proces** dat **data omzet** naar een **onomkeerbaar stuk tekst** van een **vaste lengte**.

**Hashing:**
- Produceert **altijd dezelfde** hash voor **dezelfde input**.
- Is **onomkeerbaar**.
  - Je kan wel de **originele data vinden** door **"brute force"** alle mogelijke inputs om te zetten naar een hash en die dan te vergelijken.
- Produceert **altijd een hash van dezelfde lengte**, ongeacht de lengte van de input.
- Maakt een **volledig andere hash** voor zelfs een **kleine verandering in de input**.
- Probeert te **vermijden** dat twee **verschillende inputs dezelfde hash produceren**.

## Hashing vs Encryptie vs Encoding

**Hashing, encryptie, en encoding** hebben verschillende doelen en zijn **niet hetzelfde**.

<table>
    <tr>
        <td><control>Hashing</control></td>
        <td>Encryptie</td>
        <td>Encoding</td>
    </tr>
    <tr>
        <td><control>Onomkeerbaar</control></td>
        <td>Omkeerbaar (met sleutel)</td>
        <td>Omkeerbaar</td>
    </tr>
    <tr>
        <td><control>Vaste output lengte</control></td>
        <td>Variabele output lengte</td>
        <td>Variabele output lengte</td>
    </tr>
    <tr>
        <td><control>Gebruikt voor data-integriteit, wachtwoord opslag.</control></td>
        <td>Gebruikt voor beschermen van data.</td>
        <td>Gebruikt voor data in ander formaat te zetten.</td>
    </tr>
</table>

## Hoe en waarom wordt hashing gebruikt?

Hashing wordt vaak gebruikt voor **wachtwoord opslag** en **data-integriteit verificatie**.

### Wachtwoord opslag

Stel dat een **gebruiker wil inloggen** op een website.\
De website heeft het **wachtwoord niet opgeslagen**, maar de **hash van het wachtwoord wel**.

```
    ┌──────────────┐
    │ Login pagina │
    └──────┬───────┘
           │
           │ Gebruiker voert wachtwoord in.
           ▼
    ┌──────────────┐
    │ Hash functie │
    └──────┬───────┘
           │
           │ De functie zet het wachtwoord om in een hash.
           ▼
    ┌──────────────┐
    │ Vergelijking │
    │ met hash in  │
    │ database     │
    └──────┬───────┘
           │
           │ Als de hashes overeenkomen is het wachtwoord correct.
           ▼
    ┌──────────────┐
    │ Toegang      │
    │ verleend of  │
    │ geweigerd    │
    └──────────────┘
```

### Data-integriteit verificatie

Hashing wordt ook gebruikt om te **verifiëren dat data niet is veranderd** tijdens bv. overdracht of opslag.

```
    ┌──────────────┐
    │ Originele    │
    │ data         │
    └──────┬───────┘
           │
           │ Hash functie genereert hash van originele data.
           ▼
    ┌──────────────┐
    │ Verzending   │
    │ van data en  │
    │ hash         │
    └──────┬───────┘
           │
           │ Ontvanger ontvangt data en hash.
           ▼
    ┌──────────────┐
    │ Hash functie │
    └──────┬───────┘
           │
           │ Genereert hash van ontvangen data.
           ▼
    ┌──────────────┐
    │ Vergelijking │
    │ van hashes   │
    └──────┬───────┘
           │
           │ Als de hashes overeenkomen is de data intact.
           ▼
    ┌──────────────┐
    │ Data is      │
    │ intact of    │
    │ gewijzigd    │
    └──────────────┘
```

## Hashing algoritmes

Er zijn **verschillende hashing algoritmes, elk** is anders en **beter of slechter voor verschillende toepassingen**.

### Data-integriteit algoritmes

Er bestaan veel algoritmes voor data-integriteit, zoals:
- **MD5:** Vroeger veelgebruikt, maar nu verouderd.
- **SHA-1:** Ook verouderd vanwege kwetsbaarheden.
- **SHA-256:** Moderner en veiliger, veel gebruikt.
- **SHA-3:** Nieuwste standaard, nog beter.

### Wachtwoord hashing algoritmes

Wachtwoord hashing algoritmes zijn ontworpen om **zwaar om te berekenen te zijn**, zodat **brute-forcing moeilijker** wordt.
- **bcrypt:** Modern en zwaar voor computers om te berekenen.
- **scrypt:** Nog zwaarder dan bcrypt.
- **Argon2:** Zeer modern en vaak de beste keuze.

Algoritmes zoals deze **kunnen meerdere keren worden uitgevoerd (iteraties)** om de berekeningstijd te verhogen.\
Dit is de **"cost factor"**.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Deze wachtwoorden hashing algoritmes kunnen ook **"salting"** gebruiken.\
**Salting** is het **toevoegen van data aan het wachtwoord** voordat het gehasht wordt.

```
    ┌────────────┐   ┌──────┐    ┌──────────────┐    ┌──────┐ 
    │ Wachtwoord │ + │ Salt │ -> │ Hash functie │ -> │ Hash │
    └──────┬─────┘   └──┬───┘    └──────┬───────┘    └──┬───┘
           │            │               │               │
           ╰─╮          ╰─────╮         ╰──────╮        ╰────────────╮
             ▼                ▼                ▼                     ▼
    ┌────────┴────────┐   ┌───┴────┐    ┌──────┴───────┐    ┌────────┴─────────┐
    │ "Wachtwoord123" │ + │ XyZ!@# │ -> │ Hash functie │ -> │  a1b2c3d4e5f6... │
    └─────────────────┘   └────────┘    └──────────────┘    └──────────────────┘
```

Als **resultaat van het wachtwoord en de salt** krijgen we de **hash "a1b2c3d4e5f6..."**.

Stel dat een **aanvaller de database met hashes steelt** en probeert een **brute-force aanval zonder salt** uit te voeren:

```
    ┌────────────┐    ┌──────────────┐    ┌──────┐ 
    │ Wachtwoord │ -> │ Hash functie │ -> │ Hash │
    └──────┬─────┘    └──────┬───────┘    └──┬───┘
           │                 │               │
           ╰─╮               ╰────╮          ╰──────────╮
             ▼                    ▼                     ▼
    ┌────────┴────────┐    ┌──────┴───────┐    ┌────────┴─────────┐
    │ "Wachtwoord123" │ -> │ Hash functie │ -> │  g7h8i9j0k1l2... │
    └─────────────────┘    └──────────────┘    └──────────────────┘
```

De aanvaller heeft het **juiste wachtwoord "Wachtwoord123"**, maar **weet dat niet** want de **hash komt niet overeen vanwege de salt**.

### Voorbeeld van bcrypt hash

Een bcrypt hash ziet er zo uit:

```
$2a$12$R9h/cIPz0gi.URNNX3kh2OPST9/PgBkqquzi.Ss7KIUgO2t0jWMUW
 ┣┛ ┣┛ ┣━━━━━━━━━━━━━━━━━━━━┛┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
 │  │  │                     ╰────╮
 │  │  ╰───────────────────╮    De hash.
 │  ╰────────────╮       De salt.
 │        Aantal iteraties
 ╰─╮      (cost factor).  
Het ID van              
het algoritme            
(bcrypt).
```

## Hashing aanvallen

<tabs>
<tab title="Brute-force">
<p>Een <control>brute-force</control> aanval is wanneer een aanvaller <control>alle mogelijke combinaties probeert</control>.</p>
<p>Om dit tegen te gaan kan je een <control>goed hashing algoritme</control> gebruiken en <control>complexe wachtwoorden forceren</control>.</p>
</tab>
<tab title="Dictionary">
<p>Een <control>dictionary</control> aanval maakt gebruikt van een <control>lijst van wachtwoorden</control> die worden gehasht en vergeleken.</p>
<p>Werkt heel goed als het wachtwoord in de lijst staat, maar <control>werkt niet als die er niet in staat</control>.</p>
<p>Met salting werkt dit niet.</p>
</tab>
<tab title="Rainbow table">
<p>Een <control>rainbow table</control> is een <control>vooraf berekende lijst van hashes en het toebehorende wachtwoord</control> voor veelvoorkomende wachtwoorden.</p>
<p>Zo moet de aanvaller <control>niet al die wachtwoorden opnieuw hashen</control> waardoor veel tijd wordt gewonnen.</p>
<p>Als je salting gebruikt werkt het niet.</p>
</tab>
<tab title="Collision">
<p>Een aanvaller kan proberen <control>data aan te passen</control> en <control>dezelfde hash als resultaat te behouden</control>.</p>
<p>Door moderne algoritmes te gebruiken is dit veel moeilijker.</p>
</tab>
</tabs>