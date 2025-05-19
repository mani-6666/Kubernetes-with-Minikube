# Kubernetes with Minikube

This project demonstrates the deployment and management of applications using Kubernetes on a local environment with Minikube. It includes deploying an NGINX web server, exposing it as a service, scaling it, and inspecting logs.

## Table of Contents

- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Step 1: Set up Minikube](#step-1-set-up-minikube)
  - [Step 2: Deploy the Application](#step-2-deploy-the-application)
  - [Step 3: Expose the Application](#step-3-expose-the-application)
  - [Step 4: Scale the Deployment](#step-4-scale-the-deployment)
  - [Step 5: Inspect Logs](#step-5-inspect-logs)
- [Configuration Files](#configuration-files)
  - [Deployment Configuration](#deployment-configuration)
  - [Service Configuration](#service-configuration)
- [Key Commands](#key-commands)
- [Deliverables](#deliverables)
- [Conclusion](#conclusion)

## Introduction

Kubernetes is a powerful orchestration platform for managing containerized applications. This project utilizes Minikube, a lightweight Kubernetes implementation, to provide a hands-on experience in a local development environment.

## Project Structure

```bash
Kubernetes-with-Minikube/
├── deployment.yaml        # Kubernetes Deployment configuration
├── service.yaml           # Kubernetes Service configuration
├── README.md              # Documentation for the project
```

## Prerequisites

- Minikube
- kubectl
- Docker

## Getting Started

### Step 1: Set up Minikube

Start Minikube:

```bash
minikube start --driver=docker
```

Verify the cluster:

```bash
kubectl cluster-info
```

### Step 2: Deploy the Application

Apply the deployment configuration:

```bash
kubectl apply -f deployment.yaml
```

Verify the deployment and pods:

```bash
kubectl get deployments
kubectl get pods
```

### Step 3: Expose the Application

Apply the service configuration:

```bash
kubectl apply -f service.yaml
```

Verify the service:

```bash
kubectl get services
```

Access the application:

```bash
minikube service my-app-service
```

### Step 4: Scale the Deployment

Scale the application to 4 replicas:

```bash
kubectl scale deployment my-app --replicas=4
```

Verify the scaled pods:

```bash
kubectl get pods
```

### Step 5: Inspect Logs

Describe the deployment:

```bash
kubectl describe deployment my-app
```

View logs of a specific pod:

```bash
kubectl logs <pod-name>
```

## Configuration Files

### Deployment Configuration

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
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
      - name: my-app-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

### Service Configuration

```yaml
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
```

## Key Commands

- `minikube start` – Start the Minikube cluster
- `kubectl apply -f <file>` – Apply a Kubernetes configuration file
- `kubectl get pods` – List all running pods
- `kubectl get services` – List all services
- `kubectl scale deployment <name> --replicas=<num>` – Scale a deployment
- `kubectl logs <pod-name>` – View logs of a specific pod

## Deliverables

### Files:

- deployment.yaml
- service.yaml
- README.md

### Screenshots:

- Output of `kubectl get pods`
- Output of `kubectl get services`
- The application running in the browser

## Conclusion

This project demonstrates the fundamentals of Kubernetes, including deploying applications, exposing them as services, scaling deployments, and inspecting logs. Minikube provides a simple way to experiment with Kubernetes in a local environment, making it an excellent tool for learning and testing.
