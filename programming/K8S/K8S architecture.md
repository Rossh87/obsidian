At a high level, K8S is a cluster of compute systems categorized by distinct roles:
1. One or more [[Control Plane Node]]s
2. One or more [[Worker Nodes]]s (optional, but recommended)

Deployment infrastructure can range in complexity from a single host with all control plane and worker components installed, to multiple control planes on multiple hosts, each with external [[etcd]] topology, and multiple worker nodes.