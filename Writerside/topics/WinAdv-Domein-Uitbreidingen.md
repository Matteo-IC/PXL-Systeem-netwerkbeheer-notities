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

[//]: # (TODO: afmaken)
Een extra domain controller zorgt voor redundantie en load balancing.

## Multi master replication

