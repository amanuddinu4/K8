# Build a Kubernetes Cluster Locally with Minikube
Objective
This project demonstrates how to deploy and manage applications in Kubernetes using Minikube. The focus is on creating deployments, exposing services, scaling applications, and troubleshooting issues using kubectl.
Prerequisites
Tools
- Minikube
- kubectl
- Docker

System Requirements
- A system with support for running Minikube (e.g., Linux, macOS, or Windows with virtualization enabled).
- Docker installed for building and managing container images.

Steps to Build the Cluster
1. Install Minikube and Start the Cluster
- Install Minikube:- Download Minikube from the Minikube Official Docs.
- Follow installation instructions based on your operating system.

- Start the Minikube Cluster:minikube start
 minikube start
This starts a local Kubernetes cluster.

2. Create a Deployment
- Write a Deployment Configuration File (deployment.yml):

 apiVersion: apps/v1
 kind: Deployment
  metadata:
   name: my-app-deployment
  spec:
     replicas: 2
     selector:
       matchLabels:
        app: my-app
         template:
               metadata:
                 labels:
             app: my-app
              spec:
               containers:
                 - name: my-app
                  image:  amanuddinu4/nodejs-demo-app
                   ports:
                    - containerPort: 80
  
- Apply the Deployment:
  kubectl apply -f deployment.yaml

3. Expose the App as a Service
Write a Service Configuration File (service.yml):

apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort

- Apply the Service:
  kubectl apply -f service.yaml
4. Verify Pods
  To check the status of your running pods:
kubectl get pods

5. Scale Deployments
   To scale the deployment to 5 replicas:
   kubectl scale deployment my-app-deployment --replicas=5
   
   Verify the updated pod count:
   kubectl get pods
   
6. Troubleshoot Pods Using Logs
Use kubectl describe for Pod Details:
kubectl describe pod <pod-name>
View Application Logs:
kubectl logs <pod-name>
For pods with multiple containers:
kubectl logs <pod-name> -c <container-name>   
  




 

