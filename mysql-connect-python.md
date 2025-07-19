# Connecting MySQL with Python on Ubuntu WSL 


`This guide will walk you through how to connect MySQL with Python using mysql-connector-python on Ubuntu WSL.`


✅ Prerequisites
`Make sure you have:`

- Python 3 installed

- MySQL installed and running on Ubuntu WSL

- A MySQL user (like root) and password

- mysql-connector-python package



## Step 1: Create and Configure MySQL on Ubuntu WSL
1. Install MySQL Server
```
sudo apt update
sudo apt install mysql-server
```

2. Start MySQL Server

```
sudo service mysql start
```
3. Login to MySQL (as root)
```bash

sudo mysql -u root
```

4. Set Root Password (if not already)
```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YourPassword123';
FLUSH PRIVILEGES;
```

## Step 2: Install MySQL Connector for Python
```bash

pip3 install mysql-connector-python
```
✅ Output:

```
Successfully installed mysql-connector-python-9.x.x
```

## Step 3: Create Python Script to Connect to MySQL
Create a file called connect_mysql.py:

```bash

vim connect_mysql.py
```

Paste this code:
```python
import mysql.connector
from mysql.connector import Error

try:
    conn = mysql.connector.connect(
        host="localhost",
        user="root",
        password="NewPassword123"
    )
    if conn.is_connected():
        print("✅ Connection successful!")

except Error as e:
    print(f"❌ Error: {e}")

finally:
    if 'conn' in locals() and conn.is_connected():
        conn.close()


```

### Step 4: Run the Python Script
```bash

python3 connect_mysql.py
```

✅ Output:

```pgsql

✅ Connection successful!
```
---

### 🎯 BONUS: CRUD Operation Example
Here’s a basic example to perform a SELECT query:

`Create mysql_crud.py:`
```python
import mysql.connector

# Connect to MySQL
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="NewPassword123"
)

cursor = conn.cursor()

# Create Database and Use it
cursor.execute("CREATE DATABASE IF NOT EXISTS testdb")
cursor.execute("USE testdb")

# Create Table
cursor.execute("""
    CREATE TABLE IF NOT EXISTS users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(100),
        email VARCHAR(100)
    )
""")

# Insert Data
cursor.execute("INSERT INTO users (name, email) VALUES (%s, %s)", ("Anas", "anas@example.com"))
conn.commit()

# Read Data
cursor.execute("SELECT * FROM users")
rows = cursor.fetchall()
print("📋 Users:")
for row in rows:
    print(row)

conn.close()
```
run this command 

`python3 mysql_crud.py`
output:
`
📋 Users:
(1, 'Anas', 'anas@example.com')
`
