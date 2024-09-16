Steps to Apply the Configuration:

# Create the Namespace:
kubectl apply -f namespace.yaml

# Create the Pod:
kubectl apply -f nginx-pod.yaml

# Create the Service:
kubectl apply -f nginx-service.yaml

# Verify the Setup:
List pods in the namespace:

# kubectl get pods -n my-namespace
List services in the namespace:

# kubectl get services -n my-namespace
This setup will create an Nginx pod and expose it within the my-namespace namespace using a ClusterIP service.






