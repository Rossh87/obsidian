Operators designed to manage node agents.  DaemonSets enforce a constraint of one pod per node.  In contrast, [[ReplicaSet]]s and [[Deployment (object)]]s have no control over the nodes their pods are run on--that is delegated to the scheduler.  No `replicas` field is required for a DaemonSet, one pod will be automatically created and added to each node.

Commonly used to collect monitoring data, or to run K8S agents like `kube-proxy`, which are required on every node.

Pods in a DaemonSet are placed by the controller, not by the [[Scheduler]].  When new nodes join the cluster, a pod from the DaemonSet are automatically added to the node.  When the node leaves, its pod is garbage collected.

It is possible to have pods in a DaemonSet added only to certain nodes by leveraging [[nodeSelectors]], [[Node Affinity Rules]], [[Taints]], and [[Tolerations]].