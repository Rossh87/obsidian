In this model, the [[API Server]] compares *attributes* of an incoming api request (e.g. `user`, `namespace` ) with predefined [[Policy]] objects.  If there is a match, the request `api server` services the request.

To enable ABAC, start the API server with `--authorization-mode=ABAC`

 c.f. https://kubernetes.io/docs/reference/access-authn-authz/abac/