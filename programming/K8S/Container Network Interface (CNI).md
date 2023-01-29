- [ ] Bridges the gap between the [[Container Runtime]] and individual containers or [[Pod]]s.  A CNI is needed for K8s to work, but not specific to K8s.  It can be used with most popular container runtimes with or without K8s.

The interface provided by CNI-compliant container networking solutions allows the container runtime to be agnostic about the networking specifics of the host.  The container runtime communicates with the CNI via a small number of verbs (e.g. `add`, `del`), along with a JSON-encoded text file that includes details about the request.

The CNI project includes the CNI specification as well as a few actual plugins, and is maintained by CNCF.

The spec is divided into 5 sections:
	1. Network Configuration format
		1. config is a JSON object in a static file on the host (usually, though not required by spec)
		2. spec requires a small number of keys, reserves a few, and allows plugins to read other unspecified fields that may be in the config
		3. `plugins` required key is an array of plugin configuration objects.  CNI plugins are generally narrow in scope, so a single network config might need several to meet its needs.
	2. Execution protocol
		1. container runtime expects plugins to be invoked via their respective binaries
		2. plugins receive configuration (constant) via `stdin` and parameters (invocation-specific) as environment variables, and return a JSON-encoded result on `stdout` on success, or an err on `stderr` on failure.