Create A Self-Signed Certificate
================================
```
$ sudo mkdir /etc/ssl/mydomain.com.com
# create a key
$ sudo openssl genrsa -out /etc/ssl/mydomain.com/mydomain.com.key 1024
# create a certificate request
$ sudo openssl req -new -key /etc/ssl/mydomain.com/mydomain.com.key -out /etc/ssl/mydomain.com/mydomain.com.csr
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:NC
Locality Name (eg, city) []:Raleigh
Organization Name (eg, company) [Internet Widgits Pty Ltd]:MYCOMPANY
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:*.mydomain.com
Email Address []:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:

# create a certificate from the request
$ sudo openssl x509 -req -days 365 -in /etc/ssl/mydomain.com/mydomain.com.csr -signkey /etc/ssl/mydomain.com/mydomain.com.key -ot /etc/ssl/mydomain.com/mydomain.com.crt

# create a PEM file, which is a combination of tke signing key and certificate files
$ sudo cat /etc/ssl//mydomain.com/mydomain.com.crt /etc/ssl/mydomain.com/mydomain.com.key | sudo tee /etc/ssl/mydomain.com/mydomain.com.pem
```
