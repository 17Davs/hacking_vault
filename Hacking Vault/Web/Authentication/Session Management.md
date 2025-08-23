# 📝 Session Management Notes (TryHackMe)

## 🔑 What is Session Management?

- HTTP is stateless → sessions keep track of authenticated users.
    
- A **session** is created after login and used to:
    
    - Track user state.
        
    - Authorize actions.
        
    - Maintain accountability (logging actions).
        

---

## 🔄 Session Lifecycle

1. **Session Creation** → session value issued after login.
    
    - Must be random, unpredictable, and rotated after authentication.
        
    - Weak session IDs (e.g., base64(username)) → guessable.
        
    - **Session Fixation**: if the same session persists from pre-login → hijack risk.
        
    - Transmission must be secure (HTTPS, safe redirects).
        
2. **Session Tracking** → session value sent with each request.
    
    - Done via **cookies** or **tokens**.
        
    - Vulnerabilities:
        
        - **Authorization bypass** (vertical = admin functions, horizontal = other users’ data).
            
        - **Insufficient logging** → hard to investigate incidents.
            
3. **Session Expiry**
    
    - Sessions should expire after inactivity.
        
    - Excessive lifetimes = risk of hijacking.
        
    - Long-life sessions should monitor location/IP changes.
        
4. **Session Termination**
    
    - Logout should **invalidate sessions server-side** (not only client-side).
        
    - Otherwise, attackers can still use stolen/old tokens.
        
    - Tokens may need blocklists if lifetime is embedded.
        

---

## 🍪 Cookies vs 🔑 Tokens

**Cookies**

- Auto-handled by browser (`Set-Cookie`).
    
- Security flags:
    
    - `Secure`, `HttpOnly`, `SameSite`, `Expire`.
        
- Vulnerable to CSRF if not protected.
    

**Tokens (JWT, Bearer)**

- Stored in LocalStorage, sent manually by client code.
    
- No built-in protections → must secure them manually.
    
- Resistant to CSRF (not auto-sent by browser).
    
- Work better in decentralized apps.
    

---

## ⚠️ Common Session Vulnerabilities

- Weak/predictable session IDs.
    
- Session fixation (session not rotated after login).
    
- Insecure session transmission (e.g., open redirects in SSO).
    
- Authorization bypass (vertical & horizontal).
    
- Excessive session lifetimes.
    
- Missing/insufficient server-side termination.
    
- Lack of logging/accountability.
    

---

## 🛡️ Defenses

- Strong, random, signed session IDs/tokens.
    
- Rotate session on login.
    
- Enforce HTTPS, set cookie flags properly.
    
- Use authorization checks on **every request**.
    
- Reasonable session lifetimes (shorter for sensitive apps like banking).
    
- Proper logout: invalidate server-side sessions.
    
- Log all user actions for accountability.
    

---

✅ **Key Takeaways**

- Sessions = identity + authorization after login.
    
- Secure the entire lifecycle: creation → tracking → expiry → termination.
    
- Both **cookies** and **tokens** have trade-offs — must apply defenses accordingly.
    
- Biggest risks: fixation, weak IDs, excessive lifetime, improper termination.
    
- Good logging & accountability = crucial for investigations.
    

---
