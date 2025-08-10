
HTTP Security Headers help protect web applications by mitigating attacks such as XSS, clickjacking, and MIME type sniffing.

Use [https://securityheaders.io/](https://securityheaders.io/ "https://securityheaders.io/") to analyze headers.

---
## Key Security Headers

---

### 🔐 Content-Security-Policy (CSP)

- Helps mitigate **XSS** by restricting sources of content (scripts, styles, images, etc.).

✅ **Example:**

Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'

```
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'
```

✅ **Directives:**

|Directive|Description|
|---|---|
|`default-src`|Default policy for loading content (scripts, images, etc.).|
|`script-src`|Defines trusted sources for JavaScript.|
|`style-src`|Defines trusted sources for CSS stylesheets.|
|`'self'`|Keyword to allow content from same origin only.|

---

### 🛡 Strict-Transport-Security (HSTS)

- Forces browsers to use **HTTPS**, reducing MITM risks.

✅ **Example:**

Strict-Transport-Security: max-age=63072000; includeSubDomains; preload

```
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

✅ **Directives:**

|Directive|Description|
|---|---|
|`max-age`|Time (seconds) to enforce HTTPS.|
|`includeSubDomains`|Apply rule to all subdomains.|
|`preload`|Opt into browser preload lists.|

---

### 🧯 X-Content-Type-Options

- Prevents browsers from **MIME sniffing**, forcing use of `Content-Type` specified by server.

✅ **Example:**

X-Content-Type-Options: nosniff

```
X-Content-Type-Options: nosniff
```

✅ **Directive:**

|Directive|Description|
|---|---|
|`nosniff`|Prevents guessing of MIME types.|

---

### 🔗 Referrer-Policy

- Controls how much **referrer information** is sent with requests (like when clicking a link).

✅ **Examples:**

Referrer-Policy: no-referrer
Referrer-Policy: same-origin
Referrer-Policy: strict-origin
Referrer-Policy: strict-origin-when-cross-origin

```
Referrer-Policy: no-referrer
Referrer-Policy: same-origin
Referrer-Policy: strict-origin
Referrer-Policy: strict-origin-when-cross-origin
```

✅ **Policies:**

|Policy|Description|
|---|---|
|`no-referrer`|Sends no referrer info.|
|`same-origin`|Sends referrer only to same origin.|
|`strict-origin`|Sends only the origin (scheme+host) when protocol is HTTPS→HTTPS.|
|`strict-origin-when-cross-origin`|Sends full URL for same-origin, only origin for cross-origin HTTPS.|

---

## ✅ Quick Answers to Your Questions

|Question|Correct Answer|
|---|---|
|In a CSP configuration, which property can be set to define where scripts can be loaded from?|`script-src`|
|When configuring HSTS to ensure all subdomains also use HTTPS, which directive applies to subdomains?|`includeSubDomains`|
|Which HTTP header directive prevents browsers from interpreting files as a different MIME type?|`X-Content-Type-Options: nosniff`|