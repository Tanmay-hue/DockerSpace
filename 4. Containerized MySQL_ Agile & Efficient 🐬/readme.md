# 🐬 Setting Up MySQL in a Docker Container with an Initialization Script 🚀  

## ✅ Prerequisites
Before proceeding, ensure you have the following:
- Docker installed on your machine.
- Docker is running.
- An SQL initialization script (**`database_students.sql`**) that contains database and table definitions.

---

## 📂 Project Structure
Organize your files as follows:

```
project-directory/
│── Dockerfile
│── database_students.sql
```
Keeping everything structured ensures a smooth setup process.

---

## 🏗 Step 1: Create the Dockerfile
Inside your project directory, create a **`Dockerfile`** and add the following:

```dockerfile
# 🛠 Base image
FROM mysql:latest

# 📌 Copy the SQL script into the container
COPY database_students.sql /docker-entrypoint-initdb.d/

# 🔓 Expose the default MySQL port
EXPOSE 3306
```

---

## 🗃 Step 2: Define the Database Schema
Create an **`database_students.sql`** file in the same directory with the following content:

```sql
CREATE DATABASE student_db;
USE student_db;

CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);

INSERT INTO students (name, age) VALUES ('Alice', 22), ('Bob', 24);
```

This ensures that your database is set up and preloaded with initial data.

---

## 🔨 Step 3: Build the Docker Image
Run the following command to create your custom MySQL image:

```bash
docker build -t mysql-custom .
```

🔹 This will generate an image named **`mysql-custom`**.

---

## 🚢 Step 4: Run the MySQL Container
Launch a MySQL container using the custom image:

```bash
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=root -d mysql-custom
```

📌 Breakdown:
- **`--name mysql-container`**: Assigns a name to the container.
- **`-e MYSQL_ROOT_PASSWORD=root`**: Sets the root password.
- **`-d`**: Runs the container in detached mode.
- **`mysql-custom`**: Uses the custom image we created.

---

## 🔍 Step 5: Access the Container
To open a terminal session inside the running container, use:

```bash
docker exec -it mysql-container bash
```

---

## 💻 Step 6: Connect to MySQL
Once inside the container, access MySQL with:

```bash
mysql -u root -p
```

🔐 When prompted, enter the root password (**`root`**).

---

## 📊 Step 7: Verify Database and Table
After logging in, confirm that everything is set up correctly.

🔎 List all databases:
```sql
SHOW DATABASES;
```

🔄 Switch to the **student_db** database:
```sql
USE student_db;
```

📋 Check the **students** table:
```sql
SELECT * FROM students;
```

---

## 🎯 Conclusion
Congratulations! 🎉 You have successfully deployed MySQL in a Docker container with an initialization script. This setup ensures that your database is automatically created and populated with initial data each time the container starts.

🚀 **Happy coding!** 🖥️
