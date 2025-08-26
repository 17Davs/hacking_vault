
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
Although, the Forgot Password, allows for valid email enumeration, since it displays an **"Invalid Email address"** if the email is not registered. 
Confirmed the valid email tester@hammer.thm from the previously acquired knowledge:

![](../../Pasted%20image%2020250826011653.png)
We are asked for the 4-digit code sent to the email and a 180 seconds countdown starts...
Tried a random number to submit and get a look of the request and response in Burp:

![](../../Pasted%20image%2020250826015807.png)

Here, I got the information that during the 180 second, I have a 6 tries before hitting the rate limit. Repeated the request to confirm the restriction and it indeed works:
![](../../Pasted%20image%2020250826234429.png)

So, at this point I am thinking, **Is the rate limiting associated to the Session?** 
It was the only logical option for this functionality to be vulnerable to brute-forcing otherwise I needed to be lucky to catch the correct 4 digit code in only 6 tries before getting blocked.

## Confirming the idea 

First, I checked if the seconds parameter from the request affects the results or availability of the functionality, turns out it doesn't which is a big point for my brute-force idea.  
Then, prepared a second repeater tab, with no cookie value to request for a new session to try and see if the rate limit header value starts from 6, ignoring a previously sent tentative:

![](../../Pasted%20image%2020250827001050.png)
Got blocked with the original session. 

![](../../Pasted%20image%2020250827001246.png)
Got a new session cookie to use.

![](../../Pasted%20image%2020250827001436.png)
Sent two just to confirm xd. The rate limiting is reset to 8 tries using a new session. This means, it is possible to bypass the rate limiting mechanism creating a new session for each 7 requests and try possible 4-digit codes in the 180 seconds interval (each session).






