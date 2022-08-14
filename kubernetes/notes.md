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



## Namespaces
- Namespaces are a group of services. (like households)
- YOU CAN ADD THE NAMESPACE IN THE YAML DEFINITION UNDER THE METADATA OF THE SERVICE
- By default kubernetes creates 3 namespaces:
1. kube-system -> Internal to kubernetes
2. Default -> where your services go, unless you specify a new one
3. kube-public -> Where resources that should be available to all public are published

- Namespaces provide Isolation

- You could even create namespaces for your dev, stage, etc.

- Each namespaces have their own set of policies that define who can do what and also limit their resources.

- The services inside a namespace can refer to each other by just using their names

- For referring to services in other namespaces you use the following convention:

```
db-service.dev.svc.cluster.local
```
1. db-service = name of service
2. dev = namespace name
3. svc = service
4. cluster.local = domain (literally the local cluster)

## Quotas
They are used to limit resources in a namespace


---

**PROTIP:** 

You can use the --dry-run=client flag to just run the command without actually creating anything

If you combine this with the -o yaml flag for formatting the output as yaml, you can easily create files for creating services. Check the commands on the useful-commands file by searching for generating quick files.

---

## Docker Pre-requisites
- A docker container only runs as longs as there is a processs runninig in the container, if there is no process the container dies.
 

- The differene betweeen CMD and ENTRYPOINT is that CMD executes the command directly and ENTRYPOINT is a command where you specify the parameter when running the docker run command in the CLI

e.g. 

CMD -> sleep 5 (sleeps for 5 seconds)

ENTRYPOINT -> sleep (you then need to run the image by specifing the seconds like so... docker run image 10 )


In a nutshell ENTRYPOINT appends the parameters and CMD replaces them.


You can use CMD with ENTRYPOINT to sepcify a default value for the command

e.g.

ENTRYPOINT ["sleep"]

CMD["5"]

If not specified the 5 will be appended to the sleep command


- You can use the args key in the containers spec section of the Pod definition to override the CMD of the container

- You can the command key inside the container spec of the Pod definition to substitute the actual ENTRYPOINT in the container.


--- 

Quick Note: You can't edit directly some of the Pods attributes, but you can edit the Deployment and that will make sure to delete the Pod and raise a new one

---


### Config Maps, Secrets and Environment Vars
You can type directly the env variables in your pod definition, but this can make your definition look messy. A better way to do this is to define a ConfigMap as a separate file and then inject the configmap into the pod definition.

You can use the "envFrom" key inside spec followed by the "configMapRef" key and finally the "name" key to inject the configmap into a pod.

```
spec:
  envFrom:
    - configMapRef:
        name: app-config
```

You can also inject Env vars using Volumes like so:

```
volumes:
  - name: app-config-volume
    configMap:
      name: app-config
```

for using secrets we follow the following struct:

```
spec:
  envFrom:
    - secretRef:
        name: app-secret
```

or as a file in a volume:

```
volumes:
  - name: app-secret-volume
    secret:
      secretName: app-secret
```

If you use volume, each attribute in the secret is created as a file with the value of the secret as its content.


You can enable encryption at rest for secrets so they are stored encrypted in ETCD

### Service Accounts
There are two types of accounts in kubernetes

1. User accounts -> Used by humans (admin, developer, etc.)
2. Service accounts ->  Account used by an applications used to interact with the kubernetes cluster.

**Service Account**

When a service account is created, it first creates the serviceaccount object and the generates a token and stores it in a secret object.

The secret object is then linked to the service account.

This token can then be used as an authenticator bearer token when making calls to the kubenetes API


Each namespace has its own default service account.

The default token is stored in the pod in the address:

```
/var/run/sercrets/kubernetes.io/serviceaccount
```

### Resource Requirements
- Resource Requests -> Minimum number of hardware required by the pod, by default it is .5CPU and 256Mi. You can modify them.

- The pod cant consume more cpu than its limit, but it can consume more memory. When this happens constantly, the pod is terminated.

### Taint and Tolerations
You can create taints to block pods from being allocated to certain nodes. Then you can create tolerations so that only certain types of pods can be allocated to those nodes. This is way of creating "Dedicated resources" to ceratin tasks

**Taints are set on nodes and tolerations are set on Pods**

- There are 3 taint effects:
1. NoSchedule -> No pods are going to be schedule in that node unless they have the toleration
2. PreferNoSchedule -> It will try to not schedule pods that are untolerant.
3. NoExecute -> It will not schedule untolerant pods + it will exit existing pods that are untolerant.



