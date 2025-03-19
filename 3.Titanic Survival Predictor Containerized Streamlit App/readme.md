# 🌊 **Titanic Survival Predictor:- Containerized Streamlit App**

## 📌 **Overview**
The **Titanic Survival Prediction Model** is a machine learning-based web application that determines the likelihood of a passenger surviving the Titanic disaster. It is developed using **Python**, with **scikit-learn**, **pandas**, and **Streamlit** powering the backend and frontend. The application is packaged with **Docker** to facilitate seamless deployment and execution across different environments.

---

## 📂 **Project Structure**

```bash
Titanic-Prediction-Model/
│── Dockerfile
│── requirements.txt
│── main.py
│── titanic_model.py
│── titanic_model.pkl
```

### **📜 File Descriptions:**
- **`main.py`** → The primary script for the Streamlit-based user interface.
- **`titanic_model.py`** → Contains the logic to train and save the Titanic survival prediction model.
- **`titanic_model.pkl`** → Pre-trained machine learning model stored for quick predictions.
- **`requirements.txt`** → Lists dependencies required for the application.
- **`Dockerfile`** → Defines the containerization instructions using Docker.

---

## 🤖 **Model Training (`titanic_model.py`)**
The model utilizes a **Random Forest Classifier** from `scikit-learn` to analyze Titanic dataset features. Once trained, the model is stored as **`titanic_model.pkl`** using `joblib` for efficient retrieval within the web application.

### **Key Steps in `titanic_model.py`**
1. **Load and preprocess the Titanic dataset**.
2. **Handle missing values and encode categorical features**.
3. **Train the Random Forest Classifier**.
4. **Save the trained model** in a serialized format.

---

## 🎨 **Streamlit Web Application (`main.py`)**
This interactive Streamlit-based web app provides an intuitive interface where users can enter passenger details and receive real-time predictions regarding survival chances.

### **✨ Features:**
✔️ **Simple, responsive, and easy-to-use interface**  
✔️ **Instant survival prediction based on user input**  
✔️ **Interactive sliders and dropdowns for seamless input selection**  

---

## 🐳 **Docker Integration**
The project is containerized using **Docker**, ensuring it runs consistently across different systems without dependency conflicts.

### **📄 `Dockerfile`**
```dockerfile
# Use Python 3.12 slim as base image
FROM python:3.12-slim

# Set working directory
WORKDIR /app

# Copy required files
COPY requirements.txt requirements.txt
COPY main.py main.py
COPY titanic_model.pkl titanic_model.pkl

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose the application port
EXPOSE 8501

# Run the Streamlit app
CMD ["streamlit", "run", "main.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

---

## 🚀 **Running the Application via Docker**
Follow these steps to containerize and launch the application:

### **1️⃣ Navigate to the Project Directory**
```bash
cd Titanic-Prediction-Model
```

### **2️⃣ Build the Docker Image**
```bash
docker build -t titanic-prediction .
```

### **3️⃣ Run the Docker Container**
```bash
docker run -p 8501:8501 titanic-prediction
```

### **4️⃣ Access the Application**
Open a web browser and go to:
```
http://localhost:8501
```

![Streamlit App](https://github.com/Tanmay-hue/DockerSpace/blob/main/3.Titanic%20Survival%20Predictor%20Containerized%20Streamlit%20App/img2.png)

---

## 🎯 **Final Thoughts**
This project highlights the deployment of a **machine learning model** using **Streamlit** and **Docker**. By containerizing the app, deployment becomes straightforward, ensuring compatibility across different platforms.

### 🔥 **Future Enhancements:**
- 🌐 **Deploy the application** on **AWS, GCP, or Vercel**.
- 🎨 **Enhance the UI** with additional **Streamlit widgets and visualizations**.
- 🧠 **Optimize the model performance** through further **feature engineering**.

⚡ **Happy Coding & Containerizing!** 🛳️🐳

