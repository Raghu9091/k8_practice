# Pacemaker in linux : ensuring the heartbeats of high availability services

Pacemaker is a high-availability cluster resource manager. It works to ensure that the cluster services remain available even when there are failures, either in the hardware or software. 

In essence, if one server in a cluster faces an issue, Pacemaker will ensure that its responsibilities are instantly picked up by another server to minimize service disruptions.

Pacemaker and Corosync are open-source tools that allow you to create a high-availability cluster on your Ubuntu servers.

## key components

**Cluster:** A group of servers working together to ensure high availability of services. These servers constantly communicate to monitor each other’s health.
**Resources:** These are the services that the cluster manages. Examples include virtual IPs, databases, file systems, and more.
**Nodes:** Individual servers within the cluster.

=====================================
# How does pacemaker work:

* Pacemaker works hand in hand with another tool called Corosync. 
* Pacemaker is responsible for managing the cluster’s resources (like starting or stopping services)
* Corosync handles cluster membership and messaging. Think of Corosync as the messenger that notifies Pacemaker when a node has failed.

## the due ensures:
1. Service Failover:- If a service fails on one node, it can be automatically migrated to another node.

2. Service Recovery: Restarting services that have failed.

3. Node Failover: If an entire server (node) fails, its services are migrated to a remaining healthy server.

Interview Conclussion:
Pacemaker, in the Linux world, plays a critical role in ensuring that services are always up and running. When paired with tools like Corosync, it provides a robust solution for maintaining high service availability in clustered environments.

=========================================

# Set-up & configure

**High availability** clustering involves grouping multiple servers (nodes) together to provide redundancy for critical services. 

If one node fails, another takes over seamlessly, ensuring continuous service availability.

