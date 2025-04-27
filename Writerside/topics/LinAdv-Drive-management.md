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
**Bestandssysteem:** Een **manier om data te organiseren** op een schijf.

In **Linux begint** alles vanuit de **root map `/`**.

## Mount

Om een **schijf, partitie, USB, netwerk share...** te **gebruiken** moet je die **mounten**.

**Mount locatie:** Een **locatie in het bestandssysteem** waar een **schijf aan gekoppeld** is.

Het commando volgt deze structuur:
```
sudo mount [opties] apparaat mount_locatie
```

Bijvoorbeeld:
```
[student@ServerMIC ~]$ sudo mount /dev/sda1 /mnt/schijf
```

Om niet meer te mounten kan je `umount` gebruiken:
```
[student@ServerMIC ~]$ sudo umount /mnt/schijf
```

## Partities

Een **partitie type** is een **nummer** dat **aangeeft** wat **voor soort partitie** het is.\
Dit **vertelt** het **besturingssysteem hoe** het **met** de **partitie moet omgaan**.

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

## Partities maken en aanpassen

**Als je een nieuwe schijf in je computer steekt:**
1. **Linux detecteert** de schijf.
2. Het **wordt als bestand in `/dev` gezet**.
    - SATA-schijven krijgen een bestandsnaam zoals `/dev/sda`, `/dev/sdb`...
    - NVMe schijven: `/dev/nvme0n1`, `/dev/nvme1n1`...
    - Virtuele schijven: `/dev/vda`, `/dev/vdb`...
3. Het is **nog niet verbonden** met het bestandssysteem.
4. **Je partitioneert, formatteert en "mount" het.**
    - Mounten betekent dat je de schijf aan een locatie in je bestandssysteem toewijst.

### Stappen om een schijf toe te voegen met 1 partitie

#### 1: Schijf vinden

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

#### 2: gdisk

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

#### gdisk stappen:

*Stappen voor een standaard lege schijf.*

1. **n:** Maak nieuwe partitie
2. **enter:** Gebruik standaard partitie nummer
3. **enter:** Gebruik standaard voor standaard 1ste sector
4. **enter:** Gebruik standaard laatste sector *(om de heel schijf te gebruiken)*
5. **enter:** Gebruik standaard GUID
6. **w:** Maak de veranderingen
7. **y:** Bevestig dat je wilt doorgaan.
<code-block collapsible="true">
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
</code-block>

#### 3: Formatteer en mount de partitie

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

**Mount** de locatie:\
*Om te unmounten: `sudo umount /mnt/schijf`*
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

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Partitie verwijderen

**Unmount** de partitie met `umount`:\
*Je kan de device name of het mount point gebruiken.*
```
[student@ServerMIC ~]$ sudo umount /dev/sda1
[student@ServerMIC ~]$ sudo umount /mnt/schijf
```

**Verwijder** de partitie **uit fstab**:
```
[student@ServerMIC ~]$ sudo nano /etc/fstab
```

**Verwijder** de partitie **met gdisk**:
1. Typ `p` om de partities te zien.
2. Typ `d` om een partitie te verwijderen.
3. Typ het nummer van de partitie.
   1. Als je maar 1 partitie hebt, wordt die automatisch gekozen.
4. Typ `w` en daarna `y` om de veranderingen op te slaan.
<code-block collapsible="true">
<![CDATA[
[student@ServerMIC ~]$ sudo gdisk /dev/sda
GPT fdisk (gdisk) version 1.0.7

Partition table scan:
MBR: protective
BSD: not present
APM: not present
GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): p
Disk /dev/sda: 16777216 sectors, 8.0 GiB
Model: VMware Virtual S
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 2D946427-0FFF-4097-810F-D2160E431DD9
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 16777182
Partitions will be aligned on 2048-sector boundaries
Total free space is 2014 sectors (1007.0 KiB)

Number  Start (sector)    End (sector)  Size       Code  Name
1            2048        16777182   8.0 GiB     8300  Linux filesystem

Command (? for help): d
Using 1

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sda.
The operation has completed successfully.
]]>
</code-block>

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Meerdere partities maken

**Open opnieuw** de schijf in `gdisk`.
1. **Maak een nieuwe partitie** met `n`.
2. **Kies een nummer** voor de partitie.
3. **Eerste sector** is standaard, druk op enter.
4. **Laatste sector** is de **grootte** van de partitie.
   1. `+500M` voor 500 MB.
   2. `+1G` voor 1 GB.
5. **GUID** is standaard, druk op enter.
6. **Herhaal** voor elke nieuwe partitie.
7. Check de partities met `p`.
8. **Sla de veranderingen op** met `w` en `y`.
<code-block collapsible="true">
<![CDATA[
[student@ServerMIC ~]$ sudo gdisk /dev/sda
GPT fdisk (gdisk) version 1.0.7

Partition table scan:
MBR: protective
BSD: not present
APM: not present
GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): n
Partition number (1-128, default 1): 1
First sector (34-16777182, default = 2048) or {+-}size{KMGTP}:
Last sector (2048-16777182, default = 16777182) or {+-}size{KMGTP}: +500MB
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300):
Changed type of partition to 'Linux filesystem'

Command (? for help): n
Partition number (2-128, default 2): 3
First sector (34-16777182, default = 1026048) or {+-}size{KMGTP}:
Last sector (1026048-16777182, default = 16777182) or {+-}size{KMGTP}: +1G
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300):
Changed type of partition to 'Linux filesystem'

Command (? for help): p
Disk /dev/sda: 16777216 sectors, 8.0 GiB
Model: VMware Virtual S
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 2D946427-0FFF-4097-810F-D2160E431DD9
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 16777182
Partitions will be aligned on 2048-sector boundaries
Total free space is 13655997 sectors (6.5 GiB)

Number  Start (sector)    End (sector)  Size       Code  Name
1            2048         1026047   500.0 MiB   8300  Linux filesystem
3         1026048         3123199   1024.0 MiB  8300  Linux filesystem

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sda.
The operation has completed successfully.
]]>
</code-block>

**Vergeet niet om de partities te formatteren en mounten.**

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Partitie type veranderen

**Open gdisk**
1. **Typ** `l` om de **lijst met partitie types** te zien.
2. **Typ** `t` om het **type te veranderen**.
3. **Typ** het **nummer** van de partitie.
4. **Geef** het **nieuwe type**.
5. **Controleer** met `p`.
6. **Sla de veranderingen op** met `w` en `y`.
<code-block collapsible="true">
<![CDATA[
[student@ServerMIC ~]$ sudo gdisk /dev/sda
GPT fdisk (gdisk) version 1.0.7

Partition table scan:
MBR: protective
BSD: not present
APM: not present
GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): l
Type search string, or <Enter> to show all codes:
0700 Microsoft basic data                0701 Microsoft Storage Replica
0702 ArcaOS Type 1                       0c01 Microsoft reserved
2700 Windows RE                          3000 ONIE boot
3001 ONIE config                         3900 Plan 9
...
fb00 VMWare VMFS                         fb01 VMWare reserved
fc00 VMWare kcore crash protection       fd00 Linux RAID

Command (? for help): t
Partition number (1-3): 1
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300): 8e00
Changed type of partition to 'Linux LVM'

Command (? for help): p
Disk /dev/sda: 16777216 sectors, 8.0 GiB
Model: VMware Virtual S
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 2D946427-0FFF-4097-810F-D2160E431DD9
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 16777182
Partitions will be aligned on 2048-sector boundaries
Total free space is 13655997 sectors (6.5 GiB)

Number  Start (sector)    End (sector)  Size       Code  Name
1            2048         1026047   500.0 MiB   8E00  Linux LVM
3         1026048         3123199   1024.0 MiB  8300  Linux filesystem

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sda.
The operation has completed successfully.
]]>
</code-block>

**Vergeet niet om de partities te formatteren en mounten.**

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Met `sudo parted -l` kan je **partities** en **extra info** zien.
```
Model: VMware, VMware Virtual S (scsi)
Schijf /dev/sda: 8590MB
Sectorgrootte (logisch/fysiek): 512B/512B
Partitietabel: gpt
Schijfvlaggen:

Nummer  Begin   Einde   Grootte  Bestandssysteem  Naam              Vlaggen
 1      1049kB  525MB   524MB    ext4             Linux LVM         lvm
 3      525MB   1599MB  1074MB                    Linux filesystem
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

### Fysiek volume, volume groep en logisch volume maken

**Voordat** je **fysieke volumes maakt**, moeten er **partities** van het **type** `8e00` / **Linux LVM zijn**.

1. Gebruik `pvcreate` om een **fysiek volume** (of meerdere) te maken:
```
[student@ServerMIC ~]$ sudo pvcreate /dev/sda1 /dev/sda3
```
Gebruik daarna `sudo pvs` om te controleren.

2. **Maak een volume group** met `vgcreate`:
```
[student@ServerMIC ~]$ sudo vgcreate vg_naam /dev/sda1 /dev/sda3
```
Controleer met `sudo vgs`.

3. Een **logisch volume** maak je met `lvcreate`:
```
[student@ServerMIC ~]$ sudo lvcreate -n lv_naam -L 1G vg_naam
```
Controleer met `sudo lvs`.

4. **Formatteer** het logisch volume:
```
[student@ServerMIC ~]$ sudo mkfs.ext4 /dev/vg_naam/lv_naam
```

5. Maak een **mount locatie** en **mount** het logisch volume:
```
[student@ServerMIC ~]$ sudo mkdir /mnt/lv_naam
[student@ServerMIC ~]$ sudo mount /dev/vg_naam/lv_naam /mnt/lv_naam
```

6. **Voeg** de **mount locatie** toe aan `/etc/fstab`:
```
[student@ServerMIC ~]$ sudo nano /etc/fstab
/dev/vg_naam/lv_naam    /mnt/lv_naam    ext4    defaults    0    2
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Logisch volume vergroten

Gebruik het `lvextend` commando om een logisch volume te vergroten:
```
[student@ServerMIC ~]$ sudo lvextend -L +200M -r /dev/vg_naam/lv_naam
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

### Logisch volume verkleinen

**Verkleinen** van een logisch volume is **gevaarlijk** omdat je **data kan verliezen**.

**Unmount** het logisch volume:
```
[student@ServerMIC ~]$ sudo umount /mnt/lv_naam
```

**Controleer** of er **geen fouten** zijn met het bestandssysteem:
```
[student@ServerMIC ~]$ sudo e2fsck -f /dev/vg_naam/lv_naam
```

**Verklein** het **logisch volume**:
```
[student@ServerMIC ~]$ sudo lvreduce -L 500M -r /dev/vg_naam/lv_naam
```

**Mount** het logisch volume **opnieuw**:
```
[student@ServerMIC ~]$ sudo mount /dev/vg_naam/lv_naam /mnt/lv_naam
```

**Herlaad** de configuratie bestanden (waaronder dus **fstab**):
```
[student@ServerMIC ~]$ sudo systemctl daemon-reload
```

## Swapruimte

**Swappartitie:** Als er weinig RAM is, wordt niet gebruikte RAM tijdelijk opgeslagen in de swappartitie.

### Swapruimte maken

Om **swapruimte** te **maken** heb je een **bestand nodig**:
```
[student@ServerMIC ~]$ sudo fallocate -l 1G /swapfile
```
*`fallocate` reserveert ruimte voor een bestand. Het duidt alleen het begin en einde aan zonder de content te vullen waardoor
het heel efficiënt is voor dit soort bestanden te maken.*

Zet de **juiste rechten** op het bestand zodat **alleen root het kan lezen en schrijven**:\
*RAM kan gevoelige data bevatten die je niet wilt dat anderen kunnen lezen.*
```
[student@ServerMIC ~]$ sudo chmod 600 /swapfile
```

**Maak** een **swapruimte** van het bestand:
```
[student@ServerMIC ~]$ sudo mkswap /swapfile
```

**Zet** de **swapruimte aan**:
```
[student@ServerMIC ~]$ sudo swapon /swapfile
```

**Controleer** of de **swapruimte gemaakt is**:
```
[student@ServerMIC ~]$ swapon
```

**Voeg** de **swapruimte toe** aan `/etc/fstab`:
```
[student@ServerMIC ~]$ sudo nano /etc/fstab
/swapfile    none    swap    sw    0    0
```

*Voer `sudo swapon -a` uit om de swapruimte aan te zetten als die niet al aan stond zonder de computer te herstarten.*

### Swapruimte verwijderen

**Voordat** je de **swapruimte verwijdert**, moet je **checken of** die **niet gebruikt wordt**.
```
[student@ServerMIC ~]$ swapon
```

Daarna kan je het uit zetten:
```
[student@ServerMIC ~]$ sudo swapoff /swapfile
```

## Schijf gebruik

### du commando

Het commando `du` (**disk usage**) toont hoeveel ruimte een map of bestand innemen.

Met de opties `-sh` toont het enkel de grootte en in leesbaar formaat:
```
[student@ServerMIC ~]$ du -sh /home/student
[student@ServerMIC ~]$ du -sh bestand
```

Het **toont de grootte van een map en de mappen eronder**, om **enkel de map zelf** te tonen gebruik `-d 1`:
*Als je `-d 2` gebruikt gaat het 2 mappen diep. Dit werkt niet samen met de `-s` optie*
```
[student@ServerMIC ~]$ du -hd 1 /home/
```

## Oefeningen

**1.
Toon hoe je de naam vindt van de drive die je wil gebruiken.**
```
$ lsblk
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2.
Toon de partitietabel van de virtuele drive/USB-drive**
```
$ sudo gdisk /dev/sda
[sudo] wachtwoord voor student:
GPT fdisk (gdisk) version 1.0.7

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries in memory.

Command (? for help): p
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3.
Verwijder alle partities op de USB-drive (of hoe je dit zou doen als je een virtuele drive gebruikt).
Sla deze veranderingen op en toon dat dit ook is aangepast in de partitietabel en de Linux kernel.**

<a href="LinAdv-Drive-management.md" anchor="partitie-verwijderen">Partities verwijderen</a>

```
$ ls /lib/modules/$(uname -r)/kernel/fs
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**4.
Voeg 3 partities toe aan de drive: a. 100MB Linux partitie b. 200MB swap partitie c. 500MB LVM partitie Sla deze
verandering op.**

```
$ sudo gdisk /dev/sda

Command: n
Partition number: Enter
First sector: Enter
Last sector: +100M
Hex code: Enter        # Linux is standaard

Command: n
Partition number: Enter
First sector: Enter
Last sector: +200M
Hex code: 8200         # Linux swap

Command: n
Partition number: Enter
First sector: Enter
Last sector: +500M
Hex code: 8e00         # Linux LVM

Command: p             # Partitie tabel
Command: w             # Sla op
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**5.
Geef de Linux partitie een ext4 filesystem.**

```
$ sudo mkfs.ext4 /dev/sda1
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**6.
Maak een mountpoint genaamd /mnt/mypart en mount de nieuwe linux partitie hierop.**

```
$ sudo mkdir /mnt/mypart
$ sudo mount /dev/sda1 /mnt/mypart
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**7.
Enable de swap partitie en zet deze aan zodat er extra swap ruimte bruikbaar is.**

```
$ sudo mkswap /dev/sda2
$ sudo swapon /dev/sda2
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**8.
Maak een volumegroep genaamd ‘OefVG’ van de LVM partitie.\
Maak daarna een logisch volume van 200MB van de groep OefVG genaamd ‘OefData’.\
Geef het volume OefData een ext4 filesysteem.\
Mount nu dit volume tijdelijk op een nieuwe directory genaamd ‘/mnt/oefening’.\
Kijk of dit succesvol is gemount.**

```
$ sudo pvcreate /dev/sda3
$ sudo vgcreate OefVG /dev/sda3
$ sudo lvcreate -L 200M -n OefData OefVG
$ sudo mkfs.ext4 /dev/OefVG/OefData
$ sudo mkdir /mnt/oefening
$ sudo mount /dev/OefVG/OefData /mnt/oefening
$ lsblk
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**9.
Vergroot het logische volume ‘OefData’ van 200MB naar 300MB.**

```
$ sudo lvextend -L 300M /dev/OefVG/OefData
$ sudo resize2fs /dev/OefVG/OefData # niet gevraagd maar goed (vergroot bestandssyteem)
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**10.
Doe alles wat nodig is om de USB/Drive veilig te verwijderen van de computer: a. Unmount de linux partitie
b. Zet de swap partitie uit c. Unmount het logische volume d. Verwijder de volume groep**

```
$ sudo umount /mnt/mypart
$ sudo swapoff /dev/sda2
$ sudo umount /mnt/oefening
$ sudo lvremove /dev/OefVG/OefData
$ sudo vgremove OefVG
$ sudo pvremove /dev/sda3
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**11.
Gebruik het commando du om de grootste mappen te tonen die zich bevinden in /usr/share. Sorteer de mappen van groot naar
klein en lijst alleen de 10 grootste op.**

```
sudo du -sh /usr/share/* | sort -rh | head -10
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**12.
Gebruik het commando df om alle vrije ruimte te tonen van alle filesystems die momenteel verbonden zijn met je systeem, 
maar toon de filesystems tmpfs en devtmpfs niet.**

```
$ df -h -x tmpfs -x devtmpfs
```