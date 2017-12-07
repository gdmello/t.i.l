<hostname>.<domain_name>.<domain_suffix>
e.g- west.techrepublic.com

Design
======

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

              
           
