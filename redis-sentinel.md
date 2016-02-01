**Redis sentinel** allows a high-availability, clustered deployment of redis utilizing a similar strategy to that employed by other clustered systems such as MongoDB and Elasticsearch.

Official docs: http://redis.io/topics/sentinel

Sentinel itself is a clustered service, and is run as a **separate process** using a special configuration file. Its job is strictly to monitor the specified master node of a redis cluster and reconfigure remaining nodes in case of a failure. It can be, and often is, run on the same server alongside Redis itself, but does not have to be. There is no need to specify slaves; they are discovered automatically.

Here is an example configuration file:

    sentinel monitor mymaster 127.0.0.1 6379 2
    sentinel down-after-milliseconds mymaster 60000
    sentinel failover-timeout mymaster 180000
    sentinel parallel-syncs mymaster 1

Line by line:

`sentinel monitor mymaster 127.0.0.1 6379 2` Monitor a redis master node with the name of `mymaster`, running at 127.0.0.1 on port 6379, with a quorum of 2.  
`sentinel down-after-milliseconds mymaster 60000` Consider it down after 60 seconds.  
`sentinel failover-timeout mymaster 180000` If the failover does not succeed, wait 180 seconds before trying to failover again.  
`sentinel parallel-syncs mymaster 1` When a new master is elected, only sync 1 node at a time.  

If the master node becomes unavailable, every other sentinel will send an `SDOWN` ("subjective down") message. If a quorum of reachable redis sentinels (in the above case, two) agree that the master is unreachable, an `ODOWN` ("objective down") message is sent which causes the "leader" sentinel process to begin a majority vote to select a new master, after which all sentinel configurations will be rewritten to reflect the new master. The `SDOWN` and `ODOWN` messages can be subscribed to. If the leader is on the same node that is missing, a new leader is elected before failing over.

When the missing node becomes available again, sentinel will recognize this and reconfigure it as a slave. Any writes that were sent to this master (as it may have simply been in a network partition) will be discarded.

It can be easy to conflate the terms "master" and "leader". Understand that "master" refers to `redis-server`'s role in replication, while a "leader" is strictly a sentinel concept. 