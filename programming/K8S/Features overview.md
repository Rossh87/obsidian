1. Automatic bin packing: automatically schedules containers based on specified resource constraints and availability.  Basically, we want to use the smallest amount of resources possible for a given workload.
2. Extensibility (modular and pluggable): features can be added to clusters without modifying K8S source code.
3. Self-healing: K8S runs health checks on containers.  It restarts dead containers, and prevents traffic from being routed to misbehaving containers.
4. Horizontal scaling: containers are added removed manually or based on metrics/policies.
5. Service discovery and load balancing: K8S assigns IPs to individual containers, but groups them behind a single DNS name so that it can load-balance incoming requests to all containers in the set.
6. 