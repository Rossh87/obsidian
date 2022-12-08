Caveat: the below only applies to Linux, though other platforms probably are similar.

Container networking is based on `namespaces`.  `Namespaces` are a feature for isolating kernel resources and processes from one another (sandboxing), and are available for different types  of resources, e.g. time, user ids, mounts, etc.  Here, we're most interested in network namespaces.

Container network isolation is achieved by creating a `veth` pair with one end in the `root` namespace and the other end in the container namespace.  In `Docker`, the `root` end of the `veth` is then attached to a bridge network interface.  `Docker` creates a default bridge, but it is recommended to specify a custom bridge network in production, as custom networks offer more features, most notably automatic `hostname` resolution in containers.

Because each container is in its own `namespace`, network interfaces that are not connected to the same bridge network as the container are invisible from within the container.  However, the container is *not* invisible from the `Docker` host: to prove this, find the IP address of the network device in the container, and `curl`/`ping` it from the `Docker` host.  The container will respond normally.

*Port mapping* is really just a NAT rule in the `iptables` of the host: mapping `0.0.0.0:8080 -> 80/tcp` (i.e. port 8080 on the host to 80 in the container) creates an `iptables` NAT rule that translates all incoming traffic on `0.0.0.0:8080` to `<container-ip>:80`.  Because the `container-ip` is on a subnet that matches the `Docker` bridge network, the bridge can resolve the container's ip address and the traffic reaches the correct process running in the container.