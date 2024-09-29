
# Node Affinity and Anti-Affinity in Kubernetes:
Node Affinity and Anti-Affinity are advanced ways to control how pods are scheduled on nodes based on specific rules. 
Unlike nodeSelector, these provide more flexibility with expressions, such as matching multiple labels and conditions.

2. Label the Nodes
Node Affinity and Anti-Affinity work based on node labels. First, you need to label nodes to group them for affinity/anti-affinity rules.

Label a node:
kubectl label nodes <node-name> <label-key>=<label-value>

# For example:
kubectl label nodes worker1 disktype=ssd
kubectl label nodes worker2 disktype=hdd

# 3. Create a Pod with Node Affinity
Node Affinity ensures that a pod is scheduled on a node that matches specific labels.

RequiredDuringSchedulingIgnoredDuringExecution: The pod must be scheduled on a node that matches the affinity rule.
PreferredDuringSchedulingIgnoredDuringExecution: The pod prefers to be scheduled on nodes that match the rule but can be scheduled elsewhere if necessary.


Node Affinity:

A more advanced and flexible method for scheduling pods.
Allows for complex rules based on expressions (e.g., In, NotIn, Exists, DoesNotExist).
Offers both hard (required) and soft (preferred) scheduling constraints.


Node Affinity:
When you need more complex scheduling logic, such as using multiple labels, partial matching, or preference-based scheduling.
Example: Prefer running the pod in us-east-1a but allow it to run in us-west-1 if needed.



In: Pod will run on nodes where disktype is either ssd or nvme.
NotIn: Pod will avoid nodes where environment is dev.
Exists: Pod will only run on nodes that have the region label (any value).
DoesNotExist: Pod will avoid nodes that have the gpu label.
