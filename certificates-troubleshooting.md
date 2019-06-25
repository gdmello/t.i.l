## Issue: Unable to connect to the server: x509: certificate is valid for [<hostnames>] not <target_hostname>
Full Error:

    Unable to connect to the server: x509: certificate is valid for m1-cluster, localhost, kubernetes, kubernetes.default, kubernetes.default.svc, kubernetes.default.svc.cluster.local, not m1-cluster.domain.com
    
### Verify that a certificate served by a server matches the provided hostname   

    openssl s_client -verify_hostname www.example.com -connect example.com:443
  
  [source](https://www.freecodecamp.org/news/openssl-command-cheatsheet-b441be1e8c4a/)
