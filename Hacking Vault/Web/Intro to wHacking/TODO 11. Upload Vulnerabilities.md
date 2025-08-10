---

# **File Upload Vulnerabilities – Ultimate Practical Summary**

---

### **Why File Upload Vulnerabilities Are Dangerous**

- Allow attackers to upload malicious files leading to:
    
    - Website defacement or content injection (XSS, CSRF)
        
    - Hosting illegal/malicious content
        
    - **Remote Code Execution (RCE)** — attacker gains control over the server as the web user
        
    - Potential privilege escalation and network pivoting
        

---

### **Attacker’s Typical Goals**

- Upload a **webshell** (PHP, ASP, JSP, etc.) to execute commands remotely
    
- Obtain **reverse/bind shells** for interactive access
    
- Overwrite or create critical config files (.htaccess, index.php)
    
- Deliver malware or phishing pages
    

---

### **General Testing & Exploitation Workflow**

1. **Recon & Enumeration**
    
    - Find upload points (form fields, drag-n-drop zones)
        
    - Analyze frontend filters (JavaScript, HTML input restrictions)
        
    - Enumerate files and directories (Gobuster, Burp Suite)
        
    - Identify tech stack and server type via HTTP headers or fingerprints
        
2. **Test Innocent Uploads**
    
    - Upload benign files (images, txt) to:
        
        - Confirm upload success
            
        - Find URL/location of stored files
            
        - Understand naming conventions or transformations
            
3. **Test Malicious Uploads**
    
    - Try uploading scripts (`.php`, `.asp`, `.jsp`, `.phtml`, `.phar`)
        
    - Adjust payload and filename to bypass filters
        
    - Use reverse shell or webshell payloads for execution
        

---

### **Types of Filters and How to Bypass Them**

#### 1. Client-Side Filtering

- Usually JavaScript checks on file extension, size, or type
    
- **Easily bypassed by:**
    
    - Disabling JavaScript
        
    - Intercepting and modifying requests via Burp Suite or curl
        
    - Editing filenames and headers manually
        

#### 2. Server-Side Filtering

- More robust but often flawed
    

|Filter Type|How It Works|Common Bypass Techniques|
|---|---|---|
|**Extension Validation**|Blocks/Allows files by extension|Use alternate extensions (`.phar`, `.pht`), double extensions (`shell.jpg.php`), case variation (`SHELL.PHP`)|
|**MIME Type Validation**|Checks `Content-Type` HTTP header|Spoof MIME type with Burp or curl|
|**Magic Number Validation**|Validates file's initial bytes|Prepend valid image header bytes to payload (polyglot files)|
|**Filename Filtering**|Restricts filename patterns|Use unicode, URL encoding, null byte injection (`%00`) (in legacy systems), or path traversal tricks|
|**File Size Limits**|Restricts size to prevent large uploads|Use small/minified payloads|

---

### **Bypass Tricks & Examples**

- **Double extensions:** `shell.php.jpg` or `shell.jpg.php` depending on check order
    
- **Upper/lower case:** `SHELL.PHP`, `sHeLl.PHp`
    
- **Null byte injection:** `shell.php%00.jpg` (only works on old PHP versions)
    
- **Magic number spoofing:** JPEG header `FF D8 FF E0` + PHP code appended
    
- **MIME spoofing:** Change `Content-Type: image/jpeg` even for `.php` files
    
- **Polyglot files:** Files that are both valid images and scripts simultaneously
    
- **Path traversal:** Upload to directories outside intended folder (`../../shell.php`)
    

---

### **Testing Checklist (Black-box Approach)**

1. Identify file upload points
    
2. Observe frontend restrictions and messages
    
3. Upload allowed files (images, txt) and verify location
    
4. Try forbidden extensions (`.php`, `.asp`) and note errors
    
5. Attempt alternate executable extensions and double extensions
    
6. Spoof MIME types in upload request
    
7. Test magic number prepend or polyglot payloads
    
8. Check for filename filtering bypasses (unicode, encoding, null bytes)
    
9. Confirm file upload location and if accessible/executable
    
10. Attempt to execute uploaded script for shell or command execution
    
11. Escalate access as needed
    

---

### **Defense Best Practices**

- **Validate on server side:** extension, MIME type, magic number
    
- **Use whitelist approach, not blacklist**
    
- Store uploads **outside the web root** or in inaccessible directories
    
- Rename files on upload with randomized names
    
- Strip executable permissions from upload directories
    
- Limit file sizes and scan for malware
    
- Monitor upload logs for suspicious activity
    

---
