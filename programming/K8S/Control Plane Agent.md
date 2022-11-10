Control plane agents are services running on the cluster's control plane.  Different agents have different responsibilities.  Important control plane agent types are:
1. API Server (*kube-apiserver*)
	1. All administrative tasks pass through this agent
	2. Only agent that directly reads and writes to key-value store
	3. Uses RESTful calls
	4. K8S supports defining custom API servers, in which case the main API server agent becomes a proxy, passing incoming calls to other APIs based on custom routing rules
2. Scheduler (**kube-scheduler**) 
	1. Assigns workload objects to nodes (typically worker nodes)
	2. Uses cluster state it requests from API server to decide which node is the best candidate for the workload based on the current resource usage of each node
	3. Supports configuration and customization through policies, plugins, and profiles
3. controller managers
	1. watch-loop process that compares cluster's desired state (from config objects) with actual state (from control plane key-value store) 
	2. takes corrective action if there is mismatch
	3. **kube-controller-manager** is responsible for K8S state itself: dealing with unavailable nodes, ensuring container/pod counts are correct, creating endpoints and tokens, etc.
	4. **cloud-controller-manager** is responsible for interfacing with cloud providers when nodes become unavailable, managing storage volumes from a cloud provider and network duties like load balancing and routing.
4. Key-value store (see [[etcd]])