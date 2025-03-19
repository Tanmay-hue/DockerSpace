# 🛳 **Streamlit in Docker: A Development Guide**  

Set up your **Streamlit application** inside a **Docker container** for a seamless, portable, and efficient development experience. ⚡  

---

## ✅ **Prerequisites**  
Ensure you have the following installed before proceeding:  

🔸 **Docker** 🛳 (Make sure the Docker daemon is active)  
🔸 **Python 3.9+** 🐍 (`python --version` to check)  
🔸 **pip** 📦 (`pip --version` to confirm)  
🔸 **Basic understanding of Streamlit** 📈  

---

## 📂 **Project Structure**  

```
project_root/
│── .streamlit/
│   └── config.toml
│── src/
│   └── main.py
│── Dockerfile
│── requirements.txt
│── README.md
```

---

## 📜 **File Descriptions**  

### **1️⃣ `.streamlit/config.toml`**  
Configures Streamlit for development mode:  

```toml
[server]
headless = true
runOnSave = true
fileWatcherType = "poll"
```

---

### **2️⃣ `src/main.py`**  
This script defines the **core functionality** of the Streamlit app, including:  

🏡 **Home Page** – Introduction and navigation.  
📊 **Data Explorer** – Enables users to upload and view CSV data.  
📉 **Visualization Dashboard** – Provides interactive charts and insights.  

---

### **3️⃣ `Dockerfile`**  
Blueprint for the Docker environment running Streamlit.  

```dockerfile
# Start with a minimal Python base image
FROM python:3.9-slim  

# Define the working directory
WORKDIR /app  

# Copy and install dependencies
COPY requirements.txt /app/  
RUN pip install --no-cache-dir -r requirements.txt  

# Copy application files
COPY . /app/  

# Open Streamlit’s default port
EXPOSE 8501  

# Launch the Streamlit application
CMD ["streamlit", "run", "src/main.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

---

### **4️⃣ `requirements.txt`**  
Specifies project dependencies:  

```text
streamlit
pandas
numpy
matplotlib
plotly
```

---

## ⚡ **Running the Application**  

### **1️⃣ Move to the Project Directory**  
```bash
cd path/to/project_root
```

### **2️⃣ Build the Docker Image**  
```bash
docker build -t streamlit-app .
```

### **3️⃣ Start the Docker Container**  
```bash
docker run -p 8501:8501 streamlit-app
```

### **4️⃣ Open in Browser**  
🌎 Navigate to → [http://localhost:8501](http://localhost:8501)  

---

## 🎯 **Final Thoughts**  
Congratulations! Your **Streamlit application** is now fully Dockerized and ready to go. 🚀🛳  

![Streamlit App Screenshot](https://github.com/vidhi-jaju/DockSpace/blob/ffeee9124d5ab5508d44ce7cdb2debb5a6ce94b1/2.%20Dockerized%20Streamlit%20Development%20Environment/Images/Screenshot%202025-02-19%20013824.png?raw=true)
![Streamlit App Screenshot](https://github.com/vidhi-jaju/DockSpace/blob/ffeee9124d5ab5508d44ce7cdb2debb5a6ce94b1/2.%20Dockerized%20Streamlit%20Development%20Environment/Images/Screenshot%202025-02-19%20013835.png)
![Streamlit App Screenshot](https://github.com/vidhi-jaju/DockSpace/blob/ffeee9124d5ab5508d44ce7cdb2debb5a6ce94b1/2.%20Dockerized%20Streamlit%20Development%20Environment/Images/Screenshot%202025-02-19%20013853.png)

💡 **What’s Next?**  
🔸 Enhance the Streamlit app with more features.  
🔸 Deploy the containerized app using **AWS, GCP, or Azure**.  
🔸 Experiment with **Docker Compose** for multi-container applications.  

🚀 **Happy Coding!** 🛳💙
