Networking
----------
* [Basic walkthrough](https://www.slideshare.net/ThomasGraf5/linuxcon-2015-linux-kernel-networking-walkthrough)
  * TCP fast open - `net.ipv4.tcp_fastopen`
  * Packet through the network stack (kernel space) explained
* [Networking Explained](https://events.static.linuxfound.org/sites/events/files/slides/2016%20-%20Linux%20Networking%20explained_0.pdf)
  * Network namespaces
  * VLAN - virtual LAN
  * Bonding
  * Veth - virtual ethernet cable
  * Bridge - virtual switch
 * [Routing](https://opensource.com/business/16/8/introduction-linux-network-routing)
   * The routing table sets the source and destination for each TCP packet
   * In Linux, the routing table can be viewed with
    ```bash
    $ route -n
    Kernel IP routing table
    Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
    0.0.0.0         0.0.0.0         0.0.0.0         U     50     0        0 tun0
    0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 enx8049710fae4d
    ```
    * The default gateway is always denoted by `0.0.0.0` in the destination with the `-n` flag
    * The default gateway is also denoted by the `G` flag in the `Flags` column.
    * `Iface` represents the outbound Network Interface Card (NIC)
    * The `Genmask` column represents the network mask
    * The default gateway has a netmask of `0.0.0.0` to indicate all packets not addressed to the local network or any other outbound routerwill be addressed to the default gateway. 
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

Resources
---------
[Kubernetes Networking Links](https://github.com/nleiva/kubernetes-networking-links)
