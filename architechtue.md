![image](https://github.com/user-attachments/assets/7179ba54-4aba-4212-9d5a-2d9ec43c9042)

# Kubernetes Architecture
Kubernetes deployment is called a cluster. 
A Kubernetes cluster consists of at least one main (control) plane, and one or more worker machines, called nodes. 
Both the control planes and node instances can be physical devices, virtual machines, or instances in the cloud.

# Control Plane
Also known as master node or head node.
The control plane manages the worker nodes and the Pods in the cluster.
In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.
The control plane receives input from a CLI or UI via an API.
It is not recommended to run user workloads on master mode.

# Kubernetes Control Plane Components:
The control plane’s components make global decisions about the cluster, as well as detecting and responding to cluster events. Kubernetes relies on several administrative services running on the control plane. These services manage aspects, such as cluster component communication, workload scheduling, and cluster state persistence.

API Server (kube-apiserver)
API server exposes the Kubernetes API.
Entry point for REST/kubectl — It is the front end for the Kubernetes control plane.
It tracks the state of all cluster components and managing the interaction between them.
It is designed to scale horizontally.
It consumes YAML/JSON manifest files.
It validates and processes the requests made via API.
etcd (key-value store)
It is a consistent, distributed, and highly-available key value store.
It is stateful, persistent storage that stores all of Kubernetes cluster data (cluster state and config).
It is the source of truth for the cluster.
It can be part of the control plane, or, it can be configured externally.
Scheduler (kube-scheduler)
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
Controller Manager (kube-controller-manager)
It watches the desired state of the objects it manages and watches their current state through the API server.
It takes corrective steps to make sure that the current state is the same as the desired state.
It is controller of controllers.
It runs controller processes. Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process.
Some types of controllers are:

Node controller: Responsible for noticing and responding when nodes go down.
Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
Endpoints controller: Populates the Endpoints object (that is, joins Services & Pods).
Service Account & Token controllers: Create default accounts and API access tokens for new namespaces.
Cloud Controller Manager
The cloud controller manager integrates with the underlying cloud technologies in your cluster when the cluster is running in a cloud environment.
The cloud-controller-manager only runs controllers that are specific to your cloud provider.
Cloud controller lets you link your cluster into cloud provider’s API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.
The following controllers can have cloud provider dependencies:

Node controller: For checking the cloud provider to determine if a node has been deleted in the cloud after it stops responding.
Route controller: For setting up routes in the underlying cloud infrastructure.
Service controller: For creating, updating and deleting cloud provider load balancers.


