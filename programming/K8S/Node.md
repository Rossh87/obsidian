https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-intro/#:~:text=A%20Node%20is%20a%20worker,the%20Nodes%20in%20the%20cluster.

A node is the virutal identity K8S assigns to the systems in the cluster.  The system can be a bare metal machine, a VM, or a container.  

Nodes are managed by [[kube-proxy]] and [[kubelet]], and must also include a container runtime.

Clusters generally include a control plane node and at least one worker node, but a single-node cluster can also be bootstrapped.