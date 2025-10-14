## Learn Kebernetis

# What Is Kubernetes Helm? 

Package management is not a new concept. In Linux, package managers like YUM, RPM, or APT are essential for installing and removing packages. Node.js developers rely heavily on NPM, the Node Package Manager (NPM), which has thousands of packages that can do virtually anything in a Node.js environment.

1. Helm is a package manager for Kubernetes that enables you to automate YAML manifests for Kubernetes objects, packaging information into charts and deploying to a Kubernetes cluster. It tracks the versioned history of each chart installation and change, allowing you to use simple commands to roll back to a previous version or upgrade to a newer one. It also makes it easy to install popular applications to Kubernetes via community-shared Helm charts.

You can leverage Helm to more easily deploy and test an environment, increasing productivity and reducing the time it takes to transition from testing to production. Additionally, Helm can help you simplify and automate the process of sending applications to end users for installation.

This is part of a series of articles about Kubernetes.

# How Does Helm Work?
Helm operates by defining and managing charts, which are packages of pre-configured Kubernetes resources. When a chart is deployed, Helm communicates with the Kubernetes API to create and manage the defined resources within the cluster. A file called ‘values.yaml’ provides variables needed to correctly deploy specific resources.

# Komodor | What Is Kubernetes Helm? Architecture, Quick Start, and Best Practices
[this is a copyrighted image, do not use it as is. We recommend rebuilding with your graphic designer. Change text as follows:

Container actual resource.. → Information about resources to be deployed
Contains actual configurations… → Configurations for resources 
Uses values.yaml… -> Deploys resources, using values.yaml to insert missing variables]
What Is a Helm Chart?
A Helm chart is a collection of files that describe a related set of Kubernetes resources. This includes:

1. chart.yaml: Contains metadata about the chart, such as its name, version, and description.
2. values.yaml: Specifies default configuration values for the chart.
3. templates folder: A directory containing the Kubernetes resource templates. These are processed using the values specified in values.yaml to generate the final YAML configuration files.
charts folder: A directory containing dependencies, which are other charts that this chart relies on.
README.md: Provides an overview and usage instructions for the chart.
By packaging Kubernetes manifests into a chart, Helm simplifies the deployment and management of applications. Charts can be shared and reused, promoting consistency and reducing duplication of effort.

Related content: Read our guide to Kubernetes helm charts.

What Is a Helm Chart Repository?
A Helm chart repository is a collection of Helm charts that are made available for installation. These repositories can be public or private and are often hosted on platforms like GitHub or dedicated Helm repository services.

Repositories are defined by an index.yaml file, which lists the available charts and their versions. Users can add repositories to their Helm client using the helm repo add command and then install charts from these repositories with helm install. Public repositories, such as the Helm stable and Helm incubator repositories, provide access to a wide range of community-maintained charts for popular applications and services.


