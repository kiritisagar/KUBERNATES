
In Kubernetes, Role-Based Access Control (RBAC) is used to manage permissions within the cluster. 
This allows you to control who can perform what actions (e.g., viewing pods, creating deployments) on resources in specific namespaces or across the entire cluster.

![image](https://github.com/user-attachments/assets/1664339b-5ce4-4ee0-be73-77c856b72ced)



# Key Concepts:
Role: Defines a set of permissions (what actions can be performed) within a namespace.
RoleBinding: Associates the permissions defined in a Role with a specific user, group, or service account.

1. Kubernetes Role
A Role is a namespaced resource that grants permissions to resources (like Pods, ConfigMaps, etc.) within that namespace.


# Role YAML Structure:

apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default  # Role is scoped to a specific namespace
  name: pod-reader
rules:
- apiGroups: [""]     # "" indicates the core API group
  resources: ["pods"] # Resources this Role applies to
  verbs: ["get", "list", "watch"]  # Actions this Role allows on the resources

# Explanation of Fields:

# apiVersion: 
This defines the API group for RBAC, which is rbac.authorization.k8s.io/v1.

# kind: 
The resource type, in this case, a Role.

# metadata.namespace: 
The namespace to which this Role applies. Roles are namespaced, so they cannot span multiple namespaces.

# rules: 
Contains the list of rules that define the permissions. Each rule specifies:
# 1.apiGroups: 
API group of the resources (e.g., "" for core API resources like Pods, or "apps" for deployments).

# 2.resources: The Kubernetes resources this rule applies to (e.g., pods, services, etc.).

# 3.verbs: 
Actions that can be performed on the resources (get, list, create, delete, update, etc.).



# 2. Kubernetes RoleBinding
A RoleBinding assigns the permissions from a Role to a specific user, group, or service account. It binds the Role to a subject.

# RoleBinding YAML Structure:

apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-reader-binding
  namespace: default  # Must match the Role's namespace
subjects:
- kind: User  # Can also be Group or ServiceAccount
  name: john  # The name of the user or service account to grant access
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader  # Must match the name of the Role
  apiGroup: rbac.authorization.k8s.io

# Explanation of Fields:
# subjects: 
Specifies the entity that will receive the permissions defined in the Role. It can be:
User: A human or system user.
Group: A group of users.
ServiceAccount: A Kubernetes service account.

# roleRef: References the Role that will be bound. This includes:
kind: Either Role (for namespaced permissions) or ClusterRole (for cluster-wide permissions).
name: The name of the Role to be referenced.
apiGroup: The API group for RBAC, which is always rbac.authorization.k8s.io.





# ClusterRole and ClusterRoleBinding control access at the cluster-wide level.

# Difference Between Role and ClusterRole
Role: Only applies to resources within a specific namespace.
ClusterRole: Can apply to resources across all namespaces or cluster-wide resources (like nodes, persistent volumes).
If you need to create a ClusterRole and bind it, you would use a similar approach but substitute Role with ClusterRole and RoleBinding with ClusterRoleBinding.

