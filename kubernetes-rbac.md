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
