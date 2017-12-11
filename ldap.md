http://www.ldapman.org/articles/intro_to_ldap.html

* LDAP is a protocol for accessing information from an Information Directory/ LDAP Directory.
* An LDAP server processes all the queries and updates to an LDAP Directory
* The LDAP Directory are heavily optimized for read performance
* LDAP entries are heirarchical

Entries
=======

top level entry/root
--------------------
Since LDAP entries are heirarchical, they have to have a root.  
The top level record is known as a `base DN`. The base DN has 3 different forms-

`o=Apple,c=US` - 'o' or Organization and 'c' Country
`o=apple.com` - use the company's domain name
`dc=apple,dc=com` - split the company's domain name, default when using Microsoft AD.

Directory record
----------------
Every LDAP Directory record include a `Distinguished Name` or DN, similar to DNS host names.
The DN includes two components - Relative DN and LDAP Directory location of that record, and is read
backwards, ie a bottom up approach.
e.g - The DN of this record-
* dc=apple,dc=com
* ou=tablets (Organizational Unit)
* cn=ipad7

is `cn=ipad7,ou=tablets,dc=apple,dc=com`

The Relative DN or RDN is comprimsed mostly of the Common Name or cn attribute.

Example of an LDAP Directory entry-
```
    dc=foobar, dc=com 
        ou=customers 
            ou=asia 
            ou=europe 
            ou=usa 
        ou=employees 
        ou=rooms 
        ou=groups 
        ou=assets-mgmt 
        ou=nisgroups 
        ou=recipes
```
