# 🐳 Docker & ☸️ Kubernetes — Complete Introduction  
  
## 📌 Overview  
  
Modern software development increasingly relies on **containerization** and **container orchestration**. Two of the most important technologies in this ecosystem are:  
  
- **Docker** — a platform for building and running containers  
- **Kubernetes** — a system for managing and orchestrating containers at scale  
  
Together they form the backbone of modern **cloud-native infrastructure** used by companies like **Google, Netflix, Amazon, and Spotify**.  
  
---  
  
# 🐳 What is Docker?  
  
## Definition  
  
**Docker** is a platform that allows developers to package applications and their dependencies into **containers** so they can run consistently across different environments.  
  
In simple terms:  
  
> Docker ensures that an application runs the same on every machine.  
  
For example:  
  
A Java Spring Boot app that works on your laptop will also work on:  
  
- a Linux server  
- a cloud VM  
- a Kubernetes cluster  
  
without any configuration changes.  
  
---  
  
# 📦 What is a Container?  
  
A **container** is a lightweight isolated environment that contains:  
  
- application code  
- runtime  
- libraries  
- system tools  
- dependencies  
  
Unlike virtual machines, containers **share the host OS kernel**, making them much faster and lighter.  
  
### Container vs Virtual Machine  
  
| Feature | Container | Virtual Machine |  
|-------|-------|-------|  
| OS Kernel | Shared | Separate |  
| Startup time | Seconds | Minutes |  
| Size | MB | GB |  
| Performance | Near native | Slightly slower |  
  
---  
  
# 🧱 Docker Architecture  
  
Docker consists of several core components.  

Developer → Docker CLI → Docker Daemon → Containers

  
## Docker Components  
  
### 1️⃣ Docker Client  
  
The **Docker CLI** is what developers interact with.  
  
Example commands:  
  
```bash  
docker build  
docker run  
docker ps  
docker stop

----------

### 2️⃣ Docker Daemon

The **Docker daemon** runs in the background and manages:

-   containers
    
-   images
    
-   volumes
    
-   networks
    

----------

### 3️⃣ Docker Image

A **Docker image** is a blueprint for a container.

It contains:

-   application code
    
-   runtime
    
-   dependencies
    
-   environment configuration
    

Example:

Spring Boot App  
Java Runtime  
Libraries

Images are **immutable**.

----------

### 4️⃣ Docker Container

A **container** is a running instance of a Docker image.

Example:

Image → docker run → Container

----------

### 5️⃣ Docker Registry

A **registry** stores Docker images.

Examples:

-   Docker Hub
    
-   AWS ECR
    
-   Google Container Registry
    

Example:

docker pull postgres  
docker push myapp:latest

----------

# 📜 Dockerfile

A **Dockerfile** defines how to build a Docker image.

Example for a **Spring Boot application**:

FROM eclipse-temurin:21-jre  
  
WORKDIR /app  
  
COPY target/app.jar app.jar  
  
EXPOSE 8080  
  
ENTRYPOINT ["java","-jar","app.jar"]

Explanation:

Command

Purpose

FROM

base image

WORKDIR

working directory

COPY

copy files into container

EXPOSE

declare port

ENTRYPOINT

run command

----------

# 🚀 Docker Workflow

Typical workflow:

1️⃣ Write application  
2️⃣ Create Dockerfile  
3️⃣ Build Docker image  
4️⃣ Run container

Example:

docker build -t myapp .  
  
docker run -p  8080:8080 myapp

----------

# 📦 Docker Volumes

Containers are **stateless by default**.

If a container stops, its data disappears.

To persist data Docker uses **volumes**.

Example:

docker run -v postgres-data:/var/lib/postgresql/data postgres

Volumes store data **outside the container lifecycle**.

----------

# 🌐 Docker Networking

Docker containers communicate using networks.

Types:

Network

Description

bridge

default local network

host

uses host network

overlay

multi-host networking

none

no networking

Example:

docker network create my-network

----------

# ☸️ What is Kubernetes?

## Definition

**Kubernetes (K8s)** is an open-source system for **automating deployment, scaling, and management of containerized applications**.

It was originally developed by **Google**.

If Docker manages **one container**, Kubernetes manages **thousands of containers across many servers**.

----------

# Why Kubernetes is Needed

Running containers manually becomes difficult when applications grow.

Problems:

-   many containers
    
-   many servers
    
-   scaling traffic
    
-   restarting failed containers
    
-   rolling updates
    

Kubernetes solves these problems automatically.

----------

# Kubernetes Architecture

A Kubernetes cluster consists of two types of nodes.

Cluster  
 ├── Control Plane  
 └── Worker Nodes

----------

# 🧠 Control Plane

The **control plane** manages the cluster.

Components:

Component

Role

API Server

entry point for commands

Scheduler

assigns pods to nodes

Controller Manager

maintains cluster state

etcd

cluster database

----------

# ⚙️ Worker Nodes

Worker nodes run the containers.

Each node contains:

-   kubelet
    
-   container runtime
    
-   kube-proxy
    

----------

# 📦 Kubernetes Pod

A **Pod** is the smallest deployable unit in Kubernetes.

A pod can contain:

-   one container
    
-   multiple containers
    

Example:

Pod  
 ├── Spring Boot Container  
 └── Redis Sidecar

----------

# Kubernetes Deployment

A **Deployment** manages pods.

Features:

-   scaling
    
-   rolling updates
    
-   self-healing
    

Example YAML:

apiVersion: apps/v1  
kind: Deployment  
  
metadata:  
 name: spring-app  
  
spec:  
 replicas: 3  
  
 selector:  
 matchLabels:  
 app: spring  
  
 template:  
 metadata:  
 labels:  
 app: spring  
  
 spec:  
 containers:  
 - name: spring  
 image: myapp:latest  
 ports:  
 - containerPort: 8080

----------

# 🌐 Kubernetes Service

Pods are **ephemeral** (they change IP addresses).

A **Service** provides a stable network endpoint.

Types:

Service

Description

ClusterIP

internal service

NodePort

exposed on node

LoadBalancer

external load balancer

Example:

kind: Service  
apiVersion: v1  
  
metadata:  
 name: spring-service  
  
spec:  
 selector:  
 app: spring  
  
 ports:  
 - port: 80  
 targetPort: 8080  
  
 type: NodePort

----------

# 🔄 Kubernetes Self-Healing

Kubernetes automatically:

-   restarts crashed containers
    
-   replaces failed nodes
    
-   reschedules pods
    

Example:

Pod crashes  
↓  
Kubernetes restarts it automatically

----------

# 📈 Kubernetes Scaling

Scaling is automatic.

Example:

kubectl scale deployment spring-app --replicas=10

Kubernetes will create **10 pods**.

----------

# 🔄 Rolling Updates

Kubernetes can update applications **without downtime**.

Example:

Old version running  
↓  
New version deployed gradually  
↓  
Traffic shifts to new pods

----------

# ☸️ Kubernetes Workflow

Typical deployment process:

1️⃣ Build Docker image  
2️⃣ Push image to registry  
3️⃣ Create Kubernetes deployment  
4️⃣ Expose service  
5️⃣ Scale application

----------

# Docker vs Kubernetes

Feature

Docker

Kubernetes

Purpose

Container runtime

Container orchestration

Scale

Single machine

Cluster

Complexity

Low

High

Automation

Basic

Advanced

Docker builds and runs containers.

Kubernetes **manages containers at scale**.

----------

# Real World Example

Example production system:

Frontend (React)  
↓  
API Gateway  
↓  
Microservices  
 ├── Auth Service  
 ├── Payment Service  
 ├── Order Service  
↓  
Databases

Each service runs inside **Docker containers** and is managed by **Kubernetes**.

----------

# Benefits of Docker + Kubernetes

### Consistency

Runs the same everywhere.

### Scalability

Handles thousands of containers.

### Fault tolerance

Automatically replaces failed containers.

### Portability

Works across cloud providers.

----------

# Popular Tools in the Ecosystem

Tool

Purpose

Docker

container runtime

Kubernetes

container orchestration

Helm

Kubernetes package manager

Prometheus

monitoring

Grafana

visualization

Istio

service mesh

----------

# Conclusion

Docker and Kubernetes together form the foundation of **modern cloud-native systems**.

Docker solves the problem of:

> "How do we package and run applications?"

Kubernetes solves the problem of:

> "How do we manage thousands of containers in production?"

Understanding both technologies is essential for modern **backend engineers, DevOps engineers, and cloud architects**.
