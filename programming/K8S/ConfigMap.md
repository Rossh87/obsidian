K8s API object that stores configuration, unsurprisingly.  Allows container images to be more generic/configurable.  Create via CLI or a `yaml`, like most other objects.

Containers can consume all the key-value pairs from a config map as environment variables by setting `envFrom` in the container definition, or specific key-value pairs by setting `env` and `valueFrom` in the container definition.  Note a container can consume more than one `ConfigMap`.

A `ConfigMap` can also be created as a named volume and mounted onto a path specified by the container definition.  Each key then becomes a file name at the mount path, and the value for each key will be the contents of the respective file.