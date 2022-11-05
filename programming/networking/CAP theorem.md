# CAP theorem
## Consistency
**Consistency** is a guarantee that every node in the distributed system will give the same response to a query at any given time.  Because it takes time for an update to one node to propagate to other nodes in the system, the system must confirm with all other nodes before responding to queries; otherwise, clients connecting to a single node may receive out-of-date information.

## Availability
**Availability** is a guarantee that a client will receive a response even if some nodes are down.

## Partition tolerance
**Partition tolerance** is the ability of the system to operate while some nodes are down

### Incompatibility examples
A fully-consistent distributed system cannot be fully available: if some nodes are uncommunicative, it is not possible to know whether all nodes have the same state, so the system must wait for all nodes to come online before responding.

A single-node system (e.g. a traditional RDBMS) is fully consistent and available, but not partition-tolerant: since there is only a single node, if it goes down, then by definition the system cannot continue to operate.

## Limitations
In the real world, databases have important characteristics (e.g. tolerating high write volumes, ability to index specialized data types, etc.) that should influence design decisions as much or more than CAP considerations.  In particular, partions are a relatively rare occurence; a more influential consideration might be the tradeoff between latency and consistency when there is no partition****.