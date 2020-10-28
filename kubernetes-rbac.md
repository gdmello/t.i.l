# v1.6
Role based access control is implemented using -
* `Role` - which consists of rules, always addendum. Grants access to resources within a namespace only
* `ClusterRole` - applies to entire cluster. Grants access to resources within a cluster.

Users are given access to kubernetes resources via role bindings
* `RoleBinding`
  * Gives a user access to a Role for resource access within a namespace
  * Can also give a user access to a ClusterRole, for resources in the ClusterRole with the `RoleBinding` namespace
* `ClusterRoleBinding`
  * Gives a user access to a ClusterRole to access cluster wide resources.

# v1.16.x
## Access A Cluster Via A Certificate
In order to access a Kubernetes cluster externally, certificates can be used to identify a user. The basic steps are:
1. Create a Certificate Signing Request (CSR) for the user 
1. Generate a Certificate for the user via one of these ways:
    1. Create the CSR in the cluster as a Kubernetes Resource, approve and sign this request with the Cluster Root Certificate Authority (CA), or
    1. Sign the request locally, which needs access to the Cluster root CA file and the root CA private key file.
1. Assign a cluster role to this account, to authorize the user to access certain resources in the cluster

Sources:
* [Managing TLS in a cluster](https://v1-16.docs.kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/)
* [Granting user access to your Kubernetes cluster ](https://www.openlogic.com/blog/granting-user-access-your-kubernetes-cluster)
* [Configure RBAC access in your Kubernetes Cluster ](https://docs.bitnami.com/tutorials/configure-rbac-in-your-kubernetes-cluster/)
