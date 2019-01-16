Proxy
-----
`http_proxy` environment variable can be used to proxy http requests

Search for a process by name
------------------------------
`pgrep -n 1 etcd`

Send SIGHUP signal to a process
-------------------------------
```kill SIGHUP `pgrep etcd` ```

Remote Characters
-----------------
`kubectl get cm my-config-map | jq '.data.release' | tr -d '"'`
returns the JSON string without quotes.
single quotes are not base64 ecoded.

Show/ Manipulate routing, devices, policy routing and tunnels
-------------------------------------------------------------
ip -addr

Print Logs From Kernel Ring Buffer
----------------------------------

dmesg

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

Tail Process Ids
----------------
Tail a file via it's process ID, which is useful if waiting on a process to release a file-
```
$ tail -f --pid=1234 /home/usr/myfile
$ tail -f --pid=1234 /dev/null # Make tail command quit when the PID 1234 dies, useful to wait on a process to terminate.
```

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
