Pods are impermanent resources in a cluster.  A pod may fail or be destroyed, and a replacement pod spun up with a different IP address.  A K8S service is an abstraction over a pod or pods with a particular purpose that allows consumers to reference the service without knowing details of which pods are running, or where. Services can also set policies to control how pods are accessed.

One way of defining a microservice is as a group of one or more pods that offer some functionality, running behind the abstraction of a service.

The most common way of associating a Service with a pod or pods is by setting a [[Selector]] in the service configuration object.  The appropriate controller will then automatically associate/dissociate pods that go up or come down with the service, provided the pods' `label` correspond to the service's selector.

In some cases we wish to expose some functionality through a service that is not handled by pods in our own cluster.  In that case, we can manually create an [[EndpointSlice]] that defines IP addresses, ports, and protocols that we wish to associate with the service.

EndpointSlices are considered 'slices' because they can define more than one endpoint.

Services are managed on each node by the [[kube-proxy]] agent.  `kube-proxy` does its thing by listening to the [[API Server]] (on control plane).