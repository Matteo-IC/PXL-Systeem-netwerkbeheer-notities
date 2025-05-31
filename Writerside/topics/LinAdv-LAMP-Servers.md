# LAMP Servers

De student(e):
- Kan een LAMP-server opzetten
- Kan het acroniem LAMP uitleggen en aanpassen

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

## Wat is LAMP?

**LAMP** is een **acroniem** dat staat voor **Linux, Apache, MySQL en PHP**. Dit zijn **software** die **samen een webserver** 
vormen.

## Oefeningen

**1.
We willen virtual hosting voor ELKE gebruiker op het systeem. Doe dit aan de hand van userdir.conf. Maak 2 gebruikers
met je voor- en achternaam bij en test het uit. Maak uiteraard de nodige screenshots om het te staven voor deze 2
gebruikers.**

```
$ sudo nano /etc/httpd/conf.d/userdir.conf
# UserDir: The directory under each user's home directory where they should
# place their web content.
#
UserDir public_html

# Control access to UserDir directories
<Directory "/home/*/public_html">
    AllowOverride All
    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
    Require all granted
</Directory>

$ sudo useradd -m matteo
$ sudo passwd matteo
$ sudo useradd -m ic
$ sudo passwd ic
$ sudo mkdir /home/matteo/public_html
$ sudo nano /home/matteo/public_html/index.html # Voeg tekst toe
$ sudo mkdir /home/ic/public_html
$ sudo nano /home/ic/public_html/index.html # Voeg tekst toe
$ sudo chown -R matteo:matteo /home/matteo/public_html
$ sudo chown -R ic:ic /home/ic/public_html
$ sudo chmod -R 755 /home/matteo/public_html
$ sudo chmod -R 755 /home/ic/public_html
$ sudo systemctl restart httpd
$ curl http://localhost/~matteo/
$ curl http://localhost/~ic/
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2.
Leg uit waarom er zowel symmetrische als asymmetrische encryptie gebruikt wordt bij communicatie via https?**

<a href="LinuxAdvanced-Server-Administratie.md" anchor="tegelijk">Hoe het gebeurt.</a>

Als alleen symmetrische encryptie wordt gebruikt kan de sleutel niet veilig gedeeld worden. Er wordt asymmetrische encryptie
gebruikt om de symmetrische sleutel te delen zodat het wel veilig is. Nu kan er veilig symmetrische encryptie gebruikt
worden wat veel sneller is.


<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3.
Installeer een website waarbij er op de startpagina (index.html) links staan naar Drupal, Joomla en Wordpress.
a. Toon je code van index.html en toon uiteraard je resultaat (analoog aan onderstaande: verander de voor- en achternaam
naar jouw eigen voor- en achternaam).**

```
$ sudo nano /var/www/html/index.html
<h1>Joomla, Drupal en Wordpress</h1>

<a href="/drupal/">Drupal</a>
<a href="/joomla/">Joomla</a>
<a href="/wordpress/">Wordpress</a>
</br>
Installed by Matteo Ideler Cautaert
```

**1. Installeer drupal in een subdirectory. Toon de code en het resultaat.**\
*Moet niet.*

**2. Installeer joomla in een subdirectory. Toon de code en het resultaat**
```
$ sudo systemctl start httpd mariadb
$ sudo systemctl enable httpd mariadb
$ sudo mysql_secure_installation
$ sudo mysql -u root -p
CREATE DATABASE joomla;
CREATE USER 'joomla'@'localhost' IDENTIFIED BY 'joomla_password';
GRANT ALL PRIVILEGES ON joomla.* TO 'joomla'@'localhost';
FLUSH PRIVILEGES;
EXIT;

$ sudo nano /etc/php.ini # Verander de volgende instellingen:
memory_limit = 256M
upload_max_filesize = 30M
post_max_size = 30M
max_execution_time = 30

$ wget https://downloads.joomla.org/cms/joomla5/5-3-0/Joomla_5-3-0-Stable-Full_Package.tar.gz
$ sudo tar -xzf Joomla_5-3-0-Stable-Full_Package.tar.gz -C /var/www/html/joomla
$ sudo chown -R apache:apache /var/www/html/joomla
$ sudo chmod -R 755 /var/www/html/joomla

$ sudo nano /etc/httpd/conf.d/joomla.conf
<VirtualHost *:80>
    DocumentRoot "/var/www/html/joomla"
    ServerName joomla.example.com
    <Directory "/var/www/html/joomla">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>

$ sudo apachectl configtest
$ sudo systemctl restart httpd
$ sudo firewall-cmd --permanent --add-service=http
$ sudo firewall-cmd --permanent --add-service=https
$ sudo firewall-cmd --reload

# Ga naar localhost en volg de installatie-instructies.
```

**3. Installeer Wordpress in een subdirectory. Toon de code en het resultaat.**
```
$ systemctl start mariadb
$ mysql_secure_installation # overal "y" invullen
$ systemctl enable mariadb
$ systemctl start httpd
$ systemctl enable httpd
$ mysql -u root -p
CREATE DATABASE wordpress;
CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'wordpress_password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'localhost';
FLUSH PRIVILEGES;
EXIT;

$ cd /tmp
$ wget https://wordpress.org/latest.tar.gz
$ sudo mkdir -p /var/www/html/wordpress
$ sudo tar -xzf latest.tar.gz -C /var/www/html/
$ sudo chown -R apache:apache /var/www/html/wordpress
$ sudo chmod -R 755 /var/www/html/wordpress
$ sudo nano /etc/httpd/conf.d/wordpress.conf
<VirtualHost *:80>
    DocumentRoot "/var/www/html/wordpress"
    ServerName wordpress.example.com
    <Directory "/var/www/html/wordpress">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>

$ sudo apachectl configtest
$ sudo systemctl restart httpd

# Ga naar localhost en volg de installatie-instructies.
```
