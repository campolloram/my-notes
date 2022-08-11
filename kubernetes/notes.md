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

## YAML in Kubernetes
Top level fields for a kubernetes definition file
1. apiVersion -> Version of the Kubernetes API e.g. v1
2. kind -> Types of object we are trying to create e.g. Pod, ReplicaSet, deployment
3. metadata -> [dict] Data about the object. e.g. name, labels, etc. l
4. spec -> (specification) This depends on the service you are building, for a pod you  will have a containers list where each element will have a name and an image


## Controllers
### Replication Controllers/ReplicaSets
Helps us run multiple instances of the same pod in the cluster, providing high availability. Helps us balance the load and scale.

**Replication Controller (apiVersion: v1)** -> Older technology

**Replica Set (apiVersion: apps/v1)** -> New technology, you can use selectors to match labels from pods.


## Deployments (apps/v1)
- It is higher in the hierarchy than the replicasets.
- It kind of encapsulates a replicaset and adds more functionality, under the hood it actually creates replicasets.
- It lets us deploy changes into our applications seemlessly, like update a version, etc. You can also roll back in case something goes wrong.
- It also allows you to do rolling updates which help you to deploy with zero downtime by incrementally updating Pods instances with new ones.



