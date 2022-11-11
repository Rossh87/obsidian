K8S adopts the ip-per-[[Pod]] principle.  Every pod in the cluster must be able to communicate with every other pod via a unique IP address, with needing NAT (network address translation).  One motivation for this approach is it creates a smooth migration path from virtual machines to pods: VMs in a multi-host architecture already communicate with other VMs via their IP address, so this networking model makes containerizing legacy applications easier.

Containers within the same pod communicate with each other via loopback/localhost.  Port coordination between these containers is a implementation detail of the container runtime being used.  Think of Docker networks and host resolution.

Communication between pods in a cluster is usually  managed by a [[K8S/Service]].