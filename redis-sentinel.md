**Redis sentinel** allows a high-availability, clustered deployment of redis.

Sentinel is run as a **separate process** using a special configuration file, and monitors the specified master node of a redis cluster. The name of the master node is provided in a configuration file (usually `sentinel.conf`).

If this node becomes unavailable, every other sentinel will send an `SDOWN` ("subjective down") message. If a quorum (configurable) of reachable redis sentinels agree that the master is unreachable, an `ODOWN` ("objective down") message is sent which causes the "leader" sentinel process to begin a majority vote to select a new master, after which all sentinel configurations will be rewritten to reflect the new master. These messages can be subscribed to. If the leader is on the same node that is missing, a new leader is elected before failing over.

When the missing node becomes available again, sentinel will recognize this and reconfigure it as a slave. Any writes that were sent to this master (as it may have simply been in a network partition) will be discarded.

It can be easy to conflate the terms "master" and "leader". Understand that "master" refers to `redis-server`'s role in replication, while a "leader" is strictly a sentinel concept. 

http://redis.io/topics/sentinel