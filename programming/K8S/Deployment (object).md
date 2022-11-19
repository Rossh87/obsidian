Declaratively manage [[Pod]]s and [[ReplicaSet]]s.  `spec` field defines the desired state of the deployment object that [[Controller Manager]] will compare with the current state and handle any needed changes.  

Revision history is a key feature of Deployments.  Suppose a Deployment defines a ReplicaSet with 3 replicas of one pod.  The pod is a single container, an image at `v1`.  Eventually, we may want to use image `v2` instead.  In this case, the Deployment at `v1` will snapshot that state, then seamlessly rollout a new ReplicaSet of pods with the updated container version.  The state of the Deployment with the new ReplicaSet is considered `Revision 2`. Once this rolling update is complete, the Deployment will show both ReplicaSet A, scaled to 0 pods, and ReplicaSet B, scaled to 3 pods.

Dynamic changes like scaling and labeling do not trigger a rolling update, and are not considered new revisions.

Deployments can be rolled back to any previous revision.  Setting `revisionHistoryLimit` controls how many consecutive revisions are saved; default is 10.  Each stored [[ReplicaSet]] revision takes up space in [[etcd]] and clutters output of `kubectl get rs`.