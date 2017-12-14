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

