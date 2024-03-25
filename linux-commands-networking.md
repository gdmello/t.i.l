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

View Current Network Connections
--------------------------------
```
$ resolvectl
Global
         Protocols: -LLMNR -mDNS +DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub
Current DNS Server: 45.90.28.0#76adf6.dns.nextdns.io
       DNS Servers: 45.90.28.0#76adf6.dns.nextdns.io 2a07:a8c0::#76adf6.dns.nextdns.io 45.90.30.0#76adf6.dns.nextdns.io 2a07:a8c1::#76adf6.dns.nextdns.io

Link 2 (enx0050b60f6bb3)
Current Scopes: none
     Protocols: -DefaultRoute +LLMNR -mDNS +DNSOverTLS DNSSEC=no/unsupported

Link 3 (wlp0s20f3)
Current Scopes: none
     Protocols: -DefaultRoute +LLMNR -mDNS +DNSOverTLS DNSSEC=no/unsupported

Link 4 (docker0)
Current Scopes: none
     Protocols: -DefaultRoute +LLMNR -mDNS +DNSOverTLS DNSSEC=no/unsupported

Link 5 (tun0)
    Current Scopes: DNS
         Protocols: +DefaultRoute +LLMNR -mDNS +DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 192.168.<X>.<Y>
       DNS Servers: 192.168.<X>.<Y>
        DNS Domain: <CUSTOM_DOMAIN>.com ~.

```
also via `nmcli`
```
$ nmcli c
NAME                UUID                                  TYPE      DEVICE
VPN                 29623885-efe3-4cfc-9e14-bca8e694cb4a  vpn       enx0070b70f7bb3 
tun0                56b44c3e-b6bb-427b-a51d-9ada931ab6f4  tun       tun0            
docker0             ff8bfff4-650b-4031-b454-d35167b10a76  bridge    docker0         
Wired connection 1  d8a5dc88-7233-3b57-b5cf-e0c707ad6633  ethernet  enx0070b70f7bb3 
```

Modify DNS Priority
-------------------
```
$ nmcli -p connection modify "<CONNECTION_NAME>" ipv4.dns-priority -100
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
[hostB]$ iptables -A INPUT -p udp --dport 8472 -j ACCEPT
[hostA]$ iptables -A OUTPUT -p udp --dport 8472 -j ACCEPT
```
From this point onwards, to enable bi-directional replication
```
[hostA]$ vi /etc/services
# Add this line
# otv             8472/udp                # Overlay Transport Virtualization (OTV)
[hostA]$ iptables -A INPUT -p udp --dport 8472 -j ACCEPT
[hostB]$ iptables -A OUTPUT -p udp --dport 8472 -j ACCEPT
```

Use Another Host As A Proxy Via SSH (Http Over SSH)
---------------------------------------------------
Locally access a rabbitmq management console, via a remote host which has access to the rabbitmq node.

Bind port local port 8080 to a hostname and port on the remote server, ie. bind locla port 8080 to  <RABBITMQ_MANAGEMENT_HOSTNAME> and port 15672 on <REMOTE_HOST>
```
ssh -L 8080:<RABBITMQ_MANAGEMENT_HOSTNAME>:15672 -o 'PubKeyAuthentication=no' <REMOTE_HOST>
<REMOTE_HOST> $
```

Now access the console via a web browser as-
```
curl https://localhost:8080
```

# Clear DNS Cache
```
  $ systemd-resolve --statistics
DNSSEC supported by current servers: no

Transactions
Current Transactions: 0
  Total Transactions: 325

Cache
  Current Cache Size: 156
          Cache Hits: 154
        Cache Misses: 215

DNSSEC Verdicts
              Secure: 0
            Insecure: 0
               Bogus: 0
       Indeterminate: 0

  $ sudo systemd-resolve --flush-caches
  $ gavin.dmello@pts-gdmell5 [13:41:34] ~ $ systemd-resolve --statistics
DNSSEC supported by current servers: no

Transactions
Current Transactions: 0
  Total Transactions: 326

Cache
  Current Cache Size: 0
          Cache Hits: 154
        Cache Misses: 216

DNSSEC Verdicts
              Secure: 0
            Insecure: 0
               Bogus: 0
       Indeterminate: 0
```
[source](https://vitux.com/how-to-flush-dns-cache-on-ubuntu/)
