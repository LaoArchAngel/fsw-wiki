# One or more Nodes Die

The master loses the ability to communicate with some nodes and attempts to reschedule the work after 5 minutes if the nodes have not returned. The containers running on the nodes will continue to run but not be routed to via k8s. Once the nodes return to service the replication controller will ensure the proper number of containers are running across the newly unified cluster (probably killing some containers) and load balance over all of the containers again.

# network fault

Same as node(s) dying. The master loses the ability to communicate with some nodes and attempts to reschedule the work after 5 minutes if the nodes have not returned. The containers running on the nodes will continue to run but not be routed to via k8s. Once the nodes return to service the replication controller will ensure the proper number of containers are running across the newly unified cluster (probably killing some containers) and load balance over all of the containers again.

# Master Dies

# Etcd Dies

# Etcd Data gets lost

# scale up

# Scaling Down

#Involuntary Scaling Down

This is the scenario in which we kill nodes on purpose never planning to return them to service. This scenario is very similar to the case of nodes dying, except they will never return to the cluster so the workload on them will get rescheduled to the other nodes after 5 minutes. Because the node was killed the containers running on it will be dead.