A 'highly available' system is simply a system that offers users the expected experience in terms of features and latency 100% of the time, or as close to 100% of the time as possible.

2 helpful metrics for availability are:
1. Mean Time Between Failures (MTBF) (how often do failures happen)
2. Mean Time To Repair (MTTR) (how long does it take for things to go back to normal)

MTTR can be subdivided into Time to Diagnose (how long before a problem is noticed and understood well enough to start fixing) and Time to Repair (how long to devise, implement, and deploy a fix).

Availability is often described as a percentage: within some arbitrary time unit (day, month, year), divide the time the system _is_ operating as expected by the time the system _should_ be operating as expected if it were perfect. The resulting percentage is considered 'availability'. This is often described as 'nines': a system running at '3 nines' is available 99.9% of the time, or 1.44 minutes of downtime per day. 4 nines = 8.6 seconds of downtime per day. 

Higher percentages require more automated detection and other strategies like automatic rollbacks.