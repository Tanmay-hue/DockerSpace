# Minikube with Docker on Windows ☸️

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/3/39/Kubernetes_logo_without_workmark.svg" alt="Kubernetes Logo" width="250" />
</p>

## What is Minikube? 

**Minikube** is a lightweight tool that enables developers to run a local Kubernetes cluster on their machine. It provides a straightforward way to experiment with Kubernetes without requiring a full-scale cloud environment. With support for multiple drivers such as Docker, VirtualBox, and Hyper-V, Minikube simplifies Kubernetes deployment for local development, testing, and learning.

---

## What is Kubernetes? ☸️

**Kubernetes** is an open-source container orchestration platform designed to automate application deployment, scaling, and management. It efficiently manages containerized applications to ensure high availability and optimal performance across different environments.

Key benefits of Kubernetes:
- Deploy containerized applications across clusters.
- Scale applications dynamically based on demand.
- Automate workload management for improved efficiency.
- Provide built-in load balancing, high availability, and fault tolerance.

By leveraging Kubernetes, developers can focus on building applications while Kubernetes handles deployment complexity.

---

## ✅ Step 1: Install Required Tools

Ensure you have the necessary software installed before proceeding.

### 1. Install Docker Desktop 🐋

Minikube uses Docker to run Kubernetes in a containerized environment. Install Docker Desktop:

- [Download and install Docker Desktop](https://www.docker.com/products/docker-desktop/)

**During installation:**
- Enable WSL 2 backend for better performance (recommended). ⚙️
- If using Windows Pro/Enterprise, enable Hyper-V (handled by Docker). 🔧

### 2. Install Minikube 📦

To install Minikube, open CMD or PowerShell as Administrator and execute:
```bash
choco install minikube
```
If Chocolatey is not available, [install Minikube manually](https://minikube.sigs.k8s.io/docs/start/).

### 3. Install kubectl

```bash
choco install kubernetes-cli
```
Verify the installation:
```bash
kubectl version --client
```
![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/1.png)

![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/2.png)

![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/3.png)

![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/4.png)

![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/5.png)

![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/6.png)

---

## ✅ Step 2: Start Minikube with Docker Driver 🐳

With Docker running in the background, start Minikube using the Docker driver:

### 1. Start Minikube
```bash
minikube start --driver=docker
```
This initializes a Kubernetes cluster inside a Docker container.

Verify the cluster status:
```bash
minikube status
```
![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/7.png)

---

## ✅ Step 3: Deploy an Application 🚀

Let’s deploy an Nginx application.

### 1. Create an Nginx Deployment
```bash
kubectl create deployment nginx --image=nginx
```

### 2. Expose the Deployment 🔓
```bash
kubectl expose deployment nginx --type=NodePort --port=80
```

### 3. Get the Service URL 🔗
```bash
minikube service nginx --url
```
Open the generated URL in your browser to access the Nginx server. 🌐
![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/8.png)

---

## ✅ Step 4: Manage Kubernetes Cluster

### 1. Check Running Pods 📋
```bash
kubectl get pods
```

### 2. Scale the Deployment 📏
To scale up to 3 replicas:
```bash
kubectl scale deployment nginx --replicas=3
```
Check the updated pods:
```bash
kubectl get pods
```

### 3. Delete the Deployment 🧹
```bash
kubectl delete service nginx
kubectl delete deployment nginx
```
![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/9.png)

---

## ✅ Step 5: Stop and Delete Minikube 🗑️

### 1. Stop Minikube
```bash
minikube stop
```

### 2. Delete the Cluster 
```bash
minikube delete
```
This removes all Kubernetes resources and stops the cluster.
![image](https://github.com/Tanmay-hue/DockerSpace/blob/main/9.%20Minikube%20with%20Docker%20on%20Windows/images/10.png)

---

## 🎯 Conclusion

Running Kubernetes locally with Minikube and Docker provides a convenient way to test and experiment with containerized applications. By using Minikube, developers can simulate a full Kubernetes environment without additional infrastructure dependencies.

🚀 Happy Kubernetes-ing! 😊

