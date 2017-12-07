FQDN - <hostname>.<domain_name>.<domain_suffix>
e.g- west.techrepublic.com
FQDN uniquely identifies the host within the DNS namespace.

Design
======
```
+------------------------+
|      Root Servers      |
| (.com,.net, .org,      |
|  .mil, .edu, .gov,     |
| .int)                  |
|                        |
|                        |
+------------+-----------+-----------------+
             |                             |
             |                             |
             |                             |
             |                             |
             |                             |
   +---------v--------+           +--------v---------+
   |     Name Servers |           |   Name Server    |
   |   (.com)         |           |    (.int)        |
   |domain record list+----------->domain record list|
   |                  |           |                  |
   |                  |           |                  |
   +------------------+           +------------------+
```
* Root servers are primary servers which manage top level domains
* Root servers typically delegate to authoritative named servers for specific domains
* Authoritative named servers delegate the DNS lookup to an org that owns the domain or the ISP which provides the internet connection to the organization.

How it works
============

* Web browser/ email app/ service -> DNS resolution request -> Local resolver
* local resolver -> known named servers (in tcp/ip settings) 
* known name server does not find in cache -> forward dns resolution request to root server for the dns request domain suffix -> root server returns authoritative name server
* known name server -> DNS resolution request -> authoritative name server -> gets IP -> returned to local resolver
* local resolver returns IP to requestor (web browser/ email client/ service)

Zones
=====
If a name server contains the dns records for a subset of the domain, while other name servers control the other mappings, then it contains a zone. The nameserver is authoritative for that zone. If a single name server contains all the records of a DNS namespace, then the zone and domain are synonymous.

Record Types
============

A DNS nameserver contains a listing of hostnames to IP addresses. But these records can be of other types too. See -
```
+--------+--------------------------------------------------------------------------------------+
| Record |                                       Purpose                                        |
+--------+--------------------------------------------------------------------------------------+
| SOA    | Specifies authoritative server for the zone                                          |
| NS     | Specifies address of domain’s name server(s)                                         |
| A      | Maps host name to an address                                                         |
| PTR    | Maps address to a host name for reverse lookup                                       |
| CNAME  | Creates alias (synonymous) name for specified host. Canonical Name                   |
| MX     | Mail exchange server for domain                                                      |
| SRV    | Defines servers for specific purpose such as HTTP, FTP, and so on                    |
| AAAA   | Maps host name to Ipv6 address                                                       |
| AFSDB  | Location of AFS cell database server or DCE cell’s authenticated server              |
| HINFO  | Identifies host’s hardware and OS type                                               |
| ISDN   | Maps host name to ISDN address (phone number)                                        |
| MB     | Associates host with specified mailbox; experimental                                 |
| MG     | Associates host name with mail group; experimental                                   |
| MINFO  | Specifies mailbox name responsible for mail group; experimental                      |
| MR     | Specifies mailbox name that is proper rename of other mailbox; experimental          |
| RP     | Identifies responsible person for domain or host                                     |
| RT     | Specifies intermediate host that routes packets to destination host                  |
| TXT    | Associates textual information with item in the zone                                 |
| WKS    | Describes services provided by specific protocol on specific port                    |
| X.25   | Maps host name to X.121 address (X.25 networks); used in conjunction with RT records |
| WINS   | Allows lookup of host portion of domain name through WINS server                     |
| WINS-R | Reverses lookup through WINS server                                                  |
| ATMA   | Maps domain name to ATM address                                                      |
+--------+--------------------------------------------------------------------------------------+
```
Source - https://www.techrepublic.com/article/understanding-how-dns-works-part-1/

Most common record types are SOA, A, CNAME. A record type maps a host name to an IP address. 
While the CNAME record type maps an alias to a FQDN (Fully Qualified Domain Name).
