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

### 1. Clone the Repository

Start by cloning this repository to your local machine:
```bash
git clone https://github.com/your-username/kubernetes-services-demo.git
cd kubernetes-services-demo

### 2. Build the Docker Image

Build the Docker image for the Python application:
```bash
docker build -t your-username/python-sample-app:v1 .

### 3. Start Minikube

Ensure Minikube is installed and running, then start a local Kubernetes cluster:
```bash
minikube start

Check the status of Minikube to confirm it is running:
```bash
minikube status

### 4. Deploy the Application

Apply the deployment configuration to create the pods:
```bash
kubectl apply -f deployment.yml

Verify the deployment:
```bash
kubectl get deploy

### 5. Create the Service

Apply the service configuration to expose the application:
```bash
kubectl apply -f service.yml

Check the service details:
```bash
kubectl get svc

### 6. Access the Application

Find the service’s IP and port using the kubectl get svc command.

Test the application using a web browser or curl:
```bash
curl -L http://<Service-IP>:<Exposed-Port>/demo

---

## Notes
	•	You can modify the service.yml file to change the service type (ClusterIP, NodePort, LoadBalancer) as per your requirements.
	•	This demo uses the NodePort service type for simplicity.

---

## Deployment Configuration

### deployment.yml

The deployment.yml file is used to define how your application is deployed in Kubernetes. Below are the key sections:
	•	apiVersion and kind: Defines the type of resource (Deployment).
	•	metadata: Specifies the name and labels for the deployment.
	•	spec.replicas: Defines the number of pod replicas.
	•	template: Describes the pod configuration, including containers, images, and ports.

---

## Service Configuration

### service.yml

The service.yml file is used to expose the application to the network. Below are the key sections:
	•	apiVersion and kind: Defines the type of resource (Service).
	•	metadata: Specifies the name of the service.
	•	spec.type: Defines the type of service (NodePort).
	•	spec.selector: Matches pods based on labels.
	•	spec.ports: Maps the service port to the container port.

---

## Dockerfile

### Purpose

The Dockerfile is used to containerize the application. Below are the key steps:
	1.	Base Image: Starts with the ubuntu image.
	2.	Environment Setup: Installs Python and dependencies.
	3.	Application Files: Copies the app files into the container.
	4.	Expose Port: Opens port 8000 for the application.
	5.	Run Command: Defines how to start the app using manage.py.

---

## Commands Overview

Minikube Management
	•	minikube start: Starts a local Kubernetes cluster.
	•	minikube status: Checks the status of the Minikube cluster.

Deployment Management
	•	kubectl apply -f deployment.yml: Deploys the application based on the configuration file.
	•	kubectl get deploy: Displays information about the deployment.

Service Management
	•	kubectl apply -f service.yml: Creates a service to expose the application.
	•	kubectl get svc: Retrieves details of the service, including its IP and port.

Testing the Application
	•	Use the curl command or a web browser to access the application at the service’s exposed IP and port.