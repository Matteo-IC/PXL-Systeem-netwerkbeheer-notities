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

**Standaard zoekt** Apache naar website bestanden **in de map** `/var/www/html/`.

Om **meerdere websites op hetzelfde systeem** te kunnen draaien, moet je een **configuratie bestand per website** maken.\
Dit **doe je door** een **configuratiebestand** aan te **maken** in de map `/etc/httpd/conf.d/` met de **extensie** `.conf`.

### Voorbeeld

*2 simpele websites aanmaken op hetzelfde systeem.*

**Maak** het **configuratiebestand** aan voor de 1ste website:
```
$ sudo nano /etc/httpd/conf.d/website1.conf
<VirtualHost *:80>
    ServerAdmin admin@website1.mic.lan
    ServerName www.website1.mic.lan
    ServerAlias *.website1.mic.lan
    DocumentRoot /var/www/html/website1/
    DirectoryIndex index.html
</VirtualHost>
```

**Maak** de **map** aan voor de website & de **index.html**:
```
$ sudo mkdir /var/www/html/website1
$ sudo nano /var/www/html/website1/index.html
<html>
    <head>
        <title>website 1</title>
    </head>
    <body>
        <h1>website 1</h1>
    </body>
</html>
```

**Maak** het **configuratiebestand** aan voor de 2de website:
```
$ sudo nano /etc/httpd/conf.d/website2.conf
<VirtualHost *:80>
    ServerAdmin admin@website2.mic.lan
    ServerName www.website2.mic.lan
    ServerAlias *.website2.mic.lan
    DocumentRoot /var/www/html/website2/
    DirectoryIndex index.html
</VirtualHost>
```

**Maak** de **map** aan voor de website & de **index.html**:
```
$ sudo mkdir /var/www/html/website2
$ sudo nano /var/www/html/website2/index.html
<html>
    <head>
        <title>website 2</title>
    </head>
    <body>
        <h1>website 2</h1>
    </body>
</html>
```

**Pas** de **DNS** aan:
```
$ sudo nano /etc/named/mic.lan.db
...
website1      IN	A	    10.10.10.1
www.website1  IN	CNAME   website1.mic.lan.
website2      IN    A       10.10.10.1
www.website2  IN    CNAME   website2.mic.lan.
```

**Herstart** de **DNS**:
```
$ sudo systemctl restart named
```

**Check** of de namen **gevonden worden**.
```
$ nslookup website1.mic.lan
$ ...
```

**Herstart Apache.**
```
$ sudo systemctl restart httpd
```

### Extra uitleg



