   

HTTP Enumeration

# **Enumerating HTTP**

## **The basics we’re looking for:**

✅ **Services & Version Info** (Identify server software)  
✅ **Backend Directories** (Find hidden paths)  
✅ **Source Code & Comments** (Look for sensitive info)  
✅ **Vulnerability Scanning** (Check for security flaws)

---

## **Tools**

- **nikto** → Scan for known vulnerabilities
- **dirb / dirbuster / gobuster** → Find hidden directories & files
- **whatweb** → Identify CMS & web technologies
- **curl** → Inspect HTTP headers & methods
- **nmap** → Scan for web services and security flaws

---

## **Commands & Usage**

### **1. Check Server & Version Info**

curl -I <target>        # Get HTTP headers (server type, cookies)
whatweb <target>        # Identify CMS, plugins, and technologies
nmap -p 80,443 --script=http-server-header,http-title <target>  # Detect web server details

```
curl -I <target>        # Get HTTP headers (server type, cookies)
whatweb <target>        # Identify CMS, plugins, and technologies
nmap -p 80,443 --script=http-server-header,http-title <target>  # Detect web server details
```

### **2. Enumerate Hidden Directories**

dirb <target> /usr/share/wordlists/dirb/common.txt    # Basic directory scan
gobuster dir -u <target> -w common.txt -x php,html   # Scan with file extensions
dirsearch -u <target> -e php,html,js                 # Recursive scan for files

```
dirb <target> /usr/share/wordlists/dirb/common.txt    # Basic directory scan
gobuster dir -u <target> -w common.txt -x php,html   # Scan with file extensions
dirsearch -u <target> -e php,html,js                 # Recursive scan for files
```

📌 **Remember:** Apache servers can have important `.php` files.

### **3. Extract Source Code & Comments**

wget -r <target>       # Download full website  
grep -r "password" <target>   # Search for sensitive data

```
wget -r <target>       # Download full website  
grep -r "password" <target>   # Search for sensitive data
```

### **4. Scan for Vulnerabilities**

nikto -h <target>   # Find known security issues  
nmap --script=http-enum,http-vuln-cve2021-44228 <target>   # Scan for exploits

```
nikto -h <target>   # Find known security issues  
nmap --script=http-enum,http-vuln-cve2021-44228 <target>   # Scan for exploits
```

### **5. Find API Endpoints & Hidden Params**

grep -Eo "https?://[a-zA-Z0-9./?=_-]*" <target>.js   # Extract API URLs

```
grep -Eo "https?://[a-zA-Z0-9./?=_-]*" <target>.js   # Extract API URLs
```

---

## **Important Notes**

🔹 **Specify file extensions** if needed (e.g., `.php`, `.html`)  
🔹 **Look for comments in source code** (They might reveal credentials or endpoints)  
🔹 **Check HTTP methods** (`curl -X OPTIONS -i <target>`)

---