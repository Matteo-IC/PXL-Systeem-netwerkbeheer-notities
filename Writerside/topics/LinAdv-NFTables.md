# NFTables

## Oefeningen

**1. Zorg ervoor dat er ‘vanaf de eerste seconde’ maar 1 ping-aanvraag per seconde mag verstuurd worden vanuit het
lokale netwerk (client&lt;jeintialen&gt;) zoals je hieronder ziet.**
```
$ sudo nft flush ruleset
$ sudo nft add table ip filter
$ sudo nft add chain ip filter input '{ type filter hook input priority 0; policy accept; }'
$ sudo nft add chain ip filter forward '{ type filter hook forward priority 0; policy accept; }'
$ sudo nft add rule ip filter input iif ens224 icmp type echo-request limit rate 1/second burst 1 packets accept
$ sudo nft add rule ip filter input iif ens224 icmp type echo-request counter drop
$ sudo nft add rule ip filter forward iif ens224 icmp type echo-request limit rate 1/second burst 1 packets accept
$ sudo nft add rule ip filter forward iif ens224 icmp type echo-request counter drop
$ sudo nft add rule ip filter input ct state established,related accept
$ sudo nft add rule ip filter forward ct state established,related accept
$ sudo nft add rule ip filter input iif lo accept
$ sudo systemctl enable nftables
$ sudo systemctl start nftables
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**2.Blokkeer al het binnenkomend verkeer buiten ssh-verkeer vanaf enkel clientXX (10.10.10.10) en verkeer dat je op de
machine zelf hebt aangevraagd. Maak screenshots van je resultaat van het niet en wel verbinding kunnen maken van
clientXX met nasbox.**
```
$ sudo nft flush ruleset
$ sudo nft add table inet filter
$ sudo nft add chain inet filter input '{ type filter hook input priority 0; policy drop; }'
$ sudo nft add chain inet filter forward '{ type filter hook forward priority 0; policy drop; }'
$ sudo nft add chain inet filter output '{ type filter hook output priority 0; policy accept; }'
$ sudo nft add rule inet filter input iif lo accept
$ sudo nft add rule inet filter input ct state established,related accept
$ sudo nft add rule inet filter input ip saddr 10.10.10.10 tcp dport 22 accept
$ sudo nft add rule inet filter input drop
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**3. Hoe kan je instellen dat enkel verkeer van 10.10.10.10 geblokkeerd wordt? Alle ander verkeer naar de server wordt
toegestaan. Test dit uit door te pingen vanaf je host (je computer zelf) en vanaf clientXX naar nasbox.
Maak hiervan screenshots.**
```
$ sudo nft flush ruleset
$ sudo nft add table inet filter
$ sudo nft add chain inet filter input '{ type filter hook input priority 0; policy accept; }'
$ sudo nft add chain inet filter forward '{ type filter hook forward priority 0; policy accept; }'
$ sudo nft add chain inet filter output '{ type filter hook output priority 0; policy accept; }'
$ sudo nft add rule inet filter input ip saddr 10.10.10.10 drop
$ sudo nft add rule inet filter forward ip saddr 10.10.10.10 drop
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**4. Stel in dat al het verkeer van buiten naar binnen wordt geaccepteerd op nasbox maar icmp-verkeer moet worden
geblokkeerd. Check dit uit en maak screenshot.**
```
sudo nft flush ruleset
sudo nft add table inet filter
sudo nft add chain inet filter input '{ type filter hook input priority 0; policy accept; }'
sudo nft add chain inet filter forward '{ type filter hook forward priority 0; policy accept; }'
sudo nft add chain inet filter output '{ type filter hook output priority 0; policy accept; }'
sudo nft add rule inet filter input ip protocol icmp drop
sudo nft add rule inet filter input ip6 nexthdr icmpv6 drop
```

<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->
<format style="underline">
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
</format>
<!-- INVISIBLE CHARACTERS FOR SECTION LINE -->

**5. Wat is een XMAS Packet? Hoe kan je je ertegen beveiligen? Leg met eigen woorden uit hoe een hacker hierbij tewerk 
gaat en waarom.**

Een XMAS packet is soort netwerkpakket dat alle opties / flags aan heeft staan voor dat protocol, bijvoorbeeld FIN, URG en PSH
voor TCP. Je kan je beveiligen via een firewall configuratie die deze pakketten blokkeert.

Een hacker stuurt XMAS packets om verschillende dingen te zien: of de poort waar die naar stuurt open is, welk OS gebruikt wordt
(andere OS'en reageren anders op XMAS packets) en om te zien hoe de firewall geconfigureerd is. Dit kan gebruikt worden 
om kwetsbaarheden te vinden.
