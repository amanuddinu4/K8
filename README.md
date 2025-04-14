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
- Write a Deployment Configuration File (deployment.yml):<br>
<br>
apiVersion: apps/v1<br>
kind: Deployment<br>
metadata:<br>
  name: my-app-deployment<br>
spec:<br>
  replicas: 2<br>
  selector:<br>
    matchLabels:<br>
      app: my-app<br>
  template:<br>
    metadata:<br>
      labels:<br>
        app: my-app<br>
    spec:<br>
      containers:<br>
      - name: my-app<br>
        image: nginx<br>
        ports:<br>
        - containerPort: 80<br>

  
- Apply the Deployment:<br>
  kubectl apply -f deployment.yaml<br>

3. Expose the App as a Service<br>
Write a Service Configuration File (service.yml):<br>

apiVersion: v1<br>
kind: Service<br>
metadata:<br>
  name: my-app-service<br>
spec:<br>
  selector:<br>
    app: my-app<br>
  ports:<br>
  - protocol: TCP<br>
    port: 80<br>
    targetPort: 80<br>
  type: NodePort<br>

- Apply the Service:<br>
  kubectl apply -f service.yaml<br>
4. Verify Pods<br>
  To check the status of your running pods:<br>
kubectl get pods<br>

5. Scale Deployments<br>
   To scale the deployment to 5 replicas:<br>
   kubectl scale deployment my-app-deployment --replicas=2<br>
   
   Verify the updated pod count:<br>
   kubectl get pods<br>
   
6. Troubleshoot Pods Using Logs<br>
Use kubectl describe for Pod Details:<br>
kubectl describe pod <pod-name><br>
View Application Logs:<br>
kubectl logs <pod-name><br>
For pods with multiple containers:<br>
kubectl logs <pod-name> -c <container-name> <br>  
  




 

