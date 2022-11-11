A [[Node]] in the cluster that actually runs applications.  Apps are encapsulated in [[Pod]]s: a pod is a group of one or more containers that represents all the containers needed to deliver a single service.  Pods find all the networking, compute, and storage resources the need to run on the worker node to which they are assigned.  A pod is the smallest scheduling unit in K8S.  That is, a pod can be stopped, started, or rescheduled as a single unit of work by the control plane agent [[Scheduler]].

In a multi-worker cluster, network traffic between end users and application pods is handled directly by the worker nodes.  It is not routed through the control plane.

Worker nodes include the following components:
1. [[Container Runtime]]
2. [[kubelet]] (node agent)
3. [[kube-proxy]] (proxy)
4. addons (DNS, dashboard GUI, monitoring/logging).  These are features not yet available through K8S, so they are implemented as third-party pods and services on worker nodes.