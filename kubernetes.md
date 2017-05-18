# Securing K8s

* Setup k8s cluster to use TLS between nodes.
* Can use "Let's Encrypt" as the CA (Certificate Authority) to manage certificates - revoke, request and renew 
* The certificate management agent resides on the web server.
* To begin certificate requests, the CA verifies the web server controls the domain. This is done by presenting the agent with the choice of responding to 2 [challenges](https://letsencrypt.org/how-it-works/)-
  * provision a DNS record under the domain *'example.com'* or
  * provision a resource under the URI *'http.example.com'*
* 
* If deploying k8s on AWS, *Route53* can be used as the DNS responder.
