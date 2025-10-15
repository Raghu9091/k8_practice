## learn K8s set up to our environment AWS


![alt text](k8_setup_env.svg)

## K8 services

# Service Networking
Provides a stable virtual IP (ClusterIP) for a set of Pods.

# Types of Services:

* ClusterIP – Only accessible inside the cluster.
* NodePort – Exposes service on a port on every Node for external access.
* LoadBalancer – Exposes service externally using a cloud provider’s load balancer (AWS ALB/NLB, GCP LB).
* ExternalName – Maps service to an external DNS name.

![alt text](k8-service.svg)

# sidecar Containers
Sidecar containers are the secondary containers that run along with the main application container within the same Pod.

# Some typical uses of a DaemonSet are:
A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster,

* running a cluster storage daemon on every node
* running a logs collection daemon on every node
* running a node monitoring daemon on every node