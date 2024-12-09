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
