- [ ] Bridges the gap between the [[Container Runtime]] and individual containers or [[Pod]]s.  A CNI is needed for K8s to work, but not specific to K8s.  It can be used with most popular container runtimes with or without K8s.

The interface provided by CNI-compliant container networking solutions allows the container runtime to be agnostic about the networking specifics of the host.  The container runtime communicates with the CNI via a small number of verbs (e.g. `add`, `del`), along with a JSON-encoded text file that includes details about the request.

The CNI project includes the CNI specification as well as a few actual plugins, and is maintained by CNCF.

The spec is divided into 5 sections:
	1. Network Configuration format
		1. config is a JSON object in a static file on the host (usually, though not required by spec)
		2. spec requires a small number of keys, reserves a few, and allows plugins to read other unspecified fields that may be in the config
		3. `plugins` required key is an array of plugin configuration objects.  CNI plugins are generally narrow in scope, so a single network config might need several to meet its needs.  The `type` field must be the name of an executable binary accessible to the container runtime. 
	2. Execution protocol
		1. container runtime expects plugins to be invoked via their respective binaries
		2. plugins receive configuration (constant) via `stdin` and parameters (invocation-specific, includes the 'verb' for the plugin) as environment variables, and return a JSON-encoded result on `stdout` on success, or an err on `stderr` on failure.
	3. Execution of Network Configs
		1. It is the responsibility of the container runtime to create and cleanup the contaienr's network isolation domain (e.g. network namespace).
		2. An 'attachment' is described by the tuple `[containerID, interfacename]`
		3. Plugins must tolerate parallel execution for multiple attachments, but *not* for the same attachment
		4. Each plugin defined in `plugins` field of the net config object is called in sequence (forward for `ADD`, backward for `DEL`.  Plugins will receive an object with the result of some previous plugin call or calls; the specifics of what the previous result contains depends on the verb.
		5. The container runtime must pass the appropriate plugin configuration object from the `plugins` field of the network config, with some additional fields added, to the plugin invocation on `stdin`.  Most notably, the `runtimeConfig` must be added to describe the union of capabilities offered by the plugin and those requested by the runtime.
	4. Plugin delegation
		1. CNI plugins can delegate tasks to other plugins.  The CNI plugin can call the delegate plugin from an executable binary, and is expected to pass along configuration that it (the CNI plugin received), as well as piping any errors to its own `stderr`.
	5.  Result Types (specifies format of `success`, `error`, and `version` objects that plugin binaries must produce on invocation)