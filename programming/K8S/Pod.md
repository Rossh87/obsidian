A pod is just a group of containers that work together to create a single application or service.  Think of a `docker-compose` file.

Pods are the smallest workload unit in K8S.  The pod is responsible for ensuring logical container group gets the same pod IP, and has access to the same volumes, external storage, etc.

Pods themselves are dumb.  They depend on operators/controllers for fault tolerance, spin up/down, replication, etc.  However, they can still be defined as standalone objects, without an operator.  When this is the case, the workload will be evaluated by the [[Scheduler]], and the container(s) will be started by the selected node.