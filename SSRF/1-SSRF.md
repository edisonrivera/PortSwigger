### First Exercise 🐱‍🚀


![problem.PNG](/assets/SSRF/First/problem.PNG)

#### **To do**
```
To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos. 
```


1. Check the petition of stock with **BurpSuite**
   
![petition.PNG](/assets/SSRF/First/petition.PNG)

* To check the stock, the web page do petition of API.


2. Put `http://localhost/admin` in the **stockApi** and send the petition.

![ssrf.PNG](/assets/SSRF/First/ssrf.PNG)


3. Look the result:
   
![result.PNG](/assets/SSRF/First/result.PNG)



4. Check what append if you click on button **delete** together **carlos**

![delete_user.PNG](/assets/SSRF/First/delete_user.PNG)


5. With the information recolected, **delete user carlos**

![execute.PNG](/assets/SSRF/First/execute.PNG)

You solve the lab!