   


# **Credential Stuffing & Password Spraying**

## **Understanding Credential Stuffing & Password Spraying**

|Attack Type|Description|When to Use|
|---|---|---|
|**Credential Stuffing**|Using leaked username-password pairs from data breaches to attempt logins on other platforms.|When targeting accounts that may have **reused** credentials from a breached database.|
|**Password Spraying**|Trying a few common passwords across many accounts to avoid account lockouts.|When brute force is not possible due to **lockout policies** (e.g., after 3 failed attempts).|

## **Useful Credential Sources for Stuffing**

|Source|Description|
|---|---|
|[dehashed.com](https://dehashed.com/ "https://dehashed.com/")|Search breached credentials by email, username, or domain.|
|[haveibeenpwned.com](https://haveibeenpwned.com/ "https://haveibeenpwned.com/")|Check if an email/password has been compromised.|
|[hashes.org](https://hashes.org/ "https://hashes.org/")|Community-driven hash cracking database.|
|[breach-parse (GitHub)](https://github.com/hmaverickadams/breach-parse "https://github.com/hmaverickadams/breach-parse")|Parse large breached credential dumps.|

---

## **Preventing Credential Stuffing & Password Spraying**

- Use **Multi-Factor Authentication (MFA)**
- Implement **CAPTCHAs** on login pages
- Monitor for **failed login attempts**
- Enforce **unique passwords** across services
- Detect credential reuse from breach data

---