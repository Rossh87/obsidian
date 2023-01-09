Object for storing sensitive information.  Note that by default Secret info is stored in plain text in [[etcd]].  Encrypted secret storage can be enable at the [[API Server]] level.

Options for exposing all or some of the contents of a Secret to app code in a [[Pod]] are the same as those for a [[ConfigMap]].