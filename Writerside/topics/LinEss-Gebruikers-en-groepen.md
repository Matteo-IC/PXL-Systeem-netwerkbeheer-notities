# Gebruikers en groepen

Linux maakt gebruik van gebruikers en groepen.\
Je kan **zien wie ingelogd is** met het commando `who`.

**Alle gebruikers** zijn opgeslagen **in het bestand `/etc/passwd`**.
```
gebruiker@ubuntu:~$ head -1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

In dit bestand staan **velden, gescheiden door een dubbele punt**.
1. **Gebruikersnaam**
2. **Wachtwoord** (meestal een `x`, omdat het wachtwoord in `/etc/shadow` staat)
3. **Gebruikers-ID (UID)** (0 is de root-gebruiker)
4. **Groeps-ID (GID)** (0 is de root-groep)
5. **Volledige naam** (of een beschrijving)
6. **Home directory** (de map waar de gebruiker na inloggen komt)
7. **Shell** (de opdrachtregel die wordt gebruikt na inloggen)


