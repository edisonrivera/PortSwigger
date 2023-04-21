### Fourth Exercise 👆


![problem.PNG](/assets/SQLi/Fourth/problem.PNG)

#### **To do**

```
The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform an SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data.  
```


1. Aplicate **UNION SELECT** but in this case, print a string.
![solution.PNG](/assets/SQLi/Fourth/solution.PNG)

**Explanation**
![explanation.PNG](/assets/SQLi/Fourth/explanation.PNG)

We can try put the string in any position, because, not all field are available to represent command or string. In this case only **field 2 is available**.