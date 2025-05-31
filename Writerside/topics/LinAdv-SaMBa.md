# SaMBa

SaMBa is een open-source implementatie van het SMB/CIFS-protocol.

**SMB/CIFS:** Server Message Block/Common Internet File System, protocollen die gebruikt worden voor bestanden en printers
te delen over een netwerk.

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

## Oefeningen

**1. Zorg ervoor dat je samba-server enkel toegankelijk is vanop het systemen met ip-adress 10.10.10.10.
Toegang vanop andere systemen moet geweigerd worden. Geef aan wat je aanpast aan smb.conf en test het uit.
Verander erna het ip van je 2de machine naar 10.10.10.15 en test het opnieuw uit.**
```
$ sudo nano /etc/samba/smb.conf
...
[global]
hosts allow = 10.10.10.10
...
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2. Maak een gedeelde map genaamd “share1” aan op je Linux server. De share wordt bewaard op /srv/share1. 
Een gebruiker met als naam &lt;jevoornaam&gt; met een wachtwoord moet in staat zijn vanop een client bestanden van de share af
te halen en bestanden op de share te zetten. Geen enkele andere gebruiker mag toegang hebben tot de share. 
Toon je smb.conf en neem van de client waarbij je aantoont dat je iets op de server kan zetten/afhalen een screenshot.**
```
$ sudo useradd -m matteo
$ sudo passwd matteo
$ sudo smbpasswd -a matteo
$ sudo mkdir /srv/share1
$ sudo chown matteo:matteo /srv/share1
$ sudo chmod 700 /srv/share1
$ sudo setsebool -P samba_export_all_rw on
$ sudo semanage fcontext -a -t samba_share_t "/srv/share1(/.*)?"
$ sudo restorecon -R /srv/share1
$ sudo nano /etc/samba/smb.conf
...
[share1]
    comment = Share voor matteo
    path = /srv/share1
    browseable = yes
    writable = yes
    guest ok = no
    valid users = matteo
    admin users = matteo
    write list = matteo
    create mask = 0600
    directory mask = 0700
    force user = matteo
    force group = matteo
    hide unreadable = yes
$ sudo testparm
$ sudo systemctl restart smb nmb
$ sudo systemctl enable smb nmb
$ sudo firewall-cmd --permanent --add-service=samba
$ sudo firewall-cmd --reload
$ smbclient //nasbox/share1 -U matteo
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3. Zorg ervoor dat alle toegangspogingen tot samba gelogd worden. De toegangspogingen van verschillende clients moet 
in verschillende bestanden terecht komen. De logbestanden mogen niet groter worden dan 100MB. Onderzoek tevens de
logfiles: welke informatie vind je erin terug? Geef aan wat je aanpast in smb.conf.**
```
$ sudo nano /etc/samba/smb.conf
...
[global]
   log file = /var/log/samba/%m.log
   max log size = 100000
   syslog = 0
   log level = 1
$ sudo systemctl restart smbd
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**4. Maak een Samba share “share2” waar niemand lees en schrijf-toegang toe heeft. Gebruikers van de groep groep1 hebben
enkel leestoegang. Maak 2 gebruikers (&lt;jevoornaam&gt; en &lt;jeachternaam&gt;) aan en maak ze lid van groep1. Andere gebruikers
hebben géén toegang. &lt;jevoornaam&gt;, &lt;jeachternaam&gt; en student kunnen gebruik maken van een homedirectory. Test het uit
(zowel op een Linux- als op een Windows-client in VMware). Maak ook screenshots van je resultaat.**
```
$ sudo groupadd groep1
$ sudo useradd -m -G groep1 matteo
$ sudo useradd -m -G groep1 ideler
$ sudo passwd matteo
$ sudo passwd ideler
$ sudo smbpasswd -a matteo
$ sudo smbpasswd -a ideler
$ sudo smbpasswd -a student
$ sudo mkdir /srv/share2
$ sudo chown root:groep1 /srv/share2
$ sudo chmod 750 /srv/share2
$ sudo setsebool -P samba_export_all_ro on
$ sudo semanage fcontext -a -t samba_share_t "/srv/share2(/.*)?"
$ sudo restorecon -R /srv/share2
$ sudo nano /etc/samba/smb.conf
...
[share2]
    comment = Share2 - alleen leestoegang voor groep1
    path = /srv/share2
    browseable = yes
    writable = no
    guest ok = no
    valid users = @groep1
    read list = @groep1
    create mask = 0644
    directory mask = 0755
    force group = groep1

[homes]
    comment = Home Directories
    browseable = no
    writable = yes
    valid users = %S
    create mask = 0664
    directory mask = 0775
    force create mode = 0664
    force directory mode = 0775
$ sudo testparm
$ sudo systemctl restart smb nmb
$ sudo systemctl enable smb nmb
$ sudo firewall-cmd --permanent --add-service=samba
$ sudo firewall-cmd --reload
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**5. Pas oefening 4 aan zodat je vanaf je Windows op je computer zelf (de Windows waarop je VMware hebt geïnstalleerd) 
toegang krijgt tot de shares. Maak ook een screenshot van je resultaat.**

Network adapter van de VM moet op Bridged staan.
