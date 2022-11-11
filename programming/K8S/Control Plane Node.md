The most important [[Node]] in a K8S cluster, responsible for doing the actual orchestration.  Users configure their cluster by interacting with the control plane, via CLI, API, or web-based GUI.

The control plane must never go down.  To help with fault tolerance, multiple control planes can be run in replica mode.  Only one CP is in control at a time, but the state of the active control plane is propagated to the replica(s) so that they can take over if needed.

The CPN provides the running environment for [[Control Plane Agent]]s, each of which has distinct responsibilities in managing the cluster.

The state of the cluster is persisted in a dedicated, distributed key-value store.  This store can be part of the CPN (stacked topology), or on the control plane's dedicated host (external topology).  External topology helps protect the data by decoupling the data storage from other control plane agents.  However, in replica setups with external topology, data store replication to replica hosts must be handled separately from control plane replication/propagation, leading to extra hardware costs and complexity.