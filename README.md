Overview

This guide provides steps to deploy a Kubernetes application with:

A dedicated service account

Secrets mounted as environment variables and volumes

A NodePort service for external access

A Horizontal Pod Autoscaler (HPA) for scaling

Rolling updates with minimal downtime

Prerequisites

Kubernetes cluster (Minikube, EKS, AKS, or GKE)

kubectl CLI installed

Steps

1. Create a Secret

kubectl create secret generic key-secret --from-literal=KEY_SECRET=my-secret-value

2. Apply Kubernetes Manifests

kubectl apply -f service-account.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f hpa.yaml  # Optional

3. Verify Deployment

kubectl get pods
kubectl get svc
kubectl get hpa  # Optional

4. Access the Application

If using Minikube, get the service URL:

minikube service my-app-service

If using a cloud provider, access via <NodeIP>:30007.

5. Monitor the Deployment

Check logs:

kubectl logs -l app=my-app

Describe deployment:

kubectl describe deployment my-app

Cleanup

kubectl delete -f service-account.yaml
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
kubectl delete -f hpa.yaml
kubectl delete secret key-secret

Notes

The rolling update strategy ensures only one pod is unavailable during updates.

HPA automatically scales pods based on CPU utilization.

This setup ensures a secure, scalable, and highly available Kubernetes application.



