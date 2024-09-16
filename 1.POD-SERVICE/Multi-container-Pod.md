apiVersion: v1
kind: Pod
metadata:
  name: multi-container-pod
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
  - name: sidecar-container
    image: busybox
    command: ['sh', '-c', 'echo Hello from the sidecar; sleep 3600']
