![image](https://github.com/user-attachments/assets/ab3c82c3-1f1b-48b7-baa0-8efe3e748fa6)

# Kubernetes Architecture
Kubernetes deployment is called a cluster. 
A Kubernetes cluster consists of at least one main (control) plane, and one or more worker machines, called nodes. 
Both the control planes and node instances can be physical devices, virtual machines, or instances in the cloud.


## on masternode(control plane)
![image](https://github.com/user-attachments/assets/75831052-2800-4c81-9119-4957f781ea9e)


# Control Plane
Also known as master node or head node.
The control plane manages the worker nodes and the Pods in the cluster.
In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.
The control plane receives input from a CLI or UI via an API.
It is not recommended to run user workloads on master mode.

# Kubernetes Control Plane Components:
The control plane’s components make global decisions about the cluster, as well as detecting and responding to cluster events. Kubernetes relies on several administrative services running on the control plane. These services manage aspects, such as cluster component communication, workload scheduling, and cluster state persistence.

# 1.API Server (kube-apiserver)
API server exposes the Kubernetes API.
Entry point for REST/kubectl — It is the front end for the Kubernetes control plane.
It tracks the state of all cluster components and managing the interaction between them.
It is designed to scale horizontally.
It consumes YAML/JSON manifest files.
It validates and processes the requests made via API.

# 2.etcd (key-value store)
It is a consistent, distributed, and highly-available key value store.
It is stateful, persistent storage that stores all of Kubernetes cluster data (cluster state and config).
It is the source of truth for the cluster.
It can be part of the control plane, or, it can be configured externally.

# 3.Scheduler (kube-scheduler)
It schedules pods to worker nodes.
It watches api-server for newly created Pods with no assigned node, and selects a healthy node for them to run on.
If there are no suitable nodes, the pods are put in a pending state until such a healthy node appears.
It watches API Server for new work tasks.
Factors taken into account for scheduling decisions include:

Individual and collective resource requirements.
Hardware/software/policy constraints.
Affinity and anti-affinity specifications.
Data locality.
Inter-workload interference.
Deadlines and taints.

# 4.Controller Manager (kube-controller-manager)
It watches the desired state of the objects it manages and watches their current state through the API server.
It takes corrective steps to make sure that the current state is the same as the desired state.
It is controller of controllers.

Some of the core controllers managed by the kube-controller-manager include:

1.Node controller: Monitors the health of nodes in the cluster and takes appropriate actions, such as marking a node as "NotReady" or evicting pods from a failed node.

2.Replication controller: Ensures the correct number of replicas for a ReplicationController resource is always running.

3.Endpoint controller: Populates the "Endpoints" object for services, providing a way to route traffic to pods.

4.Service Account and Token controllers: Manage default service accounts and API access tokens for namespaces.

5.Deployment controller: Ensures that the desired number of replicas for a Deployment resource is maintained, and handles rolling updates or rollbacks as needed.

6.DaemonSet controller: Ensures that the desired number of replicas for a DaemonSet resource is running on all eligible nodes.

7.Job controller: Manages the lifecycle of Job resources, which represent one-off tasks that run to completion.










It runs controller processes. Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process.
Some types of controllers are:

A.Node controller: Responsible for noticing and responding when nodes go down.
B.Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
C.Endpoints controller: Populates the Endpoints object (that is, joins Services & Pods).
D.Service Account & Token controllers: Create default accounts and API access tokens for new namespaces.
Cloud Controller Manager
The cloud controller manager integrates with the underlying cloud technologies in your cluster when the cluster is running in a cloud environment.
The cloud-controller-manager only runs controllers that are specific to your cloud provider.
Cloud controller lets you link your cluster into cloud provider’s API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.
The following controllers can have cloud provider dependencies:

Node controller: For checking the cloud provider to determine if a node has been deleted in the cloud after it stops responding.
Route controller: For setting up routes in the underlying cloud infrastructure.
Service controller: For creating, updating and deleting cloud provider load balancers.

## Kubernetes Node Components

Node components run on every node, maintaining running pods and providing the Kubernetes runtime environment.

![image](https://github.com/user-attachments/assets/4b3e9520-bc9f-47ee-85a6-3c2dcbba66f6)

# 1.kubelet
It is an agent that runs on each node in the cluster.
It acts as a conduit between the API server and the node.
It makes sure that containers are running in a Pod and they are healthy.
It instantiates and executes Pods.
It watches API Server for work tasks.
It gets instructions from master and reports back to Masters.


# 2.kube-proxy
It is networking component that plays vital role in networking.
It manages IP translation and routing.
It is a network proxy that runs on each node in cluster.
It maintains network rules on nodes. These network rules allow network communication to Pods from inside or outside of cluster.
It ensure each Pod gets unique IP address.
It makes possible that all containers in a pod share a single IP.
It facilitating Kubernetes networking services and load-balancing across all pods in a service.
It deals with individual host sub-netting and ensure that the services are available to external parties.



