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