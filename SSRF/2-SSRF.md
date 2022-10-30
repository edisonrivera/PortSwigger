### Second Exercise 🐯


![problem.PNG](/assets/SSRF/Second/problem.PNG)

#### **To do**
```
To solve the lab, use the stock check functionality to scan the internal 192.168.0.X range for an admin interface on port 8080, then use it to delete the user carlos.  
```

1. Inspect te petition of stock with **BurpSuite**

![petition.PNG](/assets/SSRF/Second/petition.PNG)


2. We have to find the correct IP address in range 192.168.0.[0-244]
* To do this use Burpsuite, send the petition to **Intruder** (push Ctrl + i)
* Next, select last number in IP address and do this
![intruder1.PNG](/assets/SSRF/Second/intruder1.PNG)
![intruder2.PNG](/assets/SSRF/Second/intruder2.PNG)


![steps.PNG](/assets/SSRF/Second/steps.PNG)

* Finally, click on **Start Attack**



3. Check the petition with **Code 200**

![code-200.PNG](/assets/SSRF/Second/code-200.PNG)
   

4. Visit the URL http://192.168.0.[Port]:8080/admin

![petition-2.PNG](/assets/SSRF/Second/petition-2.PNG)


5. Check the code page
   
![code-page.PNG](/assets/SSRF/Second/code-page.PNG)


6. Put a new URL to **delete user carlos**
![delete-carlos.PNG](/assets/SSRF/Second/delete-carlos.PNG)


You solver the lab!