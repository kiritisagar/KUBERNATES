# Deploy the Pod and Service
Now that you have the YAML files, you can deploy the Pod and Service using kubectl.

# 1.Apply the Pod YAML:
kubectl apply -f pod.yaml

# 2.Apply the Service YAML:
kubectl apply -f service.yaml

# 3.Verify the Deployment
Check the Pod:
kubectl get pods

# 4.Check the Service:
kubectl get services
