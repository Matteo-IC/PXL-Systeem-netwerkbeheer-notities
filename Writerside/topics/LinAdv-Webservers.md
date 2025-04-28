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


## Oefeningen

**1.
Je creëert 2 virtuele hosts die luisteren op de poorten 41347 en 1321. De server heeft als naam `<jevoornaam>.local`.
Geef aan hoe je dit gedaan hebt (commando’s / aanpassingen bestanden). De website die draait op poort 41347 geef je als
inhoud je voornaam. De website die draait op poort 1321 geef je als inhoud je achternaam. Je dient uiteraard ook je
resultaat te staven met screenshots.**

```
$ sudo nano /etc/httpd/conf/httpd.conf
...
# available when the service starts.  See the httpd.service(8) man
# page for more information.
#
Listen 41347
Listen 1321
Listen 80

#
# Dynamic Shared Object (DSO) Support
...
$ sudo mkdir /var/www/html/matteo-41347
$ sudo mkdir /var/www/html/ic-1321
$ sudo nano /var/www/html/matteo-41347/index.html # Voeg "Matteo" toe
$ sudo nano /var/www/html/ic-1321/index.html # Voeg "IC" toe
$ sudo nano /etc/httpd/conf.d/matteo-41347.conf
<VirtualHost *:41347>
    ServerName matteo.local
    ServerAlias www.matteo.local
    DocumentRoot /var/www/html/matteo-41347
    DirectoryIndex index.html
    ServerAdmin admin@matteo.local
</VirtualHost>
$ sudo nano /etc/httpd/conf.d/ic-1321.conf
<VirtualHost *:1321>
    ServerName matteo.local
    ServerAlias www.matteo.local
    DocumentRoot /var/www/html/ic-1321
    DirectoryIndex index.html
    ServerAdmin admin@matteo.local
</VirtualHost>
$ sudo chown -R apache:apache /var/www/html/matteo-41347
$ sudo chown -R apache:apache /var/www/html/ic-1321
$ sudo chmod -R 755 /var/www/html/
$ sudo systemctl restart httpd
$ sudo firewall-cmd --permanent --add-port=41347/tcp
$ sudo firewall-cmd --permanent --add-port=1321/tcp
$ sudo firewall-cmd --reload
$ curl matteo.local:41347
$ curl matteo.local:1321
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2.
Creëer 2 virtual hosts die luisteren op een ander ip-address. Het ene IP-adres koppel je aan `<jevoornaam>.local` en de
andere koppel je aan `<jeachternaam>.local`. Je dient de ip-nummers in te stellen via de command line interface.
Als inhoud geef de website `<jevoornaam>.local` je eigen voornaam en de website `<jeachternaam>.local` je eigen achternaam.
Je dient uiteraard ook je resultaat te staven met screenshots.**

```
$ nmcli connection add type ethernet con-name web1 ifname ens160
$ nmcli connection modify web1 ipv4.addresses 10.10.10.101/24
$ nmcli connection add type ethernet con-name web2 ifname ens160
$ nmcli connection modify web2 ipv4.addresses 10.10.10.102/24
$ sudo nmcli connection up web1
$ sudo nmcli connection up web2
$ sudo mkdir /var/www/html/matteo-site
$ sudo mkdir /var/www/html/ic-site
$ sudo nano /var/www/html/matteo-site/index.html # Voeg "Matteo" toe
$ sudo nano /var/www/html/ic-site/index.html # Voeg "IC" toe
$ sudo nano /etc/httpd/conf.d/matteo.local.conf
<VirtualHost 10.10.10.101:80>
    ServerName matteo.local
    ServerAlias www.matteo.local
    DocumentRoot /var/www/html/matteo-site
    DirectoryIndex index.html
    ServerAdmin admin@matteo.local
</VirtualHost>
$ sudo nano /etc/httpd/conf.d/ic.local.conf
<VirtualHost 10.10.10.102:80>
    ServerName ic.local
    ServerAlias www.ic.local
    DocumentRoot /var/www/html/ic-site
    DirectoryIndex index.html
    ServerAdmin admin@ic.local
</VirtualHost>
$ sudo systemctl restart httpd
$ curl matteo.local # Voeg gewoon aan hosts file toe als het niet werkt /etc/hosts
$ curl ic.local
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3.
Gebruik de websites uit de vorige opdracht, maar zorg dat je naar `<jeachternaam>.local` kan gaan vanuit 
`<jevoornaam>.local`. Je moet er ook voor zorgen dat er een login wordt gevraagd als je naar `<jeachternaam>.local` wil 
gaan. Gebruik als naam `<jevoornaam>` en als wachtwoord pxl.**

```
$ sudo nano /var/www/html/matteo-site/index.html
Matteo
<br>
<a href="http://ic.local">ic.local</a>
$ sudo htpasswd -c /etc/httpd/conf/.htpasswd Matteo
pxl
$ sudo nano /etc/httpd/conf.d/ic.local.conf
<VirtualHost 10.10.10.102:80>
    ...

    <Directory "/var/www/html/ic-site">
        AuthType Basic
        AuthName "Restricted Access"
        AuthUserFile /etc/httpd/conf/.htpasswd
        Require user Matteo
    </Directory>
</VirtualHost>
$ sudo systemctl restart httpd
$ sudo chmod 640 /etc/httpd/conf/.htpasswd
$ sudo chown root:apache /etc/httpd/conf/.htpasswd
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**4.
Zorg dat de vorige opdracht werkt via https door zelf een SSL certificaat te maken en deze in te stellen.**

```
$ sudo dnf install mod_ssl openssl -y
$ sudo mkdir /etc/httpd/ssl
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/httpd/ssl/matteo.local.key \
    -out /etc/httpd/ssl/matteo.local.crt \
    -subj "/C=BE/ST=Limburg/L=Hasselt/O=PXL/CN=matteo.local"
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/httpd/ssl/ic.local.key \
    -out /etc/httpd/ssl/ic.local.crt \
    -subj "/C=BE/ST=Limburg/L=Hasselt/O=PXL/CN=ic.local"
    
$ sudo chmod 600 /etc/httpd/ssl/*.key
$ sudo chmod 644 /etc/httpd/ssl/*.crt

$ sudo nano /etc/httpd/conf.d/matteo.local.conf
<VirtualHost 10.10.10.101:80>
    ServerName matteo.local
    ServerAlias www.matteo.local
    Redirect permanent / https://matteo.local/
</VirtualHost>

<VirtualHost 10.10.10.101:443>
    ServerName matteo.local
    ServerAlias www.matteo.local
    DocumentRoot /var/www/html/matteo-site

    SSLEngine on
    SSLCertificateFile /etc/httpd/ssl/matteo.local.crt
    SSLCertificateKeyFile /etc/httpd/ssl/matteo.local.key
</VirtualHost>

$ sudo nano /etc/httpd/conf.d/ic.local.conf
<VirtualHost 10.10.10.102:80>
    ServerName ic.local
    ServerAlias www.ic.local
    Redirect permanent / https://ic.local/
</VirtualHost>

<VirtualHost 10.10.10.102:443>
    ServerName ic.local
    ServerAlias www.ic.local
    DocumentRoot /var/www/html/ic-site

    SSLEngine on
    SSLCertificateFile /etc/httpd/ssl/ic.local.crt
    SSLCertificateKeyFile /etc/httpd/ssl/ic.local.key

    <Directory "/var/www/html/ic-site">
        AuthType Basic
        AuthName "Restricted Access"
        AuthUserFile /etc/httpd/conf/.htpasswd
        Require user Matteo
    </Directory>
</VirtualHost>

# firewall rules toevoegen als het niet werkt
$ sudo firewall-cmd --permanent --add-service=https
$ sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" destination address="10.10.10.101" port port="443" protocol="tcp" accept'
$ sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" destination address="10.10.10.102" port port="443" protocol="tcp" accept'
$ sudo firewall-cmd --reload
```