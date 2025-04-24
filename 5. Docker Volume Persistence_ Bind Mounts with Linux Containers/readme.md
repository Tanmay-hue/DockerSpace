# 🏗 Docker Volume Persistence: Bind Mounts on Linux Container 🐳

## 📌 Overview
This guide walks through how to use Docker **bind mounts** in a **Linux container** to ensure data persists beyond the lifecycle of a container. By mapping a local directory to the container, stored data remains accessible even after removing the container.

---

## 🔧 Procedure & Findings

### 🚀 Step 1: Running a Container with Bind Mount
To start, you executed:
```sh
docker run -dit --name alpine_with_bind_mount -v C:\Users\asus\docker_data:/data alpine:latest sh
```
#### 📋 Observations:
- Since `alpine:latest` was not present locally, Docker fetched it from the registry.
- A container named **alpine_with_bind_mount** was created.
- The `-v` option linked `C:\Users\asus\docker_data` on the host to `/data` inside the container.
- The container launched with a shell (`sh`) in detached mode.

---

### 📂 Step 2: Creating a File in the Bind-Mounted Directory
Inside the container, you executed:
```sh
docker exec -it alpine_with_bind_mount sh -c "echo 'Hello, tanmay!' > /data/testfile.txt"
```
#### 📋 Observations:
- A shell was launched in the running container.
- A file `testfile.txt` was created inside `/data` with the content **"Hello, tanmay!"**.
- As `/data` is mapped to a host directory, the file was actually stored at `C:\Users\asus\docker_data`.

---

### 🔎 Step 3: Checking File Existence
To verify the file’s content:
```sh
docker exec -it alpine_with_bind_mount sh -c "cat /data/testfile.txt"
```
#### ✅ Expected Output:
```
Hello, tanmay!
```
This confirms that the file was successfully created and accessible inside the container. 🎉

---

### 🗑 Step 4: Removing the Initial Container
To remove the container:
```sh
docker rm -f alpine_with_bind_mount
```
#### 📋 Observations:
- The container was **stopped and deleted**.
- However, the file in `/data` was not lost because it was stored on the host.

---

### 🔄 Step 5: Launching a New Container with the Same Bind Mount
A new container was started with:
```sh
docker run -dit --name new_alpine -v C:\Users\asus\docker_data:/data alpine sh
```
#### 📋 Observations:
- A new container named **new_alpine** was created.
- The same host directory (`C:\Users\asus\docker_data`) was mapped to `/data`.

---

### 🧐 Step 6: Confirming File Persistence
To check if `testfile.txt` still exists:
```sh
docker exec -it new_alpine sh -c "cat /data/testfile.txt"
```
#### ✅ Expected Output:
```
Hello, tanmay!
```
This demonstrates that **bind mounts preserve data even when containers are deleted**. 🔥

---

## 🎯 Key Takeaways
✔ **Bind mounts ensure data persistence across container lifecycles.**

✔ **Deleting a container does not remove files stored in bind-mounted directories.**

✔ **New containers using the same mount point can access previous data.**

✔ **Ideal for file sharing between multiple containers and long-term data retention.**

---

### 🚀 Further Exploration
- 🛠 Experiment with **Docker named volumes** (`docker volume create`) for managing persistent storage.
- 🐳 Test bind mounts with **different container images**.
- 🔐 Investigate **file permission management** in bind-mounted directories.

---

💡 *This guide highlights the usefulness of Docker bind mounts for data persistence. Keep exploring, and happy coding!* 🚀
