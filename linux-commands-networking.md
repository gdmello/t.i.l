Determine Packet Route
----------------------
Perform an actual [lookup](https://events.static.linuxfound.org/sites/events/files/slides/2016%20-%20Linux%20Networking%20explained_0.pdf) in the Kernel -
``` bash
$ ip route 10.70.70.11
10.70.70.11 via 10.103.10.11 dev eth3  src 10.103.10.112 
    cache
```

View Routes (Useful to check if a program appends to routes, like vpn/ docker-compose etc)
------------------------------------------------------------------------------------------
``` bash
$ route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         10.203.0.1      0.0.0.0         UG    0      0        0 eth3
10.0.3.0        0.0.0.0         255.255.255.0   U     0      0        0 lxcbr0
10.203.0.0      0.0.0.0         255.255.0.0     U     1      0        0 eth3
172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 docker0
172.18.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-4433db5330c8
```
or 
```bash
$ ip route
default via 10.203.0.1 dev eth3  proto static 
10.0.3.0/24 dev lxcbr0  proto kernel  scope link  src 10.0.3.1 
10.203.0.0/16 dev eth3  proto kernel  scope link  src 10.203.0.94  metric 1 
172.17.0.0/16 dev docker0  proto kernel  scope link  src 172.17.0.1 
172.18.0.0/16 dev br-4433db5330c8  proto kernel  scope link  src 172.18.0.1 
```
View Route Statistics
---------------------

[mtr](https://github.com/traviscross/mtr) combines `traceroute` and `ping` to display statistics about each hop to reach a destination host and sends ICMP packets to each host to determine quality of the link.

Check Host Is Up/ Common Ports Available
----------------------------------------
```
$ nmap c3.domain.com

Starting Nmap 6.40 ( http://nmap.org ) at 2018-10-18 15:11 EDT
Nmap scan report for c3.domain.com (10.70.180.63)
Host is up (0.0012s latency).
Not shown: 991 filtered ports
PORT     STATE  SERVICE
22/tcp   closed ssh
53/tcp   open   domain
80/tcp   open   http
113/tcp  closed ident
443/tcp  open   https
2000/tcp open   cisco-sccp
5060/tcp open   sip
8008/tcp open   http
9418/tcp closed git

Nmap done: 1 IP address (1 host up) scanned in 4.66 seconds
```

View All Sockets
----------------
```
$ ss -s
Total: 2738 (kernel 0)
TCP:   783 (estab 62, closed 693, orphaned 0, synrecv 0, timewait 3/0), ports 0

Transport Total     IP        IPv6
*	  0         -         -        
RAW	  0         0         0        
UDP	  38        33        5        
TCP	  90        83        7        
INET	  128       116       12       
FRAG	  0         0         0       
```

Open Up A Port
--------------
Assuming communication from hostA -> hostB on port 8472
```
[hostB] $ vi /etc/services
# Add this line
# otv             8472/udp                # Overlay Transport Virtualization (OTV)
[hostB]$ iptables -A INPUT -p tcp --dport 8472 -j ACCEPT
[hostA]$ iptables -A OUTPUT -p tcp --dport 8472 -j ACCEPT
```
From this point onwards, to enable bi-directional replication
```
[hostA]$ vi /etc/services
# Add this line
# otv             8472/udp                # Overlay Transport Virtualization (OTV)
[hostA]$ iptables -A INPUT -p tcp --dport 8472 -j ACCEPT
[hostB]$ iptables -A OUTPUT -p tcp --dport 8472 -j ACCEPT
```

