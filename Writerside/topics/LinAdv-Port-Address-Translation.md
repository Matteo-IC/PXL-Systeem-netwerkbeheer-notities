# Port Address Translation

**PAT** (Port Address Translation) is een **vorm van NAT** (Network Address Translation).

**PAT** vertaald een **IP-adres en poortnummer** van een pakket **naar** een **ander IP-adres en poortnummer**.\
Dit wordt vaak gebruikt om **meerdere interne hosts** te laten **communiceren** met het internet **via één publiek IP-adres**.

## Configureren van PAT

Je hebt **minstens 2 interfaces** nodig, één voor het **interne netwerk** en één voor het **externe netwerk**.

Zet het **interne interface** in de **inside-zone** en het **externe interface** in de **outside-zone**:
```
$ sudo firewall-cmd --change-interface=ens224 --zone=internal --permanent
$ sudo firewall-cmd --change-interface=ens160 --zone=external --permanent
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

Zet de **standaard zone** op **internal**:\
*Als een nieuw interface toegevoegd wordt, staat die automatisch in de standaard zone.*
```
$ sudo firewall-cmd --set-default-zone=internal
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Herlaad** de firewall:
```
$ sudo firewall-cmd --reload
```

**Standaard staat PAT aan** in **firewalld**.

## Poorten forwarden

Een **poort naar** een **andere poort** vertalen / forwarden:\
*Bijvoorbeeld: poort 8080 naar poort 80*
```
$ firewall-cmd --add-forward-port=port=8080:proto=tcp:toport=80
```

**Opslaan** van de configuratie:
```
$ firewall-cmd --runtime-to-permanent
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**Verwijderen** van een **forwarding rule**:
```
$ firewall-cmd --remove-forward-port=port=8080:proto=tcp:toport=80
```

### Rich rule

**Vertalen** van **requests van elk IP-adres** naar **meerdere poorten** naar een **intern IP-adres en poort**:
```
$ firewall-cmd --zone=external --add-rich-rule='rule source address="0.0.0.0/0" forward-port port="4000-5000" protocol="tcp" to-port="22" to-addr="intern-ip"' --permanent
```

Specifieer op **welke IP-adressen** de forwarding rule van toepassing is:
```
$ ... source address="0.0.0.0/0" forward-port port="4000-5000" protocol="tcp" to-port="22" to-addr="intern-ip"' --permanent
      ^^^^^^^^^^^^^^^^^^^^^^^^^^
```

De **poorten** die **geforward** worden:
```
$ ... forward-port port="4000-5000" protocol="tcp" to-port="22" to-addr="intern-ip"' --permanent
      ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```

Het **protocol** van de forwarding rule:
```
$ ... protocol="tcp" to-port="22" to-addr="intern-ip"' --permanent
      ^^^^^^^^^^^^^^ 
```

De **poort** en **intern IP-adres** waar de **requests naar geforward** worden:
```
$ ... to-port="22" to-addr="intern-ip"' --permanent
      ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```
