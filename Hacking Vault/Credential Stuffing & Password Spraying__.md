   

Credential Stuffing & Password Spraying**

# **Credential Stuffing & Password Spraying**

## **1. Understanding Credential Stuffing & Password Spraying**

|Attack Type|Description|When to Use|
|---|---|---|
|**Credential Stuffing**|Using leaked username-password pairs from data breaches to attempt logins on other platforms.|When targeting accounts that may have **reused** credentials from a breached database.|
|**Password Spraying**|Trying a few common passwords across many accounts to avoid account lockouts.|When brute force is not possible due to **lockout policies** (e.g., after 3 failed attempts).|

**⚠️ Important:** Before performing any credential-based attack, always check with the **client** about their **password policies** to avoid accidental account lockouts.

---

## **2. Credential Stuffing with Burp Suite & FoxyProxy**

### **Installing & Configuring FoxyProxy for Burp Suite**

FoxyProxy is a browser extension that makes it easier to toggle Burp Suite as a proxy.

#### **Installation**

- **Firefox:** Install from [FoxyProxy for Firefox](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/ "https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/")
- **Chrome:** Install from [FoxyProxy for Chrome](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp/ "https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp/")

#### **Setup for Burp Suite**

1. Open **FoxyProxy** in your browser.
2. Add a **New Proxy**:
    - **IP:** `127.0.0.1`
    - **Port:** `8080`
    - **Protocol:** HTTP
3. Enable it when intercepting with **Burp Suite**.

---

### **Credential Stuffing with Burp Intruder**

1. Open **Burp Suite** → **Proxy** → Intercept a login request.
2. Send the request to **Intruder** (`Right-click → Send to Intruder`).
3. Select the **Attack Type: Cluster Bomb**.
4. Add **positions** for usernames and passwords.
5. Load **username-password lists** (e.g., from breach databases).
6. Start the attack and analyze responses (`200 OK` or different response lengths indicate valid logins).

---

## **3. Useful Credential Sources for Stuffing**

|Source|Description|
|---|---|
|[dehashed.com](https://dehashed.com/ "https://dehashed.com/")|Search breached credentials by email, username, or domain.|
|[haveibeenpwned.com](https://haveibeenpwned.com/ "https://haveibeenpwned.com/")|Check if an email/password has been compromised.|
|[hashes.org](https://hashes.org/ "https://hashes.org/")|Community-driven hash cracking database.|
|[breach-parse (GitHub)](https://github.com/hmaverickadams/breach-parse "https://github.com/hmaverickadams/breach-parse")|Parse large breached credential dumps.|

---

## **4. Preventing Credential Stuffing & Password Spraying**

- Use **Multi-Factor Authentication (MFA)**
- Implement **CAPTCHAs** on login pages
- Monitor for **failed login attempts**
- Enforce **unique passwords** across services
- Detect credential reuse from breach data

---