![image](https://github.com/user-attachments/assets/d23bc5ac-63bf-4ab1-978c-40bff046c5b0)


When multiple pods are scheduled on the same node, they can communicate with each other directly using localhost or the loopback interface. 
This communication happens through the pod’s assigned IP address within the cluster, typically in the form of a Virtual Ethernet (veth) pair. 
The communication occurs at the network layer, enabling high-performance and low-latency interactions between pods on the same node.


# 1. Create Two Pods (App and Database)
# (app-pod.yml):

apiVersion: v1
kind: Pod
metadata:
  name: app-pod
  labels:
    app: webapp
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80

# (db-pod.yml):
apiVersion: v1
kind: Pod
metadata:
  name: db-pod
  labels:
    app: database
spec:
  containers:
  - name: mysql-container
    image: mysql:5.7
    env:
    - name: MYSQL_ROOT_PASSWORD
      value: rootpassword
    ports:
    - containerPort: 3306

# 2. Deploy the Pods
kubectl apply -f app-pod.yml
kubectl apply -f db-pod.yml


# 3. Verify Pod Status
kubectl get pods

# 4. Get Pod IP Addresses
kubectl get pods -o wide

# 5. Test Pod-to-Pod Communication via IP
