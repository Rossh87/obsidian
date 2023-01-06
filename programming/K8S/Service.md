Note: `kubectl expose` is a shorthand for creating a service.  It is comparable to writing a `yaml` Service object definition and applying it.

Pods are impermanent resources in a cluster.  A pod may fail or be destroyed, and a replacement pod spun up with a different IP address.  A K8S service is an abstraction over a pod or pods with a particular purpose that allows consumers to reference the service without knowing details of which pods are running, or where. Services can also set policies to control how pods are accessed.

One way of defining a microservice is as a group of one or more pods that offer some functionality, running behind the abstraction of a service.

The most common way of associating a Service with a pod or pods is by setting a [[Selector]] in the service configuration object.  The appropriate controller will then automatically associate/dissociate pods that go up or come down with the service, provided the pods' `label` correspond to the service's selector.

In some cases we wish to expose some functionality through a service that is not handled by pods in our own cluster.  In that case, we can manually create an [[EndpointSlice]] that defines IP addresses, ports, and protocols that we wish to associate with the service.  Note that, unless the service is for an external resource, the **Endpoint** is a [[Pod]] IP address and port. Exposed by default, incoming requests to services (or to a [[Node]] if the Service's `type` is `NodePort`) will be proxied to other nodes until a node that has one of the endpoints listed in the service definition is found.  The endpoint is then responsible for making the reply.

EndpointSlices are considered 'slices' because they can define more than one endpoint.

Services are managed on each node by the [[kube-proxy]] agent.  `kube-proxy` does its thing by listening to the [[API Server]] (on control plane).

The `type` of service affects the way the source IP address of incoming requests to a service will be [translated](https://kubernetes.io/docs/tutorials/services/source-ip/). It also affects the way the service can be accessed:
1. `ClusterIP` (default) services are only accessible from within the cluster via the service's ip address (which can  and should be configured with a DNS module). 
2. `NodePort` services make the services available at a particular port on any node in the cluster.  When a node receives a request on the designated NodePort, it forwards it to one of the service's endpoints.  Note this changes the source ip of the request, as described above.
3. `LoadBalancer` services work with a cloud provider to provision an external load balancer for incoming requests to the service. 
4. `ExternalName` services are for interfacing with external servers via their DNS records.  Cluster DNS resolution can provide `CNAME` records for the host designated by the `externalName` field.  Note this [can cause problems](https://kubernetes.io/docs/concepts/services-networking/service/#externalname) with common protocols.

When a request is made to a service, the `iptables` of the originating node (managed by `kube-proxy`) map the service IP to an [[Endpoint]] associated with the service.  By default, the endpoint selected is random.  Ideally, we would like to select an endpoint closest to the requesting node rather than a random one, which may be on a different node, or even very geographically far away from the originating node.  To influence endpoint selection, we need to set a [[Traffic Policy]] for the service.