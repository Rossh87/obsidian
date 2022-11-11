https://kubernetes.io/docs/concepts/services-networking/service/

*kube-proxy* is responsible for networking rules of its [[Node]].  It forwards connection requests to containers in pods, and is resonsible for [[TCP]], [[UDP]], and [[SCTP]] forwarding.  Users can set custom forwarding rules via *kube-proxy*.

Kube-proxy is responsible for managing `iptables` and granting pods connectivity to the public internet through [[K8S/Service]].

`kube-proxy` can run in different modes.  The default mode is `iptables` proxy mode. In this mode, `kube-proxy` updates the host's `iptables` for every service and endpoint, such that outgoing requests to the `clusterIP` and `port` of a service are routed to one of the endpoints associated with that service.  Notice that in this mode, outgoing requests from clients on a given node are never directly touched by `kube-proxy`.  They only interact with the kernel's `iptables`.  This means that `kube-proxy` cannot do error handling.  Instead, `kube-proxy` can use [[Readiness probes]] to ensure it does not add unresponsive backends to `iptables`.

IPVS (IP virtual server) mode works similarly to `iptables` mode, but with a virtual IP server that is more performant and offers additional features for balancing traffic to backend pods (defined in Service's Endpoints).  The host must have IPVS features installed and running before starting `kube-proxy` in `IPVS` mode.  Otherwise, `kube-proxy` falls back to `iptables` mode.