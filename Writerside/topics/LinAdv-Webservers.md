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

**Standaard zoekt** Apache naar website bestanden **in de map** `/var/www/html/`.\
Om **meerdere websites** te kunnen draaien, moet je de **configuratie aanpassen**.

Dit **doe je door** een **configuratiebestand** aan te **maken** in de map `/etc/httpd/conf.d/` met de **extensie** `.conf`.

### Voorbeeld

**Maak** een **configuratiebestand** aan voor de 1ste website:
```
$ sudo nano /etc/httpd/conf.d/website1.conf
<VirtualHost *:80>
    ServerAdmin webmaster@pxl.lan
    ServerName webserverXX.pxl.lan
    ServerAlias www.webserverXX.pxl.lan
    DocumentRoot /var/www/html/website1/
    DirectoryIndex index.php index.html index.htm
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

**Maak** een **configuratiebestand** aan voor de 2de website:
```
$ sudo nano /etc/httpd/conf.d/website2.conf
<VirtualHost *:80>
    ServerAdmin webmaster@pxl.lan
    ServerName webserver2XX.pxl.lan
    ServerAlias www.webserver2XX.pxl.lan
    DocumentRoot /var/www/html/website2/
    DirectoryIndex index.php index.html index.htm
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
$ sudo nano /etc/named/pxl.lan.db
...
webserverXX      IN	   A	   10.10.10.1
www.webserverXX  IN	   CNAME   webserverXX.pxl.lan.
webserver2XX     IN    A       10.10.10.1
www.webserver2XX IN    CNAME   webserver2XX.pxl.lan.
```

**Herstart** de **DNS**:
```
$ sudo systemctl restart named
```


