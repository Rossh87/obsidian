Store arbitrary key-value data about any object, e.g. version info, pointers to logs or other objects, descriptions, etc.

Annotations are not used by K8s internals for to identify or select objects, but will be displaced with object descriptions from `kubectl describe`.