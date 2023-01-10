A `Job` object is responsible for creating and monitoring one or more [[Pod]]s to complete a specific tasks.  A job is considered to have successfully completed when its pod or pods terminate successfully.  Note that when a job completes, the job and associated pods are usually *not* deleted, to allow continued access to logs.

Jobs can run start multiple pods to work on tasks in parallel.  Like all concurrency, this introduces extra requirements.

Depending on restart policy and other configuration, a job can fail at either the container or the pod level.  What constitutes a failure, and how many failures to tolerate before giving up, is configurable.

A `CronJob` recurs at an interval specified in its object definition.  K8s tries to execute a `CronJob` once per schedule execution time, but there are circumstances where a `CronJob` may run 0 or more than 1 time, so `CronJobs` should be idempotent.