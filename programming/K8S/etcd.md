Open source key-value data store used for storing K8S cluster state, and also configuration details like secrets, subnets, ConfigMaps, etc.

Distributed, strongly-consistent.

Append-only: data is never modified, only added.  Obsolete data is periodically compacted or shredded to conserve system resources.

[[API Server]] is the only [[Control Plane Agent]] able to access *etcd* directly.

The CLI management tool *etcdctl* can be useful for managing single instances of *etcd*, which is a common configuration in dev environments.  However, in production/QA environments, it is important that *etcd* be run in a high-availability configuration with replicas for failure recovery.

*etcd* can be configured as either a *stacked* topology or an *external* topology.  In a stacked topology, *etcd* runs on the same [[Node]] as the rest of the [[Control Plane Node]]s, and shares the node's resources with them.  In an external topology, *etcd* is configured to run on a separate host or hosts from the rest of the control plane nodes, giving extra resiliency.

Both topologies support high-availability configs, i.e. running several *etcd* instances in replica mode.  Nodes use the [raft consensus algorithm](https://web.stanford.edu/~ouster/cgi-bin/papers/raft-atc14) to elect a leader node for managing data replication.  Any node can become the leader at any time, making the group resilient to failure or one or more group members.