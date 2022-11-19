A recommended way to deploy a self-healing, multi-pod service.

A ReplicaSet definition uses [[Selector]]s to decide what pods to spin up.

Note that pods remain independent, event though they are identical--the [[Scheduler]] can add pods to any node to satisfy the requirements of the ReplicaSet.  The pods need not all be on the same node.

ReplicaSets can be used independently as pod controllers, but it is recommended to use [[Deployment (object)]] instead.  Deployments have more features.