# Drive management

De student(e):
- Kan drives partitioneren met fdisk en gdisk
- Kan drives handmatig en automatisch mounten

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Als je een **OS installeert** wordt de **schijf gepartitioneerd**. Elke partitie is geformatteerd met een bepaald
bestandssysteem.

**Partities:** **Virtueel afgescheiden delen van een schijf**.\
**Bestandssysteem:** Een **manier om data te organiseren** op een schijf.\
**Mount locatie:** Een **locatie in het bestandssysteem** waar een **schijf aan gekoppeld** is.

*Swappartitie: Als er weinig RAM is, wordt niet gebruikte RAM tijdelijk opgeslagen in de swappartitie.*

In **Linux begint** alles vanuit de **root map `/`**.

## Partities

Via `lsblk` kan je **schijven, partities en mount locaties zien**:
```
[student@ServerMIC ~]$ lsblk
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda             8:0    0    8G  0 disk
...
```

Je kan met de `-o` optie de **kolommen kiezen** die je wilt zien:
```
[student@ServerMIC ~]$ sudo lsblk -o NAME,UUID
NAME          UUID
sda
└─sda1        47fec413-9ec7-4f32-baa9-9046c961a82f
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

In **`/etc/fstab`** staan **partities en schijven**. Elke regel bevat 6 dingen:
1. Een **ID** voor de partitie of het apparaat:
```
UUID=1234-5678  /home  ext4  defaults,noatime  0  2
^^^^^^^^^^^^^^
```
2. Waar de **mount locatie** is:
```
UUID=1234-5678  /mnt/data  ext4  defaults,noatime  0  2
                ^^^^^^^^^
```
3. **Bestandstype**:
```
UUID=1234-5678  /home  ext4  defaults,noatime  0  2
                       ^^^^
```
4. **Hoe het mount** (default, read & write, read only...):
```
UUID=1234-5678  /home  ext4  defaults  0  2
                             ^^^^^^^^
```
5. Is een **verouderd** deel, op 0 zetten:
```
UUID=1234-5678  /home  ext4  defaults,noatime  0  2
                                               ^
```
6. **Of en wanneer** Linux het bestandssysteem **moet checken voor fouten**:\
0 = Niet checken\
1 = Eerst checken (alleen voor root `/`)\
2 = Als tweede checken (voor andere schijven / bestandssystemen)
```
UUID=1234-5678  /home  ext4  defaults,noatime  0  2
                                                  ^
```

**fstab** is het **bestand dat uitgelezen wordt** door Linux **om de schijven te mounten**.\
Als je een schijf toevoegt en die mount maar dit **niet in fstab zet gaat Linux die niet mounten**.

## Schijf toevoegen

**Als je een nieuwe schijf in je computer steekt:**
1. **Linux detecteert** de schijf.
2. Het **wordt als bestand in `/dev` gezet**.
    - SATA-schijven krijgen een bestandsnaam zoals `/dev/sda`, `/dev/sdb`...
    - NVMe schijven: `/dev/nvme0n1`, `/dev/nvme1n1`...
    - Virtuele schijven: `/dev/vda`, `/dev/vdb`...
3. Het is **nog niet verbonden** met het bestandssysteem.
4. **Je partitioneert, formatteert en "mount" het.**
    - Mounten betekent dat je de schijf aan een locatie in je bestandssysteem toewijst.

### Stappen om een schijf toe te voegen

### 1: Schijf vinden

**Oplijsten** van **schijven**:
```
[student@ServerMIC ~]$ lsblk
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda             8:0    0    8G  0 disk
sr0            11:0    1    1G  0 rom  /run/media/student/RH...
nvme0n1       259:0    0   20G  0 disk
├─nvme0n1p1   259:1    0  600M  0 part /boot/efi
```

We zien `sda` staan, dit is **de toegevoegde** schijf.

### 2: gdisk

**Open de schijf in `gdisk`:**
```
[student@ServerMIC ~]$ sudo gdisk /dev/sda
```

Veel gebruikte commando's in gdisk:
- ?: toont help menu
- p: toont partitie tabel
- n: maak nieuwe partitie
- d: verwijder partitie
- t: verander partitie type
- w: stop en sla de veranderingen op
- q: stop en sla de veranderingen niet op

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

#### gdisk stappen:

*Stappen voor een standaard lege schijf.*

1. **n:** Maak nieuwe partitie
2. **enter:** Gebruik standaard partitie nummer
3. **enter:** Gebruik standaard voor standaard 1ste sector
4. **enter:** Gebruik standaard laatste sector *(om de heel schijf te gebruiken)*
5. **enter:** Gebruik standaard GUID
6. **w:** Maak de veranderingen
7. **y:** Bevestig dat je wilt doorgaan.
```
[student@ServerMIC ~]$ sudo gdisk /dev/sda
[sudo] wachtwoord voor student:
GPT fdisk (gdisk) version 1.0.7

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries in memory.

Command (? for help): n
Partition number (1-128, default 1):
First sector (34-16777182, default = 2048) or {+-}size{KMGTP}:
Last sector (2048-16777182, default = 16777182) or {+-}size{KMGTP}:
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300):
Changed type of partition to 'Linux filesystem'

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sda.
The operation has completed successfully.
```

### 3: Formatteer en mount de partitie

De **partitie is aangemaakt** en heeft een naam gekregen:
```
[student@ServerMIC ~]$ lsblk
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda             8:0    0    8G  0 disk
└─sda1          8:1    0    8G  0 part
```

**Formatteer de partitie** zodat ext4 gebruikt wordt:
```
[student@ServerMIC ~]$ sudo mkfs.ext4 /dev/sda1
```

**Maak een locatie** om de **schijf** aan **te linken**:
```
[student@ServerMIC ~]$ sudo mkdir /mnt/schijf
```

**Mount** de locatie:
```
[student@ServerMIC ~]$ sudo mount /dev/sda1 /mnt/schijf
```

**Open `/etc/fstab` in nano:**
```
[student@ServerMIC ~]$ sudo nano /etc/fstab
```

**Voeg** de juiste **instellingen toe** als **laatste lijn**:
```
/dev/sda1    /mnt/schijf    ext4    defaults    0    2
```

## LVM

**LVM** staat voor **Logical Volume Management**.

Het is een manier om **logische volumes dynamisch te beheren**.\
**Logische volumes** zijn **partities** die **over meerdere fysieke schijven** kunnen **verspreid** worden.

**LVM** is **handig** omdat je **logische volumes** kan **vergroten en verkleinen zonder data te verliezen**.

### Hoe LVM werkt

**LVM** gebruikt **3 concepten**:
```
Physical Volume -> Volume Group -> Logical Volume
       |                |                |
       |                |                |
       ↓                |                |
Een volledige schijf    |                |
of partitie op die      |                |
schijf.                 ↓                |
                Een groep van physical   |
                volumes.                 ↓
                                   Een logisch volume waar
                                   een bestandssysteem
                                   op kan staan.
```

**In een zin:**\
Er worden één of meerdere **physical volumes** gemaakt.\
Die worden **samengevoegd** in een **volume group**.\
Daaruit worden **logische volumes** gemaakt.

De **logische volumes** worden **geformatteerd** en **gemount** zoals een normale partitie.

### LVM commando's

Checken of er Physical Volumes, Volume Groups en Logical Volumes zijn:
```
[student@ServerMIC ~]$ sudo pvs
  PV             VG   Fmt  Attr PSize  PFree
  /dev/nvme0n1p3 rhel lvm2 a--  18,41g    0
[student@ServerMIC ~]$ sudo vgs
  VG   #PV #LV #SN Attr   VSize  VFree
  rhel   1   2   0 wz--n- 18,41g    0
[student@ServerMIC ~]$ sudo lvs
  LV   VG   Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root rhel -wi-ao---- 16,41g
  swap rhel -wi-ao----  2,00g
```

Om de **partities op een schijf** met extra info **te tonen**:
```
[student@ServerMIC ~]$ sudo gdisk -l /dev/nvme0n1
[student@ServerMIC ~]$ sudo lsblk /dev/nvme0n1
```

Om **informatie** te tonen over een **physical volume**:
```
[student@ServerMIC ~]$ sudo pvdisplay /dev/nvme0n1p3
```

Hetzelfde voor een **volume group en logical volume**:
```
[student@ServerMIC ~]$ sudo vgdisplay rhel
[student@ServerMIC ~]$ sudo lvdisplay /dev/rhel/root
```
*Gebruik deze zonder pad om een lijst van alle volume groups, logical volumes of physical volumes te tonen.*

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

#### Volumegroep en logisch volume maken





