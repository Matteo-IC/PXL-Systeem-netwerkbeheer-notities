# Policies

Policies zijn **beperkingen en instellingen** die **worden toegepast op OU's**.

Er zijn **2 soorten policies**:
- **User Policies**
  - Policies die worden toegepast op **users die aanmelden** bij een domein.
  - Wordt **enkel op** de **gebruiker** toegepast.
  - **Maakt niet uit welke computer** gebruikt wordt.
  - Wachtwoorden, achtergrond, beperkingen op applicaties...
- **Computer Policies**
  - Policies die worden **toegepast op computers** binnen een domein.
  - **Maakt niet uit welke gebruiker** zich aanmeldt.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Een **GPO** (Group Policy Object) is een **object / container voor policies**. Deze worden gelinkt aan **OU's**.\
Een **GPO** wordt **toegepast** op de **OU** en **alle OU's daar onder** tenzij die expliciet is uitgesloten.

**Wanneer** een **gebruiker zich aanmeldt** bij een domein of wanneer **een computer wordt opgestart**,
**worden de GPO's toegepast**.

Er zijn **4 soorten GPO's** die worden toegepast in deze volgorde:
1. **Local GPO's**
2. **Site-linked GPO's**
3. **Domain-linked GPO's**
4. **OU-linked GPO's**

**Local Group Policy** is de **laagste prioriteit** en wordt **overschreven door de andere GPO's**.

Als je een **GPO maakt in een OU** wordt die GPO **opgeslagen in de map `Group Policy Objects`**.\
In de **OU waar je de GPO hebt gemaakt** wordt een **link gezet naar de GPO** in de map `Group Policy Objects`.
