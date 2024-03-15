# Kubernetes Express.js Example Project

This project is intended as a learning resource for running an Express.js application on a
Kubernetes cluster using Kind (Kubernetes in Docker). It demonstrates the basic setup,
scaling with Horizontal Pod Autoscalers (HPA), and access management for an Express.js
application containerized with Docker and orchestrated by Kubernetes.

### Prerequisites

Before starting with this project, ensure you have the following tools installed on your
system:

- Node.js: The runtime environment for the Express.js application. Download and install
  from Node.js website.
- Docker: Required for building and running containerized applications. Download and
  install from Docker website.
- KinD: A tool for running local Kubernetes clusters using Docker containers.
  Installation instructions are available on the Kind website.
- kubectl: The command line tool for interacting with Kubernetes clusters. Follow the
  kubectl installation instructions.

### Setup and Startup

- Build the Docker Image:
  ```bash
  docker build -t kubernetes-express-example:v1 .
  ```
- Create a Kind Cluster:
  ```bash
  kind create cluster --name local
  ```
- Load the Docker Image into the Kind cluster.
  ```bash
  kind load docker-image kubernetes-express-example:v1 --name local
  ```
- Deploy the application and related resources to the cluster.
  ```bash
  kubectl apply -f deployment.yml
  kubectl apply -f hpa.yml
    ```

### Inspection and Testing

- Verify Deployment:
  ```bash
  kubectl get deployments
  ```
- Forward a local port to access the deployed Express.js service.
  ```bash
  kubectl port-forward service/kubernetes-express-example-service 8080:8080
  ```
- Visit http://localhost:8080 in a web browser or use a tool like curl to access the
  application.

- Watch HPA
  ```bash
  kubectl get hpa kubernetes-express-example-hpa --watch
  ```
- Watch Pods
  ```bash
  kubectl get pods --watch
  ```

### Stop and Removal

- Remove all deployed resources from the cluster.
  ```bash
  kubectl delete -f deployment.yml
  kubectl delete -f hpa.yml
  ```

- Delete the Kind Cluster:
  ```bash
  kind delete cluster --name local
  ```
