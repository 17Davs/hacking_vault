   

Gobuster

# Gobuster Cheat Sheet

**Gobuster** is a fast directory and file brute-forcing tool written in Go. It is commonly used to discover hidden directories, files, DNS subdomains, and S3 buckets.

---

## 🔥 Common Usage

### 1️⃣ Directory/File brute-forcing (dir mode)

gobuster dir -u http://target.com/ -w /path/to/wordlist.txt

```
gobuster dir -u http://target.com/ -w /path/to/wordlist.txt
```

### 2️⃣ DNS subdomain brute-forcing (dns mode)

gobuster dns -d target.com -w /path/to/wordlist.txt -t 50

```
gobuster dns -d target.com -w /path/to/wordlist.txt -t 50
```

### 3️⃣ Virtual host brute-forcing (vhost mode)

gobuster vhost -u http://target.com -w /path/to/wordlist.txt

```
gobuster vhost -u http://target.com -w /path/to/wordlist.txt
```

---

## 🚀 Important Options

|Flag|Description|
|---|---|
|`-u <URL>`|Target URL|
|`-w <wordlist>`|Path to wordlist file|
|`-t <threads>`|Number of concurrent threads (default: 10)|
|`-x <ext>`|File extensions to search (comma-separated)|
|`-o <file>`|Output results to a file|
|`-s <statuscodes>`|Show specific HTTP status codes (e.g., `200,204,301,302,307,401,403`)|
|`-b <statuscodes>`|Hide status codes (e.g., `404`)|
|`-k`|Skip TLS verification (insecure)|
|`-r`|Follow redirects|
|`-c <cookie>`|Set cookies|
|`-H "Header: value"`|Add custom HTTP header|
|`-l`|Show full URL in output|
|`-q`|Quiet mode (only results)|
|`--timeout <time>`|HTTP timeout (default: 10s)|

---

## 🎯 Examples

### Directory bruteforce with specific extensions

gobuster dir -u http://target.com/ -w common.txt -x php,txt -t 50

```
gobuster dir -u http://target.com/ -w common.txt -x php,txt -t 50
```

### Hide 404 responses

gobuster dir -u http://target.com/ -w common.txt -b 404

```
gobuster dir -u http://target.com/ -w common.txt -b 404
```

### Show only 200,301,302 responses

gobuster dir -u http://target.com/ -w common.txt -s 200,301,302

```
gobuster dir -u http://target.com/ -w common.txt -s 200,301,302
```

### Save output to file

gobuster dir -u http://target.com/ -w common.txt -o results.txt

```
gobuster dir -u http://target.com/ -w common.txt -o results.txt
```

### DNS subdomain scan

gobuster dns -d target.com -w subdomains.txt -t 100

```
gobuster dns -d target.com -w subdomains.txt -t 100
```

### Virtual host discovery

gobuster vhost -u http://target.com -w vhosts.txt -t 50

```
gobuster vhost -u http://target.com -w vhosts.txt -t 50
```

---

## ⚙️ Useful Wordlists

- **Common directories & files:**  
    `/usr/share/wordlists/dirb/common.txt`  
    `/usr/share/seclists/Discovery/Web-Content/`
    
- **Subdomains:**  
    `/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt`
    

---

## ⚡ Quick tips

✅ Always adjust `-t` (threads) based on server responsiveness (20-50 is usually safe).  
✅ Use `-k` if dealing with invalid SSL certs.  
✅ Combine with `-x` to brute-force file extensions.  
✅ Review with `-o` and grep for post-analysis.