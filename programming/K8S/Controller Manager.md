
watch-loop process that compares cluster's desired state (from config objects) with actual state (from [[etcd]], via [[API Server]]) 

takes corrective action if there is mismatch

**kube-controller-manager** is responsible for K8S state itself: dealing with unavailable nodes, ensuring container/pod counts are correct, creating endpoints and tokens, etc.

**cloud-controller-manager** is responsible for interfacing with cloud providers when nodes become unavailable, managing storage volumes from a cloud provider and network duties like load balancing and routing.