Namespaces satisfy the need for multi-tenant infrastructure.  Multiple teams, project, or users can operate on the same cluster, partitioned into namespaces.

K8S creates four default namespaces:
1. `kube-system` houses objects that K8S itself needs for its own internal use--mostly the [[Control Plane Agent]]s.
2. `default` is where user-defined objects end up if a specific namespace for them is not specified.  It is recommended to add objects to specific namespaces, not `default`.
3. `kube-public` is unsecured, meant for exposing non-sensitive info about the cluster.
4. `kube-node-lease` holds objects used for tracking [[Node]] heartbeat data.

Object names within a single namespace have unique names, but uniqueness across the cluster, i.e. in different namespaces, is not required.

[[Resource quotas]] can limit the system resource consumption of a namespace.  [[LimitRanges]] limit resources consumed by containers.