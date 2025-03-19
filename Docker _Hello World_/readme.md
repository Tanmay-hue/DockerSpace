# 🐋 **Getting Started with Docker**

Welcome to **Docker Essentials**! 🌟 In this guide, we'll walk through the basics of setting up a simple Dockerized Python application. Let's start by running **"Hello, World!"** in Docker. 🚀

---

## 📁 **Setting Up the Python Application**
Begin by creating a Python file named **`app.py`**, and add the following code:

```python
print("Hello, World!")
```

This simple script will be executed inside a Docker container.

---

## 📚 **Useful Resources**
Expand your Docker knowledge with these references:

📌 [Docker Official Documentation](https://docs.docker.com/)  
📌 [Docker Desktop Setup Guide](https://docs.docker.com/desktop/)  

---

## 🚢 **Step-by-Step Deployment Guide**

Follow these steps to containerize and run your Python application with Docker:

### 🏗️ **Step 1: Install Docker & Python**
1️⃣ Download and install **Docker Desktop** → [Get Docker](https://www.docker.com/products/docker-desktop/)  
2️⃣ Make sure Docker is up and running.  
3️⃣ Install **Docker** and **Python** extensions in your development environment for a better experience.  

---

### 🔍 **Step 2: Confirm Installation**
Verify that both **Docker** and **Python** are installed correctly:

✔️ Check the installed Docker version:
```bash
docker --version 
```

✔️ Check the installed Python version:
```bash
python --version 
```

If both commands return valid versions, you're all set! ✅

---

### 🏗️ **Step 3: Build & Execute Your Docker Application**

#### **🔨 i) Build a Docker Image**
Use the command below to create a Docker image:
```bash
docker build -t myapp .
```

#### **📂 ii) Confirm Image Creation**
List the available Docker images to verify your image:
```bash
docker images
```

#### **🚀 iii) Run the Docker Container**
Execute your container to display **"Hello, World!"**:
```bash
docker run myapp
```

---

## 🎉 **Wrapping Up**
Congratulations! You've successfully built and run your **first Dockerized Python application**. 🐋✨

📌 What's Next? Explore advanced Docker features like **volumes**, **networking**, and **multi-container applications**! 💡  

⚡ **Happy Docking!** 🌊
