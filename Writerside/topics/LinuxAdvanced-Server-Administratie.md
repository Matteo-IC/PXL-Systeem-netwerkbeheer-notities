# Server Administratie

De student(e):
- Kan de 5 stappen om een server op te zetten benoemen en gebruiken
- Kent enkele services
- Kan een veilige communicatie starten met en zonder wachtwoord naar zijn/haar server

**Daemons:** Achtergrondprocessen die zonder interactie van een gebruiker werken.

## Stappen voor server administratie

1. Installeer de server
2. Configureer de server
3. Start de server
4. Beveilig de server
5. Monitor de server

### Installatie

In Red Hat een package installeren:
```
[student@ServerMIC ~]$ sudo dnf install httpd
```

### Configuratie

Configuratiebestanden (.conf) zijn meestal in de map `/etc`.

### Starten

**Servers zijn daemon processen** en moeten (meestal) geconfigureerd worden om op te **starten als het systeem start**.

**Start** de daemon:
```
[student@ServerMIC ~]$ sudo systemctl start httpd
```

**Start** de daemon **wanneer het systeem start**:
```
[student@ServerMIC ~]$ sudo systemctl enable httpd
```

Check de **status** van de daemon:
```
[student@ServerMIC ~]$ sudo systemctl status httpd
```

**Poorten voor http openen:**
```
[student@ServerMIC ~]$ sudo firewall-cmd --permanent --add-service=http
[student@ServerMIC ~]$ sudo firewall-cmd --reload
```

Om **specifieke poorten** te openen:
```
[student@ServerMIC ~]$ sudo firewall-cmd --permanent --add-port=80/tcp
```
`/tcp` is het protocol dat toegelaten wordt, dit kan ook bv. `udp` zijn.

### Beveiligen

**De SSH-toegang tot het root account uitzetten verbetert de beveiliging.**
```
[student@ServerMIC ~]$ sudo nano /etc/ssh/sshd_config
```
Stel `PermitRootLogin` in op `no`.\
Herstart de SSH daemon:
```
[student@ServerMIC ~]$ sudo systemctl restart sshd
```

### Monitoren

Logboeken bekijken:
```
[student@ServerMIC ~]$ sudo tail -f /var/log/messages
```

Updaten:
```
[student@ServerMIC ~]$ sudo dnf update
```

## Veilige communicatie

### Symmetrische encryptie

1. Een geheime **sleutel** (wiskundige formule) wordt **van één apparaat naar een ander gestuurd**.
   - Dit is **niet geëncrypteerd** en dus **niet veilig** als enkel symmetrische encryptie wordt gebruikt.
2. Een **apparaat** gebruikt de geheime **sleutel** om het bericht te **encrypteren en stuurt het** dan.
3. De **ontvanger decrypteert** het bericht met de geheime sleutel.
   - Als de **sleutel onderschept** is kan **iedereen die de sleutel ook heeft het bericht decrypteren**.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Asymmetrische encryptie

1. Een apparaat heeft een **publieke en een privésleutel**.
   - Als de **publieke sleutel iets encrypteert** kan **alleen de privésleutel dit decrypteren**.
2. Apparaat 1 maakt connectie met apparaat 2 en wil iets sturen.
   - **Apparaat 1 vraagt** voor de **publieke sleutel** van **apparaat 2**.
3. **Apparaat 2 deelt** zijn **publieke sleutel** met apparaat 1.
4. **Apparaat 1 encrypteert** en stuurt het **bericht met de publieke sleutel van apparaat 2**.
5. **Apparaat 2 decrypteert het bericht met zijn privésleutel.**

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Tegelijk

1. **Apparaat 1 maakt** een willekeurige **symmetrische sleutel**.
2. **Apparaat 1 encrypteert de sleutel met** de **publieke sleutel van apparaat 2**.
3. **Apparaat 1 stuurt** deze geëncrypteerde **sleutel naar apparaat 2**.
4. **Apparaat 2 decrypteert** de **sleutel met** zijn **privésleutel**.
5. Ze **hebben nu allebei** veilig de **symmetrische sleutel**.
   - **Asymmetrisch is trager** dan symmetrisch.
   - Het **probleem met symmetrische** encryptie is **opgelost**.
   - **Toekomstige communicatie kan** nu **sneller** en veilig **via symmetrische encryptie**.
   - **Dit is hoe SSH werkt.**

