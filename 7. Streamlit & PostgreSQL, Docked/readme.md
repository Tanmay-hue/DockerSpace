# Deploying a Streamlit App with PostgreSQL in Docker

## 🌟 Introduction
This guide walks you through the process of deploying a **Streamlit application** that interacts with a **PostgreSQL database**, all within **Docker containers**. The app retrieves and displays passenger data stored in the database, ensuring a smooth and portable setup.

---

## 📂 Project Directory Structure
```
Streamlit-Postgres-Docker/
│── Dockerfile
│── main.py
```

### 📜 File Descriptions:
- **main.py** – Streamlit application that connects to the PostgreSQL database and fetches records.
- **Dockerfile** – Defines the container environment for running the Streamlit app.

---

## 🛠 Setting Up PostgreSQL with Docker
### Step 1: Pull the PostgreSQL Image
```sh
docker pull postgres
```

### Step 2: Create a Docker Network
```sh
docker network create my_postgres_network
```
This ensures seamless communication between the PostgreSQL and Streamlit containers.

### Step 3: Run a PostgreSQL Container
```sh
docker run --name my_postgres_container --network my_postgres_network -e POSTGRES_USER=tanmay -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=testdb -p 5432:5432 -d postgres
```
This command launches a PostgreSQL container with authentication credentials.

---

## 🏗 Setting Up the Database
### Step 4: Connect to PostgreSQL
```sh
docker exec -it my_postgres_container psql -U tanmay -d testdb
```

### Step 5: Create the `passengers` Table
```sql
CREATE TABLE passengers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    location VARCHAR(100)
);
```

### Step 6: Insert Sample Data
```sql
INSERT INTO passengers (name, location) VALUES
('Tanmay', 'Pathankot'),
('Aryan', 'Jind'),
('Coach Saab', 'Atta');
```

---

## 🎨 Streamlit App (`main.py`)
The application connects to PostgreSQL, fetches records, and presents them in an intuitive UI.

### 🚀 Features:
- Establishes a database connection using **psycopg2**.
- Dynamically retrieves and displays data.
- Applies **custom styling** for an improved user experience.

---

## 📦 Building a Docker Image for Streamlit
### Step 7: Write the `Dockerfile`
```dockerfile
FROM python:3.9
WORKDIR /app
COPY main.py .
RUN pip install streamlit psycopg2
CMD ["streamlit", "run", "main.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

---

## 🚀 Running the Streamlit App in Docker
### Step 8: Build the Docker Image
```sh
docker build -t streamlit_app .
```

### Step 9: Launch the Streamlit Container
```sh
docker run --name my_streamlit_container --network my_postgres_network -p 8501:8501 -d streamlit_app
```
This step allows the Streamlit app to interact with the PostgreSQL database.

---

## 🔗 Accessing the Application
Open your web browser and visit:
👉 **[http://localhost:8501](http://localhost:8501)**

You should see a table displaying the list of passengers.

---

## 📌 Conclusion
✅ PostgreSQL stores and manages passenger data.  
✅ Streamlit retrieves and presents the data interactively.  
✅ Both containers communicate efficiently within **my_postgres_network**.  
✅ The web interface is accessible via **http://localhost:8501**.  

This setup provides a **fully containerized solution** for data visualization using **Streamlit and PostgreSQL**. 🚀

