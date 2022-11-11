All other [[Control Plane Agent]]s, as well as admin commands, pass through this agent.

It is the only agent that directly reads and writes to key-value store managed by [[etcd]]

Uses RESTful structure.

K8S supports defining custom API servers, in which case the main API server agent becomes a proxy, passing incoming calls to other APIs based on custom routing rules.