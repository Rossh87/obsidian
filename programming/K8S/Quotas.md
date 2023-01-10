Quotas can limit the amount of cluster resources that can be consumed by a single [[Namespace]].
- `ComputeResourceQuota` restricts CPU consumption.  
	- This is measured in fractions of time that a core is occupied
	- E.g. `.1` means 'up to 10% of the active time of a single core' 
	- `100m`, or 100 millicores, is equivalent to the above
 - `StorageResourceQuota` limits the sum of the storage totals for all request storage resources, e.g. `PersistentVolumeClaim`s
 - `ObjectCountQuota` limits the number of a given type of object

`LimitRange` objects give more fine-grained control over resource usage per object.  `LimitRange`s can also set limits relative to request volume.