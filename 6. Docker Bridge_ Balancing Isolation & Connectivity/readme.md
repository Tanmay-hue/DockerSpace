# 🌍 Docker Bridge: Ensuring Isolation & Connectivity

## 📌 Objective
This guide aims to explore **network isolation** in Docker containers by demonstrating how containers within the same **custom bridge network** can interact, while those on separate networks remain **isolated**. Mastering this concept is essential for **securing microservices** and ensuring proper communication within containerized environments.

---

## 🚢 Understanding Docker Networking
Networking is a key aspect of **containerized applications**, enabling interaction between containers while maintaining **security and separation**. Docker offers multiple networking configurations:

### 🏗️ Docker Network Types:
- **Bridge Network (Default)** – Allows internal communication between containers unless restricted.
- **Custom Bridge Network** – Provides enhanced control and enables name-based communication.
- **Host Network** – Directly attaches containers to the host’s network stack.
- **Overlay Network** – Facilitates multi-host communication (Docker Swarm).
- **Macvlan Network** – Assigns MAC addresses to containers, making them appear as distinct network devices.
- **None Network** – Completely disables networking for containers.

In this tutorial, we focus on **custom bridge networks** for controlled networking and **isolation**.

---

## 🔥 Why Choose a Custom Bridge Network?
A **custom bridge network** brings several benefits:
- ✅ **Enhanced Security** – Containers on different networks are **isolated** by default.
- ✅ **Optimized Performance** – Enables direct communication with minimal overhead.
- ✅ **DNS Resolution** – Allows name-based communication between containers.
- ✅ **Greater Control** – Supports custom **subnets, IP ranges, and gateways**.

To illustrate, we’ll create a **custom bridge network** named `tanmay-bridge` and connect multiple containers to it.

---

## ⚙️ 1. Setting Up a Custom Bridge Network
```bash
docker network create --driver bridge --subnet 172.20.0.0/16 --ip-range 172.20.240.0/20 tanmay-bridge
```
### 📖 Breakdown:
- `--driver bridge` → Specifies the **bridge mode**.
- `--subnet 172.20.0.0/16` → Defines the overall **IP range**.
- `--ip-range 172.20.240.0/20` → Manages **dynamic IP allocation**.

---

## 🚀 2. Deploying Containers within the Custom Network
### Running a **Redis Container** (`tanmay-database`)
```bash
docker run -itd --net=tanmay-bridge --name=tanmay-database redis
```
### Running a **BusyBox Container** (`tanmay-server-A`)
```bash
docker run -itd --net=tanmay-bridge --name=tanmay-server-A busybox
```

### 🔍 Retrieving Container IPs
```bash
docker network inspect tanmay-bridge
```
**Expected Output:**
```
 tanmay-database: 172.20.240.1
 tanmay-server-A: 172.20.240.2
```

---

## 📡 3. Verifying Container Communication
### Test Ping from **tanmay-database** to **tanmay-server-A**
```bash
docker exec -it tanmay-database ping 172.20.240.2
```
### Test Ping from **tanmay-server-A** to **tanmay-database**
```bash
docker exec -it tanmay-server-A ping 172.20.240.1
```
✅ **Expected Result:** Containers should successfully **ping** each other.

---

## 🔒 4. Demonstrating Isolation with a Separate Container
We will now introduce a new container (`tanmay-server-B`) on the **default bridge network**.
```bash
docker run -itd --name=tanmay-server-B busybox
```
### 📌 Retrieve IP of `tanmay-server-B`
```bash
docker inspect -format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' tanmay-server-B
```
(Example output: `172.17.0.2`)

---

## 🚫 5. Testing Isolation Between Networks
Attempting to ping `tanmay-server-B` from `tanmay-database`:
```bash
docker exec -it tanmay-database ping 172.17.0.2
```
🚨 **Expected Outcome:** The ping should **fail** since the containers belong to different networks.

---

## 🔎 6. Inspecting Network Details
### View Network Configurations
```bash
docker network inspect tanmay-bridge
docker network inspect bridge
```
- ✅ `tanmay-bridge` should contain `tanmay-database` & `tanmay-server-A`. 
- ✅ The **default bridge network** should contain `tanmay-server-B`.

---

## 🏁 Conclusion
- **Containers in the same network** can communicate effortlessly.
- **Containers in different networks** are **isolated** by default.
- Docker’s **networking model** provides a robust and secure communication framework.

🎯 **You now have a strong grasp of Docker Bridge Networking!** 🚀

