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

1. Step1:-Install Pacemaker and Corosync On each node, install the Pacemaker and Corosync packages

```
sudo yum update
sudo yum install pacemaker
sudo yum install corosync
```

2. Step 2: Configure Corosync Edit the Corosync configuration file on each node:

```
sudo nano /etc/corosync/corosync.conf
```
Here’s a basic configuration example for a two-node cluster:

Replace node1_IP and node2_IP with the actual IP addresses of your nodes.

```
totem {
    version: 2
    secauth: off
    cluster_name: my_cluster
    transport: udpu
}

nodelist {
    node {
        ring0_addr: node1_IP
        nodeid: 1
    }
    node {
        ring0_addr: node2_IP
        nodeid: 2
    }
}
quorum {
    provider: corosync_votequorum
}
```

3. Step 3: Start Corosync Start the Corosync service on each node:
```
sudo systemctl start corosync
```

4. Step 4: Enable Corosync at Boot Ensure Corosync starts automatically at boot:
```
sudo systemctl enable corosync
```

# Configuring Pacemaker
Step:5 & 6
```
sudo systemctl start pacemaker 
sudo systemctl start pacemaker 
```

# Creating Resource:
7. Step:7 
Create a Resource Agent Pacemaker manages resources using resource agents. To create a simple resource agent for a virtual IP (VIP) address, create a file like vip.sh:

```
sudo nano /usr/local/bin/vip.sh && chmod +x /usr/local/bin/vip.sh
```
Add the following content and make the script executable:
```
#!/bin/bash
/sbin/ifconfig eth0:0 $1 netmask 255.255.255.0 up
```

8. Step:8 Create a Resource Now, create a Pacemaker resource for the VIP. On one of the nodes, run:

Replace VIP_IP with the virtual IP address you want to use.
```
sudo crm configure primitive vip ocf:heartbeat:IPaddr2 params ip="VIP_IP" nic="eth0" cidr_netmask="24" op monitor interval="10s"

```

9. Step 9: Create a Resource Group Create a resource group that includes the VIP resource:
```
sudo crm configure group vip_group vip
```

# Testing Failover
Simulate Node Failure To test the cluster, simulate a node failure by stopping the Corosync service on one of the nodes:

```
sudo systemctl stop corosync
```
Check the status of the cluster on the remaining node:
```
sudo crm status
```
You should see that the VIP has moved the serviving node



==============

ref : Linux Nginx Set-up
https://medium.com/@christopher.suffi/how-to-set-up-a-pacemaker-cluster-for-ha-linux-os-4021251a80d8

using cluster HANA:-
https://medium.com/@christopher.suffi/using-pacemaker-cluster-for-sap-hana-debe16c74219