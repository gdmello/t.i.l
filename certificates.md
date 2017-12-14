Introduction To SSL/HTTPS
=========================
A small guide while learning SSL/HTTPs.


At the heart of securing network traffic to/fro a website, lies PKI (Public key Infrastructure).
PKI includes two keys - private and public key.
* The public key is distributed and is used to encrpyt all requests to the server to be secured.
* The private key helps determine identity, and is never shared. 
The private key is used to decrypt the requests originally encrypted by the public key

One concern about such a secure exchange is MtM - man in the middle. i.e. the request is intercepted between
the client and the server and modified. To protect against such an attack, the client can hash the request, and 
encrypt it and include it in the request to the server. The server can then use the private key to decrypt the 
hash, compute the hash of the request and compare it to the decrypted hash, if they match then the request was not 
modified in transit.

HTTPs
=====
In order to secure a webite to use SSL,
* a certificate is required from a certificate authority (CA), or 
* the certificate is self-signed to bypass a CA.

Self-signed Certificates
------------------------
* Used only to secure traffic to a service
* cannot be used to determine servers identity
* useful for non-production or non-public servers

CA-signed Certificates
----------------------
* Used to secure production and public servers
* An external authority validates the identity of the server

Both CA and Self signed certificates can be generated in any of these ways-
* CSR and a private key
* CSR and exisitng private key
* CSR from existing certificate and private key

CSR = Certificate Signing Request

Format
======
Certificates follow the X.509 format. Using OpenSSL to generate a certificate results in a *.crt* (Certificate) and *.csr* (CSR) file. Both files are in the PEM format. PEM is an ASCII encoding, other encodings include DER, PKCS7, PKCS12.

