Node agent, or *kubelet*, serves as the bridge between the control plane (via [[API Server]] aganet) and the container runtime of an individual worker.  It also monitors the health and resources of the pods.

Kubelet can interact with any container runtime that implements the Container Runtime Interface.  A shim between the lowlevel runtime and kubelet that implements the CRI is required.  E.g. `cri-containerd` provides the CRI for runtime `containerd`, CRI-O enables any Open Container Initiative-compatible runtime to work with *kubelet*, etc.

Kubelet and the shim interact via gRPC.