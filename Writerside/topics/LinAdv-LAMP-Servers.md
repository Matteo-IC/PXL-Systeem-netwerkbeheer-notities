# LAMP Servers

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
