   
# **Google Fu for Ethical Hacking**

## **1. What is Google Fu?**

Google Fu refers to advanced Google Search techniques (Google Dorking) used for reconnaissance, vulnerability identification, and gathering sensitive information. It's a powerful tool for ethical hackers during the information-gathering phase of an engagement.

---

## **2. Key Search Operators**

### **Basic Operators**

- **`site:`** – Restrict search to a specific website.  
    Example: `site:example.com`
- **`intitle:`** – Search for words in the title of a page.  
    Example: `intitle:"index of"`
- **`inurl:`** – Search for words in the URL.  
    Example: `inurl:admin`
- **`filetype:`** – Search for specific file types.  
    Example: `filetype:pdf`
- **`cache:`** – View Google's cached version of a page.  
    Example: `cache:example.com`

### **Advanced Dorking Techniques**

- **`intext:`** – Find words within the page text.  
    Example: `intext:"password" filetype:txt`
- **`allinurl:`** – Search for all terms in the URL.  
    Example: `allinurl:"login" "admin"`
- **`link:`** – Find pages linking to a URL.  
    Example: `link:example.com`
- **`related:`** – Find similar websites.  
    Example: `related:example.com`

---

## **3. Combining Operators**

- **Example**:  
    `site:example.com intitle:"index of" filetype:pdf`  
    (Find PDF files in the "index of" directory on a specific website)

---

## **4. Exposed Databases & Files**

Search for exposed files that might contain sensitive data:

- **Example 1**: `filetype:xls inurl:"password"`
- **Example 2**: `filetype:pdf "confidential"`
- **Example 3**: `filetype:log "error"`
- **Example 4**: `filetype:sql "dump"`

---

## **5. Finding Vulnerable Devices/Services**

- **Example 1**:  
    `inurl:"viewerframe?mode=motion" inurl:"/axis-cgi/mjpg/video.cgi"`  
    (Find exposed cameras)
- **Example 2**:  
    `inurl:"phpinfo.php"`  
    (Identify PHP info pages)

---

## **6. Google Hacking Database (GHDB)**

- A repository of Google dorks for security testing:  
    [Google Hacking Database](https://www.exploit-db.com/google-hacking-database "https://www.exploit-db.com/google-hacking-database")

---

## **7. Metadata Search**

Search for files with potentially sensitive metadata:

- **Example 1**:  
    `filetype:pdf "confidential" site:gov`
- **Example 2**:  
    `filetype:docx "private"`

---

## **8. Subdomain & Directory Enumeration**

Use Google to find hidden subdomains or directories:

- **Example**:  
    `site:example.com -www`  
    (Shows subdomains like `mail.example.com`)

---

## **9. Social Engineering with Google**

- Gather public info on employees, companies, or infrastructure:
    - Search job titles or patterns like:  
        `site:linkedin.com "CISO" "email"`

---

## **10. Final Notes**

- Google Fu is a powerful tool for ethical hackers, but use it responsibly and legally.
- Ensure all searches align with ethical hacking practices to avoid illegal activities.

---

## **11. Tools for Google Fu**

|Tool|Description|
|---|---|
|**Google**|Primary search engine for reconnaissance and dorking|
|**Google Hacking Database (GHDB)**|Repository of Google dorks for finding vulnerabilities|
|**Google Dorks**|Pre-configured search queries for discovering exposed information|

---