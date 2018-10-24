# Kubelet Design
Kublet interacts with the host underlying Container runtime vai the CRI (Container Runtime Interface), which is any of -
* docker
* rkt
* runC - a cli tool for spawning and running containers which meet OCI specification
* any OCI (Open Container Initiative) runtime-spec implementation
  * OCI includes two specifications
    * Runtime Specification - which defines how to access a [filesystem bundle](https://github.com/opencontainers/runtime-spec/blob/master/bundle.md) unpacked on disk
    * Image Specification - defines how to create an OCI image



# Securing K8s

* Setup k8s cluster to use TLS between nodes.
* Can use "Let's Encrypt" as the CA (Certificate Authority) to manage certificates - revoke, request and renew 
* The certificate management agent resides on the web server.
* To begin certificate requests, the CA verifies the web server controls the domain. This is done by presenting the agent with the choice of responding to 2 [challenges](https://letsencrypt.org/how-it-works/)-
  * provision a DNS record under the domain *'example.com'* or
  * provision a resource under the URI *'http.example.com'*
* If deploying k8s on AWS, *Route53* can be used as the DNS responder.

# Custom Controllers
* https://engineering.bitnami.com/articles/a-deep-dive-into-kubernetes-controllers.html

# Useful References

https://caylent.com/50-useful-kubernetes-tools/
