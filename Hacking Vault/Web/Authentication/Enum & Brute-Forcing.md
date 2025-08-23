# 🔑 Authentication — Enumeration & Brute Forcing

## 📌 What is Enumeration in Authentication?

- Process of identifying **valid usernames, password policies, and flaws** in authentication mechanisms.
    
- Acts as a **prelude to brute force attacks**, reducing guesswork and improving efficiency.
    
- Often relies on differences in **application responses** (verbose errors, status codes, timing, etc.).
    

---

## 🔍 Common Enumeration Targets

### 1. **Valid Usernames**

- Error message differences (`user not found` vs `wrong password`).
    
- Registration pages (username/email availability checks).
    
- Password reset pages (different messages for valid/invalid users).
    
- Verbose login errors exposing account existence.
    
- Leaked/breached credential reuse.
    

### 2. **Password Policies**

- Error messages may disclose regex rules (e.g., must contain uppercase, digit, symbol).
    
- Helps attackers **craft custom wordlists**.
    

### 3. **Verbose Errors** (Info disclosure)

- Reveal:
    
    - File paths / internal structure.
        
    - Database info (tables, schema).
        
    - User details (valid usernames, email formats).
        
- Often induced via:
    
    - Invalid logins.
        
    - SQL Injection (`'` in input).
        
    - Path traversal (`../../`).
        
    - Form manipulation.
        
    - Application fuzzing (Burp Intruder, wfuzz, etc.).
        

---

## ⚙️ Automation (Enumeration Scripts)

- **Python/Requests** or **Burp Intruder** to test email/username lists.
    
- Logic:
    
    - Submit login with known bad password.
        
    - Detect difference in error response (`Email does not exist` vs `Invalid password`).
        
- Tools: custom scripts, SecLists wordlists, Burp Intruder.
    

---

## 🔐 Password Reset Flow Vulnerabilities

### Attack Surface:

- **Email-based reset** → relies on email security.
    
- **Security questions** → often guessable from OSINT/PII.
    
- **SMS reset** → exposed to SIM swapping.
    

### Common Issues:

- Predictable reset tokens (e.g., numeric PINs).
    
- Tokens with long/no expiration.
    
- Error messages confirming account existence.
    
- Transmission of reset links without HTTPS.
    

### Exploitation:

- Brute-force predictable tokens (e.g., using **Burp Intruder + Crunch**).
    
- Look for **sequential/short tokens** in reset links.
    

---

## 🔑 Basic Authentication (HTTP)

- Credentials sent as **Base64 in HTTP header**:
    
    ```
    Authorization: Basic <base64(username:password)>
    ```
    
- Weaknesses:
    
    - Easily brute-forced (especially with weak creds).
        
    - Base64 is not encryption.
        
    - Unsafe without HTTPS.
        

### Exploitation:

- Intercept Basic Auth request.
    
- Decode base64 → replace with payload (`username:password`).
    
- Burp Intruder with **wordlists** (e.g., `500-worst-passwords.txt`).
    
- Payload processing:
    
    1. Append `username:` before password.
        
    2. Base64 encode.
        

---

## 🕵️‍♂️ Extra Enumeration Sources

- **Wayback Machine**: Find old endpoints/directories.
    
    - Tool: `waybackurls`.
        
- **Google Dorks**: Search exposed files/admin panels.
    
    - Examples:
        
        - `site:example.com inurl:admin`
            
        - `filetype:log "password" site:example.com`
            
        - `intitle:"index of" "backup" site:example.com`
            

---

## 📌 Key Takeaways

- Enumeration reduces brute-force noise by targeting **only valid accounts**.
    
- Verbose errors & password reset flows are major **info disclosure risks**.
    
- Brute forcing should leverage **wordlists tailored to password policies**.
    
- Basic Auth is highly vulnerable if not paired with **HTTPS + strong creds**.
    
- Tools: **Burp Suite, SecLists, Crunch, waybackurls, Google Dorks**.
    
- Always conduct attacks ethically & with authorization.
    

---

Would you like me to now make the **next module notes** (Session Management) in the **same style/format** so your whole Authentication section stays consistent?