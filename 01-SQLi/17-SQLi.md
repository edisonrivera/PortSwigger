### Seventeen Exercise 👆


![problem.PNG](/assets/SQLi/Seventeen/problem.PNG)

#### **To do**
```
This lab contains a SQL injection vulnerability in its stock check feature. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables.

The database contains a users table, which contains the usernames and passwords of registered users. To solve the lab, perform a SQL injection attack to retrieve the admin user's credentials, then log in to their account. 
```

1. Click on

![check-stock.PNG](/assets/SQLi/Seventeen/check-stock.PNG)

2. With BurpSuite look the petition

![petition.PNG](/assets/SQLi/Seventeen/petition.PNG)
> Here we can inject our SQLi


3. Know what database is used
   
![db.PNG](/assets/SQLi/Seventeen/db.PNG)

* The web page use **MySQL**
* When our attack is detected the web page don't show information.


4. Use **Hackvertor** to "ocult" our SQLi
   
![hackvertor.PNG](/assets/SQLi/Seventeen/hackvertor.PNG)

5. Access to password from **administrator user**

```sql
1 union select password from users where username='administrator'-- -
```


**Output**

![creds.PNG](/assets/SQLi/Seventeen/creds.PNG)



![login.txt](/assets/SQLi/Eleven/login.PNG)