# Step 1: Install Metrics Server

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

# Check the status of your HPA:

kubectl get hpa

# Step 5: Test Autoscaling
kubectl run -i --tty load-generator --image=busybox /bin/sh

# Step 6: Observe Scaling
kubectl get pods

# Clean Up
kubectl delete hpa nginx-hpa
kubectl delete deployment nginx-deployment
