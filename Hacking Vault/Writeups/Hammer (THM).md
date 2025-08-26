
Authentication Bypass and RCE


# Enumeration 

## Nmap Scan

![](../../Pasted%20image%2020250826001827.png)
``` bash
sudo nmap -A -p 22,1337 -T4 hammer.thm -oN hammer.nmap 
```

![](../../Pasted%20image%2020250826002022.png)

## 1337 Web App Enumeration

``` bash
dirsearch -u http://hammer.thm:1337 -r -o endpoints.dirsearch 
```
Didn't find much other than the `/phpmyadmin` (now we now it is using php), some `/vendor` :
![](../../Pasted%20image%2020250826003623.png)
At the same time, visited the site manually and found some useful information on the source page

![](../../Pasted%20image%2020250826003009.png)
This indicates that possibly we need to use `hmr_` as a prefix in our enumeration.

Used the build-in prefix parameter in dirsearch: 
``` bash
dirsearch --help | grep prefix
    --prefixes=PREFIXES     Add custom prefixes to all wordlist entries
```
So, the command used was:
``` bash
dirsearch -u http://hammer.thm:1337 --prefixes=hmr_ -o prefixed.dirsearch
```
![](../../Pasted%20image%2020250826004513.png)Found `hmr_logs` directory, with directory listing and `errors.log` file:

![](../../Pasted%20image%2020250826005759.png)
Great, looks like some information:
- username enumeration: tester@hammer.thm
- possible directory discovery: `/restricted-area`, `/admin-login`, `/protected`, `/locked-down`
- System user leak: `hammmerthm` user from `/home/hammerthm/test.php`
-  Apparently Lock-down mechaniosm in place 


# Bypassing

## Overview of the login page
Login page does not provide username enumeration since incorrect login cause the display of a generic message.
![](../../Pasted%20image%2020250826011548.png)
Although, the Forgot Password, allows for valid email enumeration, since it displays an **"Invalid Email address"** if the email is not registered. Confirmed the valid email tester@hammer.thm from the previously acquired knowledge:

![](../../Pasted%20image%2020250826011653.png)
We are asked for the 4-digit code sent to the email and a 180 seconds countdown starts...

![](../../Pasted%20image%2020250826015807.png)

