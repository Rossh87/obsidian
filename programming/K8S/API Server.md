All other [[Control Plane Agent]]s, as well as admin commands, pass through this agent. Human users generally interact with a cluster with a tool like `kubectl` that abstracts over the `apiserver` REST interface.  This interface is documented as an `OpenAPI` specification.  Endpoints are versioned, e.g. `/api/v1`, but note that different versions of the same object are just *projections* of the same underlying data.  In other words, different API versions represent different ways of accessing and describing data, but do **not** distinguish objects.  Objects are distinguished by their API group, resource type, namespace (if applicable), and name.

API server functionality is segregated into API groups, some of which can be activated or deactivated.  That is, not all API endpoints will be available unless they are specifically activated.

It is the only agent that directly reads and writes to key-value store managed by [[etcd]]

K8S supports defining custom API servers, in which case the main API server agent becomes a proxy, passing incoming calls to other APIs based on custom routing rules.

Cluster admin is managed through the API server.  There are 3 ways to interface with the cluster:
1. via `kubectl` CLI
2. via `HTTP`-based API. K8S api server requires communication be authenticated.  Running `kubectl proxy` will start a reverse-proxy service on the local machine.  Request to the appropriate port will be proxed to Kube api, with needed credentials.  Alternatively, requests can manually include a `Bearer: token` header or use a certificate for authentication.
3. via dashboard.  Start with `minikube dashboard` (if you have `minikube`)...