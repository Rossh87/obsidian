Both `NodePort` and `LoadBalancer` [[K8S/Service]]s are needy, and `LoadBalancer` resources are expensive. An `Ingress` object is an abstraction that sits between a `Service` and the outside world, and abstracts some of the details of managing the service.  An `Ingress` allows us to do internal, name-based routing, without clients needing to follow the details of [[Node]] or `Service` IPs.  The `Ingress` passes the incoming request to the specified `Service`, and the `Service` forwards it to one of its [[Pod]]s.

Routing can be specified as *name-based virtual hosting*, where requests are matched to `Services` via `host` header/subdomaining, or as a *fanout*, where requests are matched based on the request path, e.g. `domain.com/pathone` & `domain.com/path2`.

The `Ingress` itself does not actually forward requests, it only defines routing rules.  The actual routing is handled by an `IngressController`, which reverse-proxies incoming requests based on rules defined in the `Ingress`.

K8s does not include an `IngressController`.  There are many third-party ICs available from common sources like Nginx, Istio, etc.