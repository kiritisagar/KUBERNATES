![image](https://github.com/user-attachments/assets/a4d7a9e7-473b-42d1-a648-26d021234b0b)


Pods can contain a single or multiple containers as a group, that share the same resources within that Pod (storage, network resources, namespaces). Pods typically have a 1–1 mapping with containers, but in more advanced situations, we may run multiple containers in a Pod.

Pods are epheremeral resources, meaning that Pods can be terminated at any point and then restarted on another node within our Kubernetes cluster. They live and die, but Pods will never come back to life.

A Kubernetes pod is the smallest and simplest unit in the Kubernetes object model that you can create or deploy.

# What’s the difference between single container and multi-container Pods?
Running a single container in a Pod is a common use case. Here, the Pod acts as a wrapper around the single container and Kubernetes manages the Pods rather than the containers directly.

We can also run multiple containers in a Pod. Here, the Pod wraps around an application that’s composed of multiple containers and share resources.

# How can we create Pods in Kubernetes?
We can define Pods in Kubernetes using YAML files.

# Pod Lifecycle
Pods are ephemeral. They are created, run, and terminated. When a pod dies (e.g., due to a node failure), Kubernetes can create a new pod with the same configuration, but it will be a new instance with a new IP address.
Pods are usually managed by higher-level controllers such as Deployments, StatefulSets, or DaemonSets, which ensure the desired state of pods.

# Networking
Each pod has a unique IP address in the cluster, and containers within a pod share this IP. They can communicate with each other via localhost.
Pods can communicate with other pods, services, or external resources using the cluster network.

# Storage
Pods can use volumes to persist data across container restarts. Volumes are defined at the pod level and can be shared by all containers in the pod.

# Breaking Down the Pod Manifest:
apiVersion: Defines the API version of the Kubernetes object.
kind: Specifies that this is a Pod object.
metadata: Provides metadata about the pod, such as its name and labels.
spec: Describes the desired state of the pod, including:
containers: Lists the containers that should be run in the pod. Each container is described by its image, name, and other configuration details.
volumes: Describes any volumes that should be mounted into the pod's containers.
