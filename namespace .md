Namespaces are a way to organize clusters into virtual sub-clusters

![image](https://github.com/user-attachments/assets/9c9d3e19-ba96-4087-9251-91f554fc043c)


### Key features of namespaces:
1. **Resource Isolation**: Different namespaces allow teams or applications to run in the same Kubernetes cluster without interfering with each other.
2. **Unique Resource Names**: Resources within a namespace must have unique names, but different namespaces can have resources with the same name.
3. **Access Control**: Kubernetes RBAC (Role-Based Access Control) can be applied per namespace, allowing finer control over who can access or modify resources.
4. **Quota Management**: Resource quotas can be applied to each namespace to limit the resources (CPU, memory, etc.) that can be used.

### Default Namespaces:
1. **default**: The default namespace for resources that do not specify any namespace.
2. **kube-system**: Contains resources managed by Kubernetes, like the scheduler and controller manager.
3. **kube-public**: Used for publicly accessible resources, but rarely used.
4. **kube-node-lease**: Used for node heartbeat data.

### Commands:
- **List namespaces**:
      kubectl get namespaces
   
   - **Create a new namespace**:
      kubectl create namespace <namespace-name>
   
   - **Run a pod in a specific namespace**:
      kubectl run nginx --image=nginx --namespace=<namespace-name>
   
   - **Delete a namespace**:
      kubectl delete namespace <namespace-name>
   
Namespaces are ideal when you need logical separation of resources, but they're not needed for small projects or clusters with few applications.
