# 1. First Deploy

# 1.1 What are microservices

Microservices are small autonomous services that work together. The top 3 reasons for using microservices are:

1. Zero downtime independent deployability
2. Isolation of data and processing around that data
3. Use microservices to reflect the organizational structure

An application following a microservice architecture is composed of several (potentially dozens) of independently operating services. Managing and operating such a complex system is challenging.

# 1.2 What is Kubernetes?

K8s is an open source system for automating deployment, scaling and management of containerized applications. (In essence, K8s is the sum of all bash scripts and best practises that most sysadmins would cobble over time)

A container orchestration system such as K8s is required when maintaining containerized applications. The main responsibility of orchestration is starting and stopping of container. For eg: we want the critical services to restart whenever it crashes.

# 1.3 K8s cluster with `k3d`

A cluster is a group of machine, nodes that work together. A k8s cluster can be of any size. A single node cluster would have 1 machine that hosts the k8s control-pane, that can then be expanded to 5000 total nodes.

The **control pane** is essentialy the brains of the k8s cluster - handles scheduling workloads, maintaining the desired state of applications, and responding to cluster events.

We refer to **server nodes** to refer to nodes with control-pane and **agent nodes** to refer to nodes to without that role.

`k3d cluster create -a 2` starts a cluster with 2 agent nodes.

- We see that `6443` is tied opened to `"k3d-k3s-default-serverlb"` which is a load balancer proxy. (We could have opted to open the cluster without the load balancer)

`k3d kubeconfig get k3s-default` sets up a `kubeconfig` file.

The other tool we will use is `kubectl` - which is the command line tool which will allow us to interact with the cluster.

`kubectl cluster-info` will give us info about the cluster.

NOTE : `k3d` sets up additional infra - ie 2 agent nodes, 1 server nodes, 1 load balancer and 1 internal container.

# 1.4 First Deploy

To deploy an image we need the cluster to have access to the image. By default, k8s is intended to be used with a registry. We use _Docker Hub_.
