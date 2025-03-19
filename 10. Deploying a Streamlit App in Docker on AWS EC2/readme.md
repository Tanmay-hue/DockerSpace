# 🌍 Deploying a Streamlit App in Docker on AWS EC2

## 🔥 Introduction
This guide walks you through the process of deploying a Streamlit app inside a Docker container on an AWS EC2 instance with a tailored network configuration. You'll learn:

✅ Configuring a VPC, Subnet, Route Table, and Internet Gateway  
✅ Setting up an EC2 instance  
✅ Installing Docker  
✅ Uploading project files to EC2  
✅ Running a Streamlit app in Docker  
✅ Managing Docker containers  

---

## 📌 Table of Contents
1️⃣ Configuring VPC, Subnet, Route Table, and Internet Gateway  
2️⃣ Setting Up an EC2 Instance  
3️⃣ Connecting to EC2  
4️⃣ Adjusting Permissions for PEM Key  
5️⃣ Installing Docker  
6️⃣ Uploading Files to EC2  
7️⃣ Building & Running the Docker Container  
8️⃣ Accessing the Streamlit App  
9️⃣ Managing the Docker Container  

---

## 1️⃣ Configuring VPC, Subnet, Route Table, and Internet Gateway

### 🌟 Creating a VPC
Navigate to AWS Console → VPC Dashboard → Create VPC  
- **VPC Name:** MyCustomVPC  
- **IPv4 CIDR:** 10.0.0.0/16  

![img1](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/1.png)

### 🌟 Setting Up a Subnet
Go to VPC Dashboard → Subnets → Create Subnet  
- **VPC:** MyCustomVPC  
- **Subnet Name:** MyPublicSubnet  
- **CIDR:** 10.0.1.0/24  
- **Auto-assign Public IPv4:** Enabled  

![img2](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/2.png)

### 🌟 Creating an Internet Gateway
- **Gateway Name:** MyIGW  
- **Attach to:** MyCustomVPC  

![img3](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/3.png)

### 🌟 Setting Up a Route Table
- **Route Table Name:** MyPublicRouteTable  
- **Destination:** 0.0.0.0/0  
- **Target:** MyIGW  
- **Associate with:** MyPublicSubnet  

![img4](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/4.png)

---

## 2️⃣ Setting Up an EC2 Instance

### 🏗️ Launching an EC2 Instance
- **Instance Name:** Streamlit-EC2  
- **AMI:** Amazon Linux 2023  
- **Type:** t2.micro (Free Tier)  
- **Key Pair:** Create or Select  
- **VPC:** MyCustomVPC  
- **Subnet:** MyPublicSubnet  
- **Public IP Assignment:** Enabled  
- **Security Group:** Allow SSH (22), HTTP (80), Streamlit (8501)  

![img5](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/5.png)

---

## 3️⃣ Connecting to EC2

### 🔗 Using EC2 Instance Connect
Go to EC2 Dashboard → Select Instance → Click Connect  
- **Connection Method:** EC2 Instance Connect  
- **Click:** Connect  

![img6](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/6.png)

---

## 4️⃣ Adjusting Permissions for PEM Key
```sh
mv /path/to/your-key.pem ~/your-work-directory/
chmod 600 your-key.pem
```

---

## 5️⃣ Installing Docker
```sh
sudo yum update -y
sudo yum install -y docker
sudo systemctl enable docker
sudo systemctl start docker
```

![img7](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/7.png)

---

## 6️⃣ Uploading Files to EC2
```sh
scp -i your-key.pem app.py Dockerfile requirements.txt mushrooms.csv ec2-user@your-ec2-public-ip:/home/ec2-user/
```

![img8](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/8.png)

---

## 7️⃣ Building & Running the Docker Container

### 🏗️ Navigating to Project Directory
```sh
cd /home/ec2-user
```
### 🏗️ Building the Docker Image
```sh
sudo docker build -t streamlit-app .
```

![img9](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/9.png)

### 🏗️ Running the Docker Container
```sh
sudo docker run -d -p 8501:8501 --name streamlit_container streamlit-app
```

![img10](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/10.png)

---

## 8️⃣ Accessing the Streamlit App
🌎 Open your browser and go to:
```sh
http://your-ec2-public-ip:8501
```

![img11](https://github.com/Tanmay-hue/DockerSpace/blob/main/10.%20Deploying%20a%20Streamlit%20App%20in%20Docker%20on%20AWS%20EC2/Images/11.png)

---

## 9️⃣ Managing the Docker Container

### 🛠️ Checking Running Containers
```sh
sudo docker ps
```
### 🛠️ Stopping the Container
```sh
sudo docker stop streamlit_container
```
### 🛠️ Removing the Container
```sh
sudo docker rm streamlit_container
```
### 🛠️ Restarting the Container
```sh
sudo docker start streamlit_container
```

---

## 🎯 Final Thoughts
This guide provides a structured approach to deploying a Streamlit app within Docker on AWS EC2 using a customized VPC configuration. This deployment ensures scalability, security, and availability. 🚀

✅ Happy Cloud Deployment! 🌤️🐳

