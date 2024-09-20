# 1. Communication Within a Pod (Same Pod)
![image](https://github.com/user-attachments/assets/b0780e06-0003-47df-a242-2fa3bb8eb042)

# When multiple containers are deployed in the same Pod (multi-container Pod), they share the same network namespace. This means that:

1.Containers in the same Pod can communicate with each other via localhost and the port numbers exposed by the containers.
2.Shared filesystem volumes can also be used for data exchange between containers.

# Example:
If two containers, A and B, are running in the same Pod:

Container A can reach container B using localhost:<port> (assuming Container B exposes some service on a port).

# yml file
apiVersion: v1
kind: Pod
metadata:
  name: multi-container-pod
spec:
  containers:
  - name: container-a
    image: nginx
    ports:
    - containerPort: 80
  - name: container-b
    image: redis
    ports:
    - containerPort: 6379

In this example:

Container A (nginx) can communicate with Container B (redis) by accessing localhost:6379.

# 2. Communication Between Pods (Same Cluster)
![image](https://github.com/user-attachments/assets/6dd54207-1982-489b-aff6-e5359aac7e39)



