# Network File System

## Oefeningen

**1. Maak 2 directories (/<je_voornaam>/ en /<je_achternaam>/) aan op de server. Deel /<je_voornaam> readonly en
/<je_achternaam> lezen/schrijven. Test dit uit tussen 2 virtuele machines (nasbox en client<je_inititialen>). 
De mounting points op de clients zijn respectievelijk /lezen en /lezenenschrijven. Test dit uit met het commando mount
op de client en toon het resultaat.**
```
$ sudo mkdir /matteo
$ sudo mkdir /idelercautaert
$ sudo nano /etc/exports
(...)
/matteo 10.10.10.0/255.255.255.0(ro)
/idelercautaert 10.10.10.0/255.255.255.0(rw,async)
$ sudo exportfs -a -r -v
$ sudo firewall-cmd --permanent --add-service=nfs
$ sudo firewall-cmd --permanent --add-service=rpc-bind
$ sudo firewall-cmd --permanent --add-service=mountd
$ sudo firewall-cmd --reload
$ sudo setsebool -P use_nfs_home_dirs on
$ sudo setsebool -P nfs_export_all_ro on
$ sudo setsebool -P nfs_export_all_rw on
$ sudo semanage fcontext -a -t public_content_rw_t "/matteo(/.*)?"
$ sudo semanage fcontext -a -t public_content_rw_t "/idelercautaert(/.*)?"
$ sudo restorecon -F -R -v /matteo
$ sudo restorecon -F -R -v /idelercautaert
$ sudo chmod a+w /idelercautaert

# Op de client:
$ sudo mkdir /lezen
$ sudo mkdir /lezenenschrijven
$ sudo mount 10.10.10.1:/matteo /lezen
$ sudo mount 10.10.10.1:/idelercautaert /lezenenschrijven
$ cd /net/10.10.10.1/matteo
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2. Pas bovenstaande oefening aan zodanig dat er gemount wordt via fstab. Maak een screenshot van je fstab-file.
Er moet niet automatisch gemount worden. Test het mounten ook uit.**
```
$ sudo nano /etc/fstab
...
10.10.10.1:/matteo /lezen nfs rsize=8192,wsize=8192 0 0
10.10.10.1:/idelercautaert /lezenenschrijven nfs rsize=8192,wsize=8192 0 0
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3. We gaan nu het mounten automatiseren via autofs. Geef alle commando’s, ook om dit uit te testen.**
```
$ sudo umount /lezen
$ sudo umount /lezenenschrijven
$ sudo nano /etc/auto.master
/- /etc/auto.direct --timeout=60
$ sudo nano /etc/auto.direct
/lezen -ro,soft,intr,vers=4 10.10.10.1:/matteo
/lezenenschrijven -rw,soft,intr,vers=4 10.10.10.1:/idelercautaert
$ sudo systemctl reload autofs
$ ls /lezen
$ ls /lezenenschrijven
$ mount | grep auto
```
