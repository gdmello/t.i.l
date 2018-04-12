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
