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

Certificate Authorities (CAs)
=============================
* A CA generates and validates digital certificates
* The CA adds it's own signature to the public key of the client, essentially indicating that the public key is valid. 
* Examples of CA are - VeriSign, Entrust and GlobalSign

Obtain a Certificate
--------------------
1. Requestor requests a certificate from CA
2. CA authenticates requestor and issues a digital certificate
3. CA publishes the certificate in a public certificate store, so message receiver can authenticate the CA

TLS Flow
--------
* Browser makes request to webserver
* webserver returns public key and certificate
* browser possesses the public key of the CA and verifies the CA signature in the Certificate and thus trusts the certificate
and the public key in it.
* Browser then uses the public key to enrcypt/decrypt data to/from the webserver (maybe with a temporary symmetric key)

Format
======
Certificates follow the X.509 format. Using OpenSSL to generate a certificate results in a *.crt* (Certificate) and *.csr* (CSR) file. Both files are in the PEM format. PEM is a base64 (ASCII) encoding, other encodings include DER, PKCS7, PKCS12.

PEM
---
A pem file can contain a number of certificates and a key, [source](http://how2ssl.com/articles/working_with_pem_files/)-
* public certificate
* root certificate
* intermediate certificate
* private key

Sources
=======
* https://www.digitalocean.com/community/tutorials/openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs
* http://how2ssl.com/articles/openssl_commands_and_tips/
* https://www.scientificcomputing.com/blog/2007/11/understanding-digital-certificates-beginner%E2%80%99s-guide
* http://www.tech-faq.com/understanding-certificate-authorities.html

