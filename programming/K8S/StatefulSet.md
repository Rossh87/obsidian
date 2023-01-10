Similar to a [[ReplicaSet]], but [[Pod]]s have a persistent identity.  A `StatefulSet` can also handle details like ordered deployment/inter-pod dependencies.  They are useful for the following:
- Stable, unique network identifiers, i.e. guarantees of reaching a *specific* pod when requesting a resource
- Stable, persistent storage
- Ordered, graceful deployment and scaling, e.g. multi-container pods whose container startup order matters
- Ordered, automated rolling updates

Pods created by a `StatefulSet` are programatically named based on their ordinal identity plus the `StatefulSet` name.  A [[Headless Service]] can be used to expose each unique pod identity to the rest of the cluster via cluster DNS.