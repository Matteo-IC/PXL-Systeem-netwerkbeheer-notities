# Module 1

## Introductie

Een **netwerk** is een **verzameling van computers** en andere apparaten die **met elkaar verbonden** zijn.\
Alle **apparaten die verbonden** zijn **met een netwerk** en **deelnemen aan communicatie** worden **hosts genoemd**.

Hosts kunnen ook end devices of clients genoemd worden.\
**End device:** De **bron of de bestemming** van **communicatie**.\
**Client:** Het **apparaat of de software** die **diensten van een server aanvraagt**.

Om te kunnen **communiceren met andere hosts** hebben ze een **manier van identificatie nodig**.\
Een **IP-adres** is een van de **identificatiemethoden**.

```
      IP-adres 1       IP-adres(sen)      IP-adres 2
      ┌────────┐       ┌──────────┐       ┌────────┐
      │ Client ├───────┤ Internet ├───────┤ Server │
      └────────┘       └──────────┘       └────────┘
          ↓                  ↓                 ↓
      End device       Andere hosts       End device
      Host             tussen de client   Host
      Browser          en de server       Website
```

Het "Internet" zoals hierboven getoond is een **aantal tussenliggende hosts die de client en de server verbinden**.\
Deze hosts zijn **bijvoorbeeld routers**.

De **mogelijke functie(s)** van deze tussenliggende hosts:
- **Verkeer doorsturen**
- **Signalen versterken**
- **Verkeer filteren voor veiligheid**
- **Routes bepalen**
- **Andere apparaten verwittigen van problemen**

## Netwerk hardware

### Verbinding

**Communicatie** tussen hosts **kan via verschillende soorten media**.

- **Kabels**:
  - **Koper kabels**
    - Data wordt verstuurd via **elektrische signalen**.
  - **Glasvezel kabels**
    - Data wordt verstuurd via **lichtsignalen**.
- **Draadloos**:
  - Data wordt verstuurd via **elektromagnetische golven**.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Apparaten

Een paar **belangrijke apparaten**:

- **Router**: Verbindt verschillende **netwerken** met elkaar.
- **Switch**: Verbindt verschillende **apparaten** binnen hetzelfde netwerk.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Componenten

- **NIC (Network Interface Card)**: Een **fysiek deel van een apparaat** dat **verbinding maakt met een netwerk**.
- **Fysieke poort**: Een **fysieke connector** op een netwerkapparaat **waar het transport media** (kabel) **in gaat**.

## Netwerk types

Om een **overzicht** te **krijgen van** een **netwerk** moet je kunnen **zien wat met wat verbonden is en waar het is**.\
Dit kan je doen door een **netwerk diagram / topologie** te maken.

```
Kleine basis logische topologie: 
             ┌──────────────┐
             │   Internet   │
             └──────┬───────┘
                    │
               ┌────┴────┐
               │ Router  │
               └────┬────┘
                    │
                ┌───┴───┐        ┌─────────┐
                │Switch ├────────┤ Printer │
               ╭└───────┘╮       └─────────┘
               │         │
          ┌────┴────┐┌───┴────┐
          │ Desktop ││ Server │
          └─────────┘└────────┘
```

Een **netwerk topologie** kan **fysiek** of **logisch** zijn.
- **Fysieke topologie**: **Waar** de **apparaten fysiek zijn**.
- **Logische topologie**: **Hoe** de **data stroomt** binnen het netwerk.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Een **netwerk topologie** moet bevatten:
- **Welke apparaten** er zijn.
- **Hoe de apparaten verbonden** zijn.
  - Welke **media** er gebruikt wordt.
  - Welke **poorten** er gebruikt worden.
- **Waar de apparaten zich bevinden**.
  - Logisch of fysiek.
- **Identificatie van de apparaten.**
  - Bijvoorbeeld: IP-adres, hostnaam, apparaat model enz.

