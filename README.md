# Kubernetes Services Demo

This repository demonstrates the use of Kubernetes services to manage and expose a Python-based web application. 
The project includes deployment configurations, service definitions, and a Dockerfile to containerize the application.

---

## Key Concepts

### 1. **Deployment**
- **Purpose**: Manages the lifecycle of pods in Kubernetes.
- **What it Does**:
  - Ensures the application runs with the desired number of replicas.
  - Automatically replaces failed pods to maintain availability.
- **Key Components**:
  - **Replicas**: Defines the number of pod instances to run.
  - **Labels and Selectors**: Used to match pods with the service for communication.

### 2. **Service**
- **Purpose**: Exposes the application to the network, enabling communication between users and pods.
- **What it Does**:
  - Handles dynamic IP changes of pods using labels and selectors.
  - Provides different levels of accessibility (internal, organizational, external).
- **Types**:
  - **ClusterIP**: Internal communication within the cluster.
  - **NodePort**: Exposes the service on each node’s IP address and a static port.
  - **LoadBalancer**: Provides external access to the service.

### 3. **Dockerfile**
- **Purpose**: Defines the environment and steps to containerize the application.
- **What it Does**:
  - Installs necessary dependencies (Python, virtual environment).
  - Copies application files into the container.
  - Sets up the application to run on port 8000.

---

## Commands Overview

### Minikube Management
- `minikube start`: Starts a local Kubernetes cluster.
- `minikube status`: Checks the status of the Minikube cluster.

### Deployment Management
- `kubectl apply -f deployment.yml`: Deploys the application based on the configuration file.
- `kubectl get deploy`: Displays information about the deployment.

### Service Management
- `kubectl apply -f service.yml`: Creates a service to expose the application.
- `kubectl get svc`: Retrieves details of the service, including its IP and port.

### Testing the Application
- Use the `curl` command or a web browser to access the application at the service's exposed IP and port.

---

## Repository Structure

- `deployment.yml`: Contains the deployment configuration, including replica settings and pod template.
- `service.yml`: Defines the service configuration for exposing the application.
- `Dockerfile`: Instructions for building the Docker image for the application.

---

## How to Use This Repository

Follow these steps to set up and run the Kubernetes services demo:

---

## 1. Clone the Repository  
Clone the repository to your local machine:  
```bash
git clone https://github.com/your-username/kubernetes-services-demo.git
cd kubernetes-services-demo
```  

## 2. Build the Docker Image  
Build the Docker image for the Python application:  
```bash
docker build -t your-username/python-sample-app:v1 .
```  

## 3. Start Minikube  
Start a local Kubernetes cluster:  
```bash
minikube start
minikube status
```  

## 4. Deploy the Application  
Apply the deployment configuration:  
```bash
kubectl apply -f deployment.yml
kubectl get deploy
```  

## 5. Expose the Application  
Apply the service configuration to expose the app:  
```bash
kubectl apply -f service.yml
kubectl get svc
```  

## 6. Access the Application  
Use the service’s IP and port:  
```bash
curl -L http://<Service-IP>:<Exposed-Port>/demo
```  

---

## Notes  
- Modify `service.yml` to change the service type (e.g., ClusterIP, NodePort, LoadBalancer).  
- This demo uses the **NodePort** type for simplicity.  

---

### Deployment Configuration (`deployment.yml`)  
Defines application deployment:  
- **apiVersion** and **kind**: Resource type (Deployment).  
- **spec.replicas**: Number of pod replicas.  
- **template**: Pod configuration (containers, images, ports).  

### Service Configuration (`service.yml`)  
Exposes the application:  
- **apiVersion** and **kind**: Resource type (Service).  
- **spec.type**: Service type (NodePort).  
- **spec.selector**: Matches pods based on labels.  
- **spec.ports**: Maps service port to container port.  

---

## Dockerfile Overview  
Steps to containerize the app:  
1. **Base Image**: Ubuntu with Python.  
2. **Environment Setup**: Installs dependencies.  
3. **App Files**: Copies files into the container.  
4. **Expose Port**: Opens port 8000.  
5. **Run Command**: Starts the app with `manage.py`.  

---

## Key Commands  

### Minikube Management  
- `minikube start`: Start a local cluster.  
- `minikube status`: Check cluster status.  

### Deployment Management  
- `kubectl apply -f deployment.yml`: Deploy the app.  
- `kubectl get deploy`: View deployment details.  

### Service Management  
- `kubectl apply -f service.yml`: Create a service.  
- `kubectl get svc`: View service details.  

### Testing  
Access the app via `curl` or a web browser using the service’s IP and port.  

---  