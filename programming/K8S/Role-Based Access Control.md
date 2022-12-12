In this model, named [[Role]] objects are defined for individual namespaces.  The `Role` specifies a list of resource types, and a list of verbs that can be performed on those resources in the namespace (unless it is a `ClusterRole` object).  A [[RoleBinding]] object can then link a subject (e.g. a user) to a `Role`.  A subject can only perform an action inside of a namespace if the subject is linked by a `RoleBinding` to a `Role` within that namespace that includes the desired action.

To enable ABAC, start the API server with `--authorization-mode=ABAC`.  

 c.f. https://kubernetes.io/docs/reference/access-authn-authz/rbac/