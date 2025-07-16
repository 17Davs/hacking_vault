There are three main ways of discovering content on a website which we'll cover. Manually, Automated and OSINT (Open-Source Intelligence).

# Manual discovery 

## Roboots.txt
The robots.txt file is a document that tells search engines witch pages not to index. This file gives us a great list of locations on the website that the owners don't want us to discover as penetration testers.
```txt
#example of content in a roboots.txt file
User-agent: *
Allow: /
Disallow: /staff-portal
```

## Favicon
The favicon is a small icon displayed in the bowser's address bar or tab used for branding a website. 
This sometimes is leftofer from some frameworks after installation and can give us a clue on what is in use. OWAS p hosts a databse of common frameworks icons:  https://wiki.owasp.org/index.php/OWASP_favicon_database

```Bash
root@ip-10-10-42-219:~# curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- 100  1406  100  1406    0     0  25107      0 --:--:-- --:--:-- 100  1406  100  1406    0     0  24666      0 --:--:-- --:--:-- --:--:-- 24241
f276b19aabcb4ae8cda4d22625c6735f  -
```
With that info, searching on the OWASP database, we get:
```
f276b19aabcb4ae8cda4d22625c6735f:cgiirc (0.5.9) 
```

## Sitemap.xml
The sitemap.xml file gives a list of every file the website owner wishes to be indexed. These can sometimes contain areas that are deeper or harder to navigate to or even list some old webpages that still working.

## HTTP Headers
Server response HTTP headers can sometimes contain useful information about softwares and possibily the programming/scripting language in use. This can lead to version information, useful for exploit/vulnerability research for the target.

## Framework Stack
Considering that we have the information about what framework is being used from the previous discovery methods, we can try to lean more about the software and other information, possibly leading to more content we can discover.

# OSINT 

## Google Hacking / Dorking
Utilizes google's advanced search features, which allow us to pick out custom content. 

| **Filter** | **Example**        | **Description**                                              |
| ---------- | ------------------ | ------------------------------------------------------------ |
| site       | site:tryhackme.com | returns results only from the specified website address      |
| inurl      | inurl:admin        | returns results that have the specified word in the URL      |
| filetype   | filetype:pdf       | returns results which are a particular file extension        |
| intitle    | intitle:admin      | returns results that contain the specified word in the title |
## Wappalyzer
Online tool and browser extension that helps identify waht technologies a website uses.
## Wayback Machine
([https://archive.org/web/](https://archive.org/web/)) is a historical archive of websites that dates back to thje late 90s. It shows all the times the service scraped the web pages from a given domain and saved the contents. Can help uncover old pages that may still be active. 
## GitHub
Git is a version control system that tracks changes to files in projects. GitHub is a hosted version of Git on the internet.
We can use GitHub's search feature to look for company names or website names to try and locate repos belonging to a target. Information about source code, password or others can be found.

## S3 Buckets
S2 buckets are a storage service provided by Amazon AWS, allowing file storage and even static website content in the cloud accessible over HTTP/S. The owner is responsible for setting the permissions which  sometimes are set incorreclty and allow unwanted access to sensitive files. 
S3 buckets format:  http(s)://{name}.s3.amazonaws.com. 
These can be found in many ways such as in the pages sources, GitHub repos or automated processes. It is comun to brute-force through terms such as **{name}**-assets, **{name}**-www, **{name}**-public, **{name}**-private, etc.

# Automated Discovery 
Automated discover refers to the process that involves using tools to discover content, using wordlists to feed multiple requests made to the web servers. 

**Using ffuf:**
```shell-session
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://10.10.32.60/FUZZ
```

**Using dirb:**
```shell-session
user@machine$ dirb http://10.10.32.60/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

**Using Gobuster:**
```shell-session
user@machine$ gobuster dir --url http://10.10.32.60/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```