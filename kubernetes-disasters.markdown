# One or more Nodes Die

The master loses the ability to communicate with some nodes and attempts to reschedule the work after 5 minutes if the nodes have not returned. The containers running on the nodes will continue to run but not be routed to via k8s. Once the nodes return to service the replication controller will ensure the proper number of containers are running across the newly unified cluster (probably killing some containers) and load balance over all of the containers again.

# network fault

Same as node(s) dying. The master loses the ability to communicate with some nodes and attempts to reschedule the work after 5 minutes if the nodes have not returned. The containers running on the nodes will continue to run but not be routed to via k8s. Once the nodes return to service the replication controller will ensure the proper number of containers are running across the newly unified cluster (probably killing some containers) and load balance over all of the containers again.

# Master VM Shuts down unexpectedly

Without employing a [High Availability](http://kubernetes.io/v1.1/docs/admin/high-availability.html#running-the-podmaster) strategy for the master, the cluster will be down for the duration of the master down time. It's possible that the nodes may still respond as long as nothing occured to knock them off kilter (like etcd data being unavailable and the nodes killing the containers).

Simply turning on the master VM should restore cluster functionality within minutes assuming no other issues (like etcd data corruption).

# Etcd Dies

If the Etcd process somehow dies and isn't restarted internal state might get wonky but simply rebooting the master should fix the issue (assuming it was photons that messed up the ram as opposed to a misconfiguration somewhere).

# Etcd Data gets lost/corrupt

The cluster is in trouble. If possible, recover a backup. Otherwise, all the work needs to be redeployed to the cluster after flushing etcd.

# Rude Down Scaling

This is the scenario in which we kill nodes on purpose never planning to return them to service. This scenario is very similar to the case of nodes dying, except they will never return to the cluster so the workload on them will get rescheduled to the other nodes after 5 minutes. Because the node was killed the containers running on it will be dead.