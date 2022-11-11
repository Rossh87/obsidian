K8S does not itself provide the ability to build or run containers.  This functionality has to be provided through a *container runtime*.  Docker is an example.  Some other choices are *containerd*, *CRI-O*, and Mirantis runtime/Docker Enterprise Edition.

All nodes, worker and control plane, require a container runtime.

[Since version 1.23](https://kubernetes.io/blog/2020/12/02/dont-panic-kubernetes-and-docker/), Docker is no longer a supported container runtime.  However, containers built with Docker are compliant with the Open Container Initiative, and can be run on any runtime that interfaces with this initiative.  This is possible because Docker uses *containerd* under the surface; the rest of the Docker stack provides better UX than interfacing with container interface directly.