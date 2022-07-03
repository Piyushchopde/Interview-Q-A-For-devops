1) What is Kubernetes?
Kubernetes is an open source orchestration tool developed by Google for managing micro-services or containerized applications across a distributed cluster of nodes.

2) Kubernetes Components and Architecture
K8s Master Node: the master server that will create the cluster and it has all thecomponents and service that manage, plan, schedule and monitor all the worker nodes.
 Worker Node: the server that has host the applications as Pods and containers.

3) Kubernetes Master Node Components
- API server – is the primary management components of kubernetes and is responsible for orchestrating all operations (scaling, updates, and so on) in the cluster. It also acts as the gateway to the cluster, so the API server must be accessible by clients from outside he cluster integration with CLI and GUI

- Controller-manager - The Controller Manager is the engine that runs the core control loops, create Pods, watches the state of the cluster, and makes changes to drive status toward the desired state.

- Replication-Controller - A ReplicationController ensures that a specified number of pod replicas are running at any one time. It makes sure that a pod is always up and available.

- Node Controller - The node controller is a Kubernetes master component which manages various aspects of nodes.

- Scheduler - is identify the right node to place a container on based resource limitations taints, tolerations and affinity/anti-affinity roles.

- etcd cluster - etcd is a critical part of the Kubernetes. etcd database that stores the state of the cluster, including node and workload information in a key/value format

- Container runtime : The container runtime is the software that is responsible for running containers. Kubernetes supports several container runtimes: Docker , containerd , CRI-O

Node (worker) components:
 - kubelet - the main service on a node, connect between Master and Node and ensuring that pods and their containers are healthy and running in the desired 	state. This component also reports to the master on the health of the host 	where it is running.

- kube-proxy - a proxy service that runs on each worker node to deal with individual host subnetting and expose services to the external world. It performs request forwarding to the correct pods/containers across the various isolated networks in a cluster.

Kubectl
kubectl command is a line tool that interacts with kube-apiserver and send commands to the master node. Each command is converted into an API call.

Pod - one or more containers that should be controlled as a single application.



Deployment – it provides declarative updates to applications, a deployment allows youto describe an application’s life cycle, such as which images to use for the app, the number of pods there should be, and the way in which they should be updated.

Service – Allows you to dynamically access a group of replica Pods via IP and Port from your network and define name for the service.

What is a Namespace?
 Namespace as a virtual cluster inside your Kubernetes cluster. You can have multiple namespaces inside a single Kubernetes cluster, and they are all logically isolated from each other. 

Secret - At the application level, Kubernetes secrets can store sensitive information (such as passwords, SSH keys, API keys or tokens) per cluster 

CoreDNS - CoreDNS is a flexible, extensible DNS server that can serve as the Kubernetes cluster DNS. 

Node-Proxy - a proxy service that runs on each worker node to deal with individual host subnetting and expose services to the external world. It performs request forwarding to the correct pods/containers across the various isolated networks in a cluster.

Replica Set & Deployment - A ReplicaSet is a set of Pod templates that describes a set of Pod replicas. It uses a template that describes what each Pod must contain.

Daemon Set - 
Deamon set are like replica set its helps you deploy multiple instance of pods but its run one copy of your pod each node in cluster whenever new node is add  to the cluster the replica of the pod  automatically add to the node when node is remove the pod will automatically remove deamon set insure one copy of pod alway present in cluster.

Why use DaemonSets?
To run a daemon for cluster storage on each node , such as: glusterd
To run a daemon for logs collection on each node, such as: logstash
To run a daemon for node monitoring on ever note, such as: collectd



Label - Labels are key/value pairs that are attached to Kubernetes objects, such as pods,services

Taints: are used to repel Pods from specific nodes. This is quite similar to the node anti-affinity  Instead of applying the label to a node, we apply a taint that tells a scheduler to repel Pods from this node if it does not match the taint. Only those Pods that have a toleration for the taint can be let into the node with that taint.
There are 3 taint effect
NoSchedule
PerferNoSchedule
NoExecute

Tolerations : are applied to pods, and allow the pods to schedule onto nodes with matching taints.
Eq: 
tolerations:
- key=”app”
  operator= “Equal”
  value=”blue”       
  effect=”No Schedule”




Meaing V1 and apps/v1
v1
This was the first stable release of the Kubernetes API. It contains many core objects.
apps/v1
apps is the most common API group in Kubernetes, with many core objects being drawnfrom it and v1. It includes functionality related to running applications on Kubernetes,like Deployments, RollingUpdates, and ReplicaSets.

Service types:
Cluster IP - It is the default kubernetes service used for internal communication within the cluster.
NodePort - It will open a ports on each nodes and traffic will be forwarded to the service through random port. And I can access the service (Pod) with the node IP + Defined port.You can only use ports 30000–32767
LoadBalancer - It is a type that forwards all external traffic to a service through this type. And I can access the service (Pod) with the node name only.
External Name - it is a type used to access a service internally that is hosted outside cluster through DNS CName or A record...

Volume - similar to a container volume in Docker, but a Kubernetes volume applies to a whole pod and is mounted on all containers in the pod. Kubernetes guarantees data is preserved across container restarts. The volume will be removed only when the pod gets destroyed. Also, a pod can have multiple volumes

Persistent volume (PV):
Persistent Volume is a solution to store data of our containers permanently even after the pods got deleted.

Persistent volume claim (PVC)
A Persistent Volume Claim (PVC) is a claim request for some storage space by users.
Persistent Volume supports three types of Reclaim Policy
 Retain
 Delete
 Recycle
	
Persistent Volume supports three types of access modes
 ReadWriteOnce
 ReadOnlyMany
 ReadWriteMany

What is Kubernetes Volumes?
Kubernetes Volumes are used to store data that should be accessible across all your containers running in a pod based on the requirement.

What are the types of Kubernetes Volumes?
Kubernetes supports many kind of storage types, these are determined by how it is created and assigned to pods.
Local Node Types - emptyDIR, hostpath, local
File Sharing types - nfs
Storage types - fc, iscsi
Special Purpose Types - Secret, Git repo
Cloud Provider types - Vsphere, Cinder, awsElasticBlockStore, azureDisk, gcepersistentDisk
Distributed filesystem types - glusterfs, cephfs
Special type - persistent volume, persistent volume claim

Note:

1) emptyDIR - It’s a  storage types that writes data only in memory till the pods running. So  data will be erased when the pod is deleted. So it’s not a persistent kind of types.
2) hostpath, local, fc and other types are persistent kind only, but volume won’t be available across the nodes. It will be available only on local nodes. So we may need to setup something shared volume using traditional storage mount across all the nodes.
3) Persistent volume type volumes can be accessible across all the nodes.



CRI: ( Container Runtime Interface )
The CRI is a plugin interface which enables the kubelet to use a wide variety of container runtimes, without having a need to recompile the cluster components.
You need a working container runtime on each Node in your cluster, so that the kubelet can launch Pods and their containers.
The Container Runtime Interface (CRI) is the main protocol for the communication between the kubelet and Container Runtime.

ConfigMaps
A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.
A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.
A ConfigMap is not designed to hold large chunks of data. The data stored in a ConfigMap cannot exceed 1 MiB. If you need to store settings that are larger than this limit, you may want to consider mounting a volume or use a separate database or file service.
ConfigMap does not provide secrecy or encryption. If the data you want to store are confidential, use a Secret rather than a ConfigMap



Ingress:
An API object that manages external access to the services in a cluster, typically HTTP.
Ingress may provide load balancing, SSL termination and name-based virtual hosting.
Node affinity:
Node affinity is a set of rules used by the scheduler to determine where a pod can be placed. 
 There are two types of node affinity:
    • requiredDuringSchedulingIgnoredDuringExecution: The scheduler can't schedule the Pod unless the rule is met. 
    • preferredDuringSchedulingIgnoredDuringExecution: The scheduler tries to find a node that meets the rule. If a matching node is not available, the scheduler still schedules the Pod.


What is static Pod?
Static Pods are managed directly by the kubelet daemon on a specific node, without the API server observing them.





Pod status:
1) CrashLoopBackOff state 
one of your pods is in a constant state of flux—one or more containers are failing and restarting repeatedly. This typically happens because each pod inherits a default restartPolicy of Always upon creation

2) Pending state
If a Pod is stuck in Pending it means that it can not be scheduled onto a node. Generally this is because there are insufficient resources of one type or another that prevent scheduling
3) 


