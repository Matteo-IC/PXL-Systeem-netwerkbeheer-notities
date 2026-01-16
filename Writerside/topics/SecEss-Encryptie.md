# Encryptie

**Encryptie** is het proces van het **omzetten** van **leesbare data** (plaintext) **naar** een **onleesbare data** (ciphertext).

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Plain text:** De leesbare data, voor encryptie.\
**Cipher text:** De onleesbare data, na encryptie.\
**Algorithm:** De wiskundige formule achter de encryptie.\
**Key:** Een geheime waarde die gebruikt wordt door het algoritme om de data te versleutelen of ontsleutelen.\
**Decryptie:** Het proces van het omzetten van ciphertext terug naar plaintext.

## Encryptie vs Hashing vs Encoding

<table>
    <tr>
        <td><control>Encryptie</control></td>
        <td>Hashing</td>
        <td>Encoding</td>
    </tr>
    <tr>
        <td><control>Omkeerbaar (met sleutel)</control></td>
        <td>Onomkeerbaar</td>
        <td>Omkeerbaar</td>
    </tr>
    <tr>
        <td><control>Variabele output lengte</control></td>
        <td>Vaste output lengte</td>
        <td>Variabele output lengte</td>
    </tr>
    <tr>
        <td><control>Gebruikt voor beschermen van data.</control></td>
        <td>Gebruikt voor data-integriteit, wachtwoord opslag.</td>
        <td>Gebruikt voor data in ander formaat te zetten.</td>
    </tr>
</table>

## Symmetrische encryptie

**Symmetrische encryptie** gebruikt **één enkele sleutel** voor zowel **encryptie** als **decryptie**.

De **zender en ontvanger** moeten dus **beide dezelfde sleutel** hebben.\
Symmetrische encryptie is **efficient**, maar het is **moeilijk** om de sleutel **veilig te delen**.

Het meest gebruikte symmetrische algoritme is **AES (Advanced Encryption Standard)**.

### Voorbeeld van symmetrische encryptie

Stel dat Alice een bericht naar Bob wil sturen.

```
    ┌──────────────┐
    │ Alice's      │
    │ Bericht      │
    └──────┬───────┘
           │
           │ Alice gebruikt de symmetrische sleutel om te encrypteren.
           ▼
    ┌──────────────┐
    │ Encryptie    │
    │ (met sleutel)│
    └──────┬───────┘
           │
           │ Het versleutelde bericht en sleutel worden naar Bob gestuurd.
           ▼
    ┌──────────────┐
    │ Bob ontvangt │
    │ Ciphertext   │
    └──────┬───────┘
           │
           │ Bob gebruikt dezelfde sleutel om het bericht te decrypteren.
           ▼
    ┌──────────────┐
    │ Decryptie    │
    │ (met sleutel)│
    └──────┬───────┘
           │
           │
           ▼
    Bob leest het originele bericht van Alice.
```

Maar als het versturen van de sleutel niet veilig gebeurt kan een derde partij de sleutel onderscheppen en het bericht lezen.

## Asymmetrische encryptie

**Asymmetrische encryptie** gebruikt **twee verschillende sleutels**: een **publieke sleutel** voor **encryptie** en een **privésleutel** voor **decryptie**.

Elke zender en ontvanger heeft een **publieke en privésleutel**.\
De publieke sleutel kan **vrij gedeeld worden**, terwijl de privésleutel **geheim blijft**.

**Asymmetrische encryptie** is **trager dan symmetrische encryptie**, maar het lost het probleem van sleuteluitwisseling op.

De meest gebruikte asymmetrische algoritmes zijn **RSA (Rivest-Shamir-Adleman) & ECDHE (Elliptic Curve Diffie-Hellman Ephemeral)**.

### Voorbeeld van asymmetrische encryptie (RSA)

Stel dat Alice een bericht naar Bob wil sturen.

```
    ┌──────────────┐
    │ Alice's      │
    │ Bericht      │
    └──────┬───────┘
           │
           │ Alice gebruikt Bob's publieke sleutel om te encrypteren.
           ▼
    ┌──────────────┐
    │ Encryptie    │
    │ (met Bob's   │
    │ publieke     │
    │ sleutel)     │
    └──────┬───────┘
           │
           │ Het versleutelde bericht wordt naar Bob gestuurd.
           ▼
    ┌──────────────┐
    │ Bob ontvangt │
    │ Ciphertext   │
    └──────┬───────┘
           │
           │ Bob gebruikt zijn privésleutel om het bericht te decrypteren.
           ▼
    ┌──────────────┐
    │ Decryptie    │
    │ (met Bob's   │
    │ privésleutel)│
    └──────┬───────┘
           │
           │
           ▼
    Bob leest het originele bericht van Alice.
```

Zo is het versturen van de sleutel veilig, de publieke sleutel kan vrij gedeeld worden omdat alleen Bob met zijn privésleutel het bericht kan decrypteren.

Het enige nadeel is dat asymmetrische encryptie minder efficiënt is dan symmetrische encryptie.

## Beide tegelijk

In de praktijk worden **symmetrische en asymmetrische encryptie vaak samen gebruikt**.

Bijvoorbeeld, bij het opzetten van een beveiligde verbinding (zoals HTTPS) wordt **asymmetrische encryptie gebruikt om een symmetrische sleutel veilig uit te wisselen**.\
Vervolgens wordt symmetrische encryptie gebruikt vanwege de hogere snelheid.

### Tegelijk - RSA

```
    ┌──────────────┐
    │ Client       │
    └──────┬───────┘
           │
           │ Client vraagt om een beveiligde verbinding.
           ▼
    ┌──────────────┐
    │ Server       │
    └──────┬───────┘
           │
           │ Server stuurt zijn publieke sleutel naar de client.
           ▼
    ┌──────────────┐
    │ Client       │
    └──────┬───────┘
           │ Client genereert een pre-master secret en
           │ encrypteert deze met de server's publieke sleutel.
           ▼
    ┌──────────────┐
    │ Server       │
    └──────┬───────┘
           │ Server decrypteert de pre-master secret
           │ met zijn privésleutel.
           ▼
    ┌──────────────┐
    │ Client       │
    │ Server       │
    └──────┬───────┘
           │ Beide partijen genereren de symmetrische sleutel
           │ uit de pre-master secret.
           ▼
    Beveiligde verbinding is opgezet met 
    symmetrische encryptie voor verdere communicatie.
```




### Tegelijk - ECDHE

**ECDHE (Elliptic Curve Diffie-Hellman Ephemeral)** is een moderne variant van Diffie-Hellman.

Het maakt gebruik van **tijdelijke sleutels** en **elliptische krommen** voor verbeterde beveiliging en efficiëntie.\
Daarom wordt het gebruikt in bijvoorbeeld TLS 1.3, wat de nieuwste en aanbevolen versie van TLS is.

```
    ┌──────────────┐
    │ Client       │
    └──────┬───────┘
           │ Client genereert een tijdelijke privé en publieke sleutel.
           │ Stuurt de publieke sleutel naar de server.
           ▼
    ┌──────────────┐
    │ Server       │
    └──────┬───────┘
           │ Server genereert ook een tijdelijke publieke & privé sleutel
           │ en stuurt de publieke sleutel naar de client.
           ▼
    ┌──────────────┐
    │ Client       │
    │ Server       │
    └──────┬───────┘
           │ Beide partijen gebruiken elkaars publieke sleutel
           │ en hun eigen privésleutel om allebei een symmetrische
           │ sleutel te genereren die door wiskunde hetzelfde is.
           ▼
    De tijdelijke sleutels die gebruikt zijn worden verwijderd.
    De symmetrische sleutel wordt gebruikt voor verdere communicatie.
    
    Bij iedere nieuwe sessie wordt dit opnieuw gedaan,
    zo kunnen derde partijen geen oude sessies ontcijferen.
```

## Toepassingen

### Digitale handtekening

Een **digitale handtekening** wordt gebruikt om de **authenticiteit en integriteit** van data te bewijzen.

1. De zender maakt een hash van de data.
2. De zender encrypteert de hash met zijn privésleutel, dit is de digitale handtekening.
3. De ontvanger ontvangt de originele data en de digitale handtekening.
4. De ontvanger maakt een hash van de ontvangen originele data.
5. De ontvanger decrypteert de digitale handtekening met de publieke sleutel van de zender.
6. De ontvanger vergelijkt de gedecrypteerde digitale handtekening (hash) met de zelfgemaakte hash.
7. Als de 2 hashes overeenkomen is de data authentiek en intact.

### Digitaal certificaat

Een **digitaal certificaat** wordt gebruikt om de **identiteit van een entiteit** (website, server...) te **verifiëren**.\
De identiteit wordt bevestigd door een vertrouwde derde partij, een **Certificate Authority (CA)**.

**Een digitaal certificaat bevat:**
- De **publieke sleutel** van de entiteit
- **Informatie over de entiteit** (naam, domein...)
- Informatie over de CA
- Geldigheidsperiode
- Digitale handtekening van de CA
- Andere metadata

Digitale certificaten volgen het **X.509-standaard**.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**PKI (Public Key Infrastructure):** Het systeem dat digitale certificaten beheert, uitgeeft en intrekt.

Dit bestaat uit:
- **Root CA's:** De hoogste vertrouwde autoriteiten die certificaten uitdelen aan Intermediate CA's.
- **Intermediate CA's:** Delen certificaten uit aan eindgebruikers of servers.
- **Digitale certificaten:** Bevestigen de identiteit van entiteiten en bevatten hun publieke sleutels.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Hoe een website een digitaal certificaat krijgt:**
1. De website-eigenaar genereert een **publieke en privésleutel**.
2. De eigenaar maakt een **Certificate Signing Request (CSR)** met de publieke sleutel en informatie over de website.
3. De CSR wordt naar een **Certificate Authority (CA)** gestuurd.
4. De CA **verifieert de informatie** en maakt een digitaal certificaat.
5. De CA **ondertekent het certificaat** door het te hashen en dat te encrypteren met zijn privésleutel.
6. De website-eigenaar **ontvangt het digitale certificaat** en installeert het op de webserver.

### SSH authenticatie

Hoe SSH asymmetrische encryptie gebruikt voor authenticatie:
1. De gebruiker genereert een **publieke en privésleutel**.
2. De gebruiker **plaatst de publieke sleutel** op de server.
3. De gebruiker probeert te **verbinden**, de server checkt of de publieke sleutel overeenkomt met een opgeslagen sleutel.
4. De server encrypteert data met de publieke sleutel van de gebruiker en stuurt deze terug.
5. Als de gebruiker de data kan decrypteren met zijn privésleutel, weet de server dat de gebruiker correct is.
