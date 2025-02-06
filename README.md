# Kubernetes Services Demo

This repository demonstrates the use of Kubernetes services to manage and expose a Python-based web application. The project includes deployment configurations, service definitions, an Ingress resource, and a Dockerfile to containerize the application.

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

### 3. **Ingress**  
- **Purpose**: Manages external access to services inside the cluster via HTTP and HTTPS.  
- **What it Does**:  
  - Provides a single entry point to multiple services using domain-based routing.  
  - Reduces the need for multiple `LoadBalancer` services.  
  - Enables SSL/TLS termination for secure connections.  

**Example: Nginx Ingress Controller**  
A common way to manage Ingress in Kubernetes is by using the **Nginx Ingress Controller**. After installing it, you can define rules to route traffic to specific services based on the requested domain or path.  

Example Ingress configuration:  
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: demo-ingress
spec:
  rules:
  - host: demo.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: demo-service
            port:
              number: 80
```
This routes all traffic from `demo.example.com` to the `demo-service` running on port `80`.  

---

## Commands Overview  

### Minikube Management  
- `minikube start` – Starts a local Kubernetes cluster.  
- `minikube status` – Checks the status of the Minikube cluster.  

### Deployment Management  
- `kubectl apply -f deployment.yml` – Deploys the application based on the configuration file.  
- `kubectl get deploy` – Displays information about the deployment.  

### Service Management  
- `kubectl apply -f service.yml` – Creates a service to expose the application.  
- `kubectl get svc` – Retrieves details of the service, including its IP and port.  

### Ingress Management  
- `kubectl apply -f ingress.yml` – Deploys the Ingress resource to route external traffic to the service.  
- `kubectl get ing` – Displays the Ingress resource details, including its associated hostname and rules.  

### Testing the Application  
- Use the `curl` command or a web browser to access the application at the service’s or Ingress’s exposed IP and port.  

---

## Repository Structure  

- `deployment.yml` – Contains the deployment configuration, including replica settings and pod template.  
- `service.yml` – Defines the service configuration for exposing the application.  
- `ingress.yml` – Configures routing and external access for the application.  
- `Dockerfile` – Instructions for building the Docker image for the application.  

---

## How to Use This Repository  

### 1. Clone the Repository  
Clone the repository to your local machine:  
```bash
git clone https://github.com/your-username/kubernetes-services-demo.git
cd kubernetes-services-demo
```  

### 2. Build the Docker Image  
Build the Docker image for the Python application:  
```bash
docker build -t your-username/python-sample-app:v1 .
```  

### 3. Start Minikube  
Start a local Kubernetes cluster:  
```bash
minikube start
minikube status
```  

### 4. Deploy the Application  
Apply the deployment configuration:  
```bash
kubectl apply -f deployment.yml
kubectl get deploy
```  

### 5. Expose the Application  
Apply the service configuration to expose the app:  
```bash
kubectl apply -f service.yml
kubectl get svc
```  

### 6. Set Up Ingress  
Apply the Ingress configuration:  
```bash
kubectl apply -f ingress.yml
kubectl get ing
```  
This will configure routing for external access.  

### 7. Access the Application  
Use the service’s IP and port:  
```bash
curl -L http://<Service-IP>:<Exposed-Port>/demo
```  
Or, if using Ingress with a configured domain:  
```bash
curl -L http://demo.example.com
```  

---

## Notes  
- Modify `service.yml` to change the service type (e.g., ClusterIP, NodePort, LoadBalancer).  
- Modify `ingress.yml` to update routing rules based on the domain and path requirements.  
