### First Exercise 👆


![problem.PNG](/assets/SQLi/First/problem.PNG)

#### **To do**


```
To solve the lab, perform an SQL injection attack that causes the application to display details of all products in any category, both released and unreleased. 
```

![first-exercise.PNG](/assets/SQLi/First/first_exercise.PNG)

Explanation:
1) **Close quotiation marks** to force close a query for after inject our sql code.
2) **Query all products**, `1=1` always true so, all products are show.
3) **Query products released and unreleased** because the problem put this condition.
4) Use `-- -` to comment rest of query.