# 🚢 Evidently AI Sets Sail in Docker: A Voyage into Data Monitoring 🐳📊

## 📌 Overview

This guide explains how to set up an `Evidently AI` dashboard within a `Streamlit` application and run it inside a `Docker` container. With this setup, you can:

- Monitor machine learning models effectively.
- Interact with a dynamic dashboard powered by `Streamlit`.
- Manage reports and projects efficiently.
- Leverage `Docker` for seamless deployment and scalability.

---

## 📂 Directory Structure

Ensure your project directory includes the following components:

```
📁 evidently-ai-streamlit
 ├── 📂 projects                # Houses ML monitoring projects
 │    ├── 📂 project_1
 │    │    ├── 📂 reports       # Stores monitoring reports
 │    │    ├── ...
 │    ├── 📂 project_2
 │    │    ├── 📂 reports
 │    │    ├── ...
 │    ├── ...
 │
 ├── 📂 src                     # Python scripts for UI and utilities
 │    ├── ui.py                 # UI components
 │    ├── utils.py              # Helper functions
 │    ├── ...
 │
 ├── 📂 static                  # Static assets like CSS and images
 │    ├── style.css             # Custom styling
 │    ├── ...
 │
 ├── 📄 app.py                   # Main Streamlit application
 ├── 📄 Dockerfile               # Docker configuration for the app
 ├── 📄 requirements.txt          # Lists dependencies
 ├── 📄 README.md                 # Documentation
```

---

## 📝 Application Core (`app.py` Overview)

The `app.py` script manages the following functionalities:

- Dynamically loads projects and available reports.
- Provides user-friendly project selection and period filtering.
- Integrates `Evidently AI` reports seamlessly within `Streamlit`.
- Implements error handling for missing reports or projects.
- Utilizes `src/ui.py` for UI rendering and `src/utils.py` for backend logic.

Key functions include:

- `display_sidebar_header()`: Creates a sidebar for navigation.
- `select_project()`: Allows users to choose a project.
- `select_period()`: Enables selection of reporting periods.
- `select_report()`: Retrieves and lists available reports.
- `display_report()`: Loads and displays selected reports interactively.

---

## 🐳 Docker Configuration (`Dockerfile`)

```dockerfile
# Use Python base image
FROM python:3.10

# Define working directory inside the container
WORKDIR /app

# Copy dependencies and install them
COPY requirements.txt /app/
RUN pip install --no-cache-dir --break-system-packages -r requirements.txt

# Copy the full project into the container
COPY . /app/

# Expose the Streamlit port
EXPOSE 8501

# Run the Streamlit app
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

---

## 📦 Python Dependencies (`requirements.txt`)

```txt
category_encoders==2.6.0
evidently==0.2.6
jupyter==1.0.0
jupyter_contrib_nbextensions==0.7.0
matplotlib==3.7.0
numpy==1.24.2
pandas==1.5.3
pyarrow==11.0.0
python-box==5.4.1
requests==2.28.2
streamlit==1.19.0
pyyaml==5.1
scikit-learn==1.2.1
scipy==1.10.1
seaborn==0.12.2
altair==4.0
```

---

## 🚀 How to Run the Application

### 1️⃣ Clone the Repository & Navigate to the Project

```sh
git clone <repo-link>
cd evidently-ai-streamlit
```

### 2️⃣ Build & Run the Docker Container

```sh
docker build -t evidently-streamlit .
docker run -p 8501:8501 evidently-streamlit
```

### 3️⃣ Open the Streamlit App

Visit [http://localhost:8501](http://localhost:8501) in your browser.

![Streamlit Dashboard](https://github.com/Tanmay-hue/DockerSpace/blob/main/8.%20Evidently%20AI%20Sets%20Sail%20in%20Docker/image.png)

---

## 🎯 Summary

- ✅ Successfully deployed an `Evidently AI` dashboard with `Streamlit` inside `Docker`.
- ✅ Implemented dynamic project-based report selection.
- ✅ Used Docker for streamlined deployment and scalability.
- ✅ Organized the code into modular components for better maintenance.

---

## 🔜 Future Enhancements

🔹 Implement authentication for secure project access.
🔹 Enable report comparison across different time periods.
🔹 Deploy on cloud platforms such as AWS/GCP for global accessibility.

💡 Keep innovating and happy coding! 🚀

