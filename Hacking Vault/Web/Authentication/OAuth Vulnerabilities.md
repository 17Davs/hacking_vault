# 🔑 OAuth 2.0 Security

## 📌 Introduction

- OAuth 2.0 = **authorization framework**, widely used in modern apps.
    
- Provides **delegated access**: one app can access user data from another app without exposing credentials.
    
- Vulnerabilities emerge due to **weak implementations** (CSRF, XSS, open redirects, token leakage, etc.).
    
- OAuth 2.1 is the **secure evolution**, fixing many issues.
    

---

## 🧩 Key Concepts

- **Resource Owner** → The user who owns the data.
    
- **Client** → The app requesting access (e.g., mobile/web app).
    
- **Authorization Server** → Issues tokens after authentication & consent.
    
- **Resource Server** → Hosts the protected resources (e.g., API, DB).
    
- **Authorization Grant** → Temporary credential exchanged for tokens.
    
- **Access Token** → Short-lived credential allowing access.
    
- **Refresh Token** → Long-lived credential for obtaining new tokens.
    
- **Redirect URI** → Registered endpoint where tokens are sent.
    
- **Scope** → Defines what permissions are requested (least privilege).
    
- **State Parameter** → Protects against CSRF attacks.
    
- **Endpoints**:
    
    - `/authorize` → user authentication & consent.
        
    - `/token` → exchange grant for access token.
        

---

## 🔄 OAuth Grant Types

|Grant Type|Use Case|Pros|Cons|
|---|---|---|---|
|**Authorization Code**|Server-side apps|Most secure, supports refresh tokens|More steps|
|**Implicit**|SPAs, mobile apps|Simpler, faster|Insecure (tokens in URL) → deprecated in OAuth 2.1|
|**Password Credentials**|First-party apps|Direct, simple|User shares creds with client → risky|
|**Client Credentials**|Server-to-server|Secure for backend|No user context|

---

## ⚙️ OAuth Flow (Typical)

1. **Client** redirects user to `/authorize` with `client_id`, `redirect_uri`, `scope`, `state`.
    
2. **User** logs in & gives consent.
    
3. **Authorization Server** redirects back with an **authorization code**.
    
4. **Client** exchanges code at `/token` endpoint.
    
5. **Access Token** returned, used in `Authorization: Bearer <token>` header.
    
6. **Optional**: refresh token for session renewal.
    

---

## 🔍 Identifying OAuth in Pentests

- Look for **"Login with Google/Facebook/GitHub"**.
    
- Inspect redirects → `/authorize` requests with parameters:
    
    - `response_type`, `client_id`, `redirect_uri`, `scope`, `state`.
        
- Check **frameworks/libraries**: `django-oauth-toolkit`, `oauthlib`, `passport.js`, `spring-security-oauth`.
    
- Inspect **HTTP headers, error messages, or source code** for framework leaks.
    

---

## 💥 Exploiting OAuth

### 1. Token Hijacking via Redirect_URI

- Misconfigured or overly broad `redirect_uri` → attacker can hijack authorization codes/tokens.
    
- Attack: control a registered redirect domain, steal tokens sent there.
    

### 2. CSRF in OAuth Flow

- Missing/weak `state` parameter → CSRF possible.
    
- Attack: force victim to authorize attacker’s app.
    
- Consequence: victim’s account linked to attacker’s, data exfiltration.
    

### 3. Implicit Flow Token Leakage

- Token returned in URL fragment (`#access_token=...`).
    
- Vulnerabilities:
    
    - Token exposure via XSS.
        
    - Token logged in browser history.
        
    - No refresh tokens, weaker security.
        
- Exploit: malicious JS extracts token and exfiltrates via HTTP request.
    

### 4. Other Common Issues

- **Insufficient Token Expiry** → long-lived tokens = high risk if stolen.
    
- **Replay Attacks** → token reuse if no nonce/timestamp validation.
    
- **Insecure Token Storage** → storing in localStorage/sessionStorage → XSS stealable.
    

---

## 🛡️ Defenses & Best Practices

- ✅ Use **Authorization Code with PKCE** (OAuth 2.1 standard).
    
- ✅ Always validate `redirect_uri` (exact match).
    
- ✅ Enforce **short-lived access tokens** + refresh tokens.
    
- ✅ Implement **state parameter** for CSRF protection.
    
- ✅ Use **HTTPS everywhere**.
    
- ✅ Store tokens in **secure, HttpOnly cookies** (not localStorage).
    
- ✅ Monitor for **token replay** → nonce, timestamp, one-time use.
    

---

## 🚀 OAuth 2.1 Improvements

- 🔒 **Deprecates Implicit Flow** → use Authorization Code with PKCE.
    
- 🔒 **State parameter mandatory**.
    
- 🔒 Stronger **redirect URI validation**.
    
- 🔒 Secure **token storage** recommendations.
    
- 🔒 Better **interoperability & consistency**.
    

---

## 🧪 Pentesting Methodology for OAuth

1. Identify OAuth usage (`/authorize`, `client_id`, `redirect_uri`).
    
2. Test for **open redirect** or weak `redirect_uri`.
    
3. Check `state` → missing, predictable, or reused?
    
4. Look for **token exposure** (URL fragments, logs, HTML).
    
5. Verify **token expiry** and refresh token handling.
    
6. Attempt **replay attacks** with captured tokens.
    
7. Inspect client storage (localStorage, cookies).
    
8. Check for **scope abuse** (overly broad permissions).
    

---

✅ **Key Takeaway**: OAuth 2.0 is powerful but dangerous when misconfigured. OAuth 2.1 fixes many weaknesses — but **pentesters should always test `redirect_uri`, `state`, token handling, and grant types**.
