# Kubernetes

## Core concepts

### Node
A physical or virtual machine

There are two types of nodes:
1. Worker node
2. Master node

### Cluster
Group of nodes.

### Components of Kubernetes
1. API -> Frontend, CLI talks to the API
2. ectd -> Key Value database
3. kubelet -> Agent that runs on each node on each cluster, it makes sure the container are running as expected.
4. Container Runtime (docker)
5. Controller -> Brain behind orchestration, brings up new container when they go down
6. Scheduler -> Looks for newly created containers and assigng them to nodes.


### Master vs Worker Nodes
Master server has the kube-apiserver, etcd, controller and scheduler

Worker server has the kubelet agent 


### kubectl
It's a tool used to deploy and manage applications in a cluster. e.g.
```
kubectl run hello-minikube # Runs an application in the cluster

kubectl cluster-info

kubectl get nodes
```


## Pods (Wrapper of container/s)
Smallest unit of all

It can only contain at most 1 container for the application, but it can have other containers called "helper containers"

The containers inside a Pod share the same network, storage, etc.







