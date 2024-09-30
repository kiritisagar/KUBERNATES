# Pod Affinity: 
Ensures that a pod is placed on the same node (or in the same zone/region) as other specified pods.
You want all instances of your service to be scheduled close to each other for fast communication.

![image](https://github.com/user-attachments/assets/002db467-8093-40f6-a296-6290c3ed81d6)

# Pod Anti-Affinity: 
Ensures that a pod is placed on a different node (or in a different zone/region) from other specified pods.
You want to avoid placing all instances of a service on the same node to increase fault tolerance (if one node fails, other instances continue running on different nodes).

![image](https://github.com/user-attachments/assets/4aa60bfa-391a-4841-aeb9-9a6bd293affc)

