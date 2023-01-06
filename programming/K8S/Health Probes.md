[[Pod]] definitions can include instructions to [[kubelet]] for determining if the pod is healthy (`livenessProbe`), or if it is ready to serve traffic (`readinessProbe`).  

The check can be done by executing a command and expecting a non-zero exit code, sending an HTTP request to a predefined route and expecting a success code, or by trying to open a TCP connection to the container on a specified port.

If the number of failed liveness checks crosses the predefined threshold (3 by default), `kubelet` will restart the pod.  If readiness probes fail, [[K8S/Service]]s will not direct traffic to the pod.