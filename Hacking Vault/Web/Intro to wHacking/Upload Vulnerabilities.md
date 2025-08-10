
Key Takeaways

### **Why It’s Dangerous**

- Uploading files without restrictions can lead to:
    
    - Website defacement or content alteration
        
    - XSS / CSRF injection via uploaded pages
        
    - Hosting malicious/illegal content
        
    - **Remote Code Execution (RCE)** – full control of server as web user
        

---

### **General Exploitation Methodology**

1. **Recon & Enumeration**
    
    - Look at page source for client-side filters
        
    - Use Gobuster (`-x` option for extensions) to find upload locations
        
    - Wappalyzer / HTTP headers for tech stack clues
        
    - Intercept with Burp Suite to inspect requests & responses
        
2. **Test Innocent Upload**
    
    - Confirm if and where the file is stored
        
    - Identify naming scheme, accessible URLs
        
3. **Test Malicious Upload**
    
    - Start with known working extensions
        
    - Adjust payload to bypass filters based on error messages
        

---

### **Attacker Goals**

- **Webshell** – Run commands via HTTP parameters
    
- **Reverse/Bind Shell** – Connect back to attacker for interactive access
    

---

### **Common Filtering Types**

#### **Client-Side Filtering**

(Easy to bypass — filtering in browser via JavaScript)

- Methods to bypass:
    
    1. Disable JS in browser
        
    2. Intercept and remove filter code from response (Burp)
        
    3. Intercept upload request & modify parameters (MIME, filename)
        
    4. Send file directly with `curl` or other HTTP client
        

#### **Server-Side Filtering**

(More challenging — filtering happens on the server)

- **Extension Validation**
    
    - Blacklist: Blocks certain extensions (e.g., `.php`, `.phtml`)  
        → Try alternate executable extensions (`.phar`, `.php5`, `.pht`, `.php7`, etc.)
        
    - Whitelist: Allows only listed extensions → harder to bypass, often needs double extensions (`shell.jpg.php`) or exploiting flawed logic
        
- **MIME Validation**
    
    - Checks Content-Type header → spoof via request modification
        
- **Magic Number Validation**
    
    - Checks first bytes in file → prepend correct magic number to payload (`FF D8 FF DB` for JPEG)
        
- **File Length Filtering**
    
    - Size limits can block large shells → use smaller/minified payloads
        
- **Filename Filtering**
    
    - Sanitizes names, avoids overwrites → must hunt for renamed shell
        

---

### **Bypass Examples**

- **Blacklisted Extensions**: Use `.phar` or `.pht`
    
- **Double Extension Trick**: `shell.jpg.php` if filter only checks for `.jpg` anywhere in filename
    
- **Magic Number Spoofing**: Add valid file signature bytes at file start
    
- **MIME Type Spoofing**: Change `Content-Type` in intercepted request
    

---

### **Practical Steps for Black-Box Testing**

1. **Identify accepted file types**
    
2. **Try disallowed file type** (see rejection message)
    
3. **Test alternate extensions**
    
4. **Try double extensions**
    
5. **Test MIME type spoof**
    
6. **Test magic number spoof**
    
7. **Adjust for file size or naming rules**
    
8. **Confirm uploaded file is executable**
    
9. **Execute shell → escalate privileges**
    

---
