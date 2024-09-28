![image](https://github.com/user-attachments/assets/a8ce91e0-70fd-4609-9a54-3521dae0fabb)

# 1. ClusterIP
ClusterIP is the default and most common service type.
Kubernetes will assign a cluster-internal IP address to ClusterIP service. This makes the service only reachable within the cluster.
You cannot make requests to service (pods) from outside the cluster.
You can optionally set cluster IP in the service definition file.
Use Cases
Inter service communication within the cluster. For example, communication between the front-end and back-end components of your app.
Example

![image](https://github.com/user-attachments/assets/2222fa5a-b78b-489c-91b2-4297f171af70)

Kubernetes ClusterIP Service
# 2. NodePort
NodePort service is an extension of ClusterIP service. A ClusterIP Service, to which the NodePort Service routes, is automatically created.
It exposes the service outside of the cluster by adding a cluster-wide port on top of ClusterIP.
NodePort exposes the service on each Node’s IP at a static port (the NodePort). Each node proxies that port into your Service. So, external traffic has access to fixed port on each Node. It means any request to your cluster on that port gets forwarded to the service.
You can contact the NodePort Service, from outside the cluster, by requesting <NodeIP>:<NodePort>.
Node port must be in the range of 30000–32767. Manually allocating a port to the service is optional. If it is undefined, Kubernetes will automatically assign one.
If you are going to choose node port explicitly, ensure that the port was not already used by another service.
Use Cases
When you want to enable external connectivity to your service.
Using a NodePort gives you the freedom to set up your own load balancing solution, to configure environments that are not fully supported by Kubernetes, or even to expose one or more nodes’ IPs directly.
Prefer to place a load balancer above your nodes to avoid node failure.
Example

![image](https://github.com/user-attachments/assets/5937aa12-a157-47af-9624-0bd2c5c3f7e9)

Kubernetes NodePort Service
3. LoadBalancer
LoadBalancer service is an extension of NodePort service. NodePort and ClusterIP Services, to which the external load balancer routes, are automatically created.
It integrates NodePort with cloud-based load balancers.
It exposes the Service externally using a cloud provider’s load balancer.
Each cloud provider (AWS, Azure, GCP, etc) has its own native load balancer implementation. The cloud provider will create a load balancer, which then automatically routes requests to your Kubernetes Service.
Traffic from the external load balancer is directed at the backend Pods. The cloud provider decides how it is load balanced.
The actual creation of the load balancer happens asynchronously.
Every time you want to expose a service to the outside world, you have to create a new LoadBalancer and get an IP address.
Use Cases
When you are using a cloud provider to host your Kubernetes cluster.
This type of service is typically heavily dependent on the cloud provider.

Example
![image](https://github.com/user-attachments/assets/bd240dcf-f73f-49b6-9872-640477b8e2b5)

Kubernetes LoadBalancer Service
4. ExternalName
Services of type ExternalName map a Service to a DNS name, not to a typical selector such as my-service.
You specify these Services with the `spec.externalName` parameter.
It maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value.
No proxying of any kind is established.
Use Cases
This is commonly used to create a service within Kubernetes to represent an external datastore like a database that runs externally to Kubernetes.
You can use that ExternalName service (as a local service) when Pods from one namespace to talk to a service in another namespace.
Example

Kubernetes ExternalName Service
