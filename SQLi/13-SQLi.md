### Thirdteen Exercise 👆


![problem.PNG](/assets/SQLi/First/problem.PNG)

#### **To do**
```
 This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs an SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay.  
```


1. Inject on cookie
![cookie.PNG](/assets/SQLi/Thirdteen/cookie.PNG)

* `pg_sleep(10)` do the page delay to 10 seconds. (Now the page use Posgrest)
