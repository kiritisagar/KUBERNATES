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
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
  - name: busybox-container
    image: busybox:latest
    command: ["/bin/sh"]
    args: ["-c", "while true; do sleep 3600; done"]



![Screenshot (222)](https://github.com/user-attachments/assets/3f90d511-4bd0-4bdd-a5d1-7a3608f40195)

# Enter into the container-a:
kubectl exec -it multi-container-pod -c container-a -- /bin/sh

# Test communication with the Nginx container:

wget -qO- http://localhost:80

![Screenshot (223)](https://github.com/user-attachments/assets/64e86e15-c5f0-4e05-9fca-28ecfb7e93dc)


# 2. Communication Between Pods (Same Cluster)
![image](https://github.com/user-attachments/assets/6dd54207-1982-489b-aff6-e5359aac7e39)



