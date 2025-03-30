# Webservers

De student(e):
- Weet waar de configuratie en HTML bestanden van Apache mogen/kunnen staan.
- kan een basis HTML-file voor een website aanmaken met een titel en inhoud.
- Kan meerdere Apache websites tegelijk runnen.
- Kan een SSL certificaat maken en toevoegen aan een website van Apache.
- Kan een beveiligde pagina maken op een website van Apache.
- Kan de firewall (en later ook SELinux) instellen voor Apache.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Een **webserver is** een **server die webpagina's stuurt** naar clients die een request sturen naar de server.

## Apache

**Apache** is een **open-source webserver** die veel gebruikt wordt op het internet.

**Apache installeren**:
```
$ sudo dnf install -y httpd
```

**Apache starten** en **activeren**:
```
$ sudo systemctl start httpd
$ sudo systemctl enable httpd
```
