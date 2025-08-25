
# 🔑 Multi-Factor Authentication (MFA)

## 📌 Introduction

- **MFA** = authentication using **two or more verification factors**.
    
- Factors:
    
    1. **Something you know** → password, PIN.
        
    2. **Something you have** → phone, token, smartcard.
        
    3. **Something you are** → biometrics.
        
    4. **Somewhere you are** → IP/geolocation.
        
    5. **Something you do** → behavior (typing speed, mouse movement).
        

👉 **2FA is a subset of MFA** (uses exactly 2 factors). All 2FA = MFA, but not all MFA = 2FA.

---

## 🧪 Types of MFA / 2FA

- **TOTP (Time-Based OTP)** → codes valid ~30s (Google Authenticator, Authy).
    
- **Push Notifications** → approve/deny login from device.
    
    - Attack: _MFA fatigue_ → spamming push requests until user accepts (e.g., Uber breach).
        
- **SMS OTP** → insecure (SIM swapping, interception).
    
- **Email OTP** → insecure if email account compromised.
    
- **Hardware Tokens (YubiKey, NFC, Smartcards)** → strong, offline, resistant to phishing.
    

---

## ⚙️ Conditional Access

- Contextual MFA enforcement (dynamic requirements).
    
- Examples:
    
    - **Location-based**: stricter auth when logging in from new location.
        
    - **Time-based**: extra check outside business hours.
        
    - **Behavior-based**: detect unusual activity → ask for MFA again.
        
    - **Device-based**: block/require MFA on unregistered devices.
        

---

## 🌍 Adoption & Regulation

- Rapidly adopted due to phishing/social engineering defenses.
    
- Mandated in **finance, healthcare, payments** (GDPR, HIPAA, PCI-DSS).
    
- Could have prevented breaches like Equifax (2017), Target (2013).
    

---

## ⚠️ Common MFA Vulnerabilities

### 🔑 OTP Issues

- **Weak OTP generation** → predictable codes.
    
- **OTP leakage** → app/API responses accidentally return OTP.
    
- **OTP brute force** → if no rate limiting.
    

### 🔐 Logic Flaws

- MFA not enforced across all flows → attacker bypasses by directly accessing endpoints (e.g., dashboard).
    
- Session flag (`authenticated=true`) set too early (before OTP validated).
    

### 📱 Delivery Channel Weaknesses

- **SMS OTP** → vulnerable to SIM swap or interception.
    
- **Email OTP** → weak if email compromised.
    

### 🎭 Evilginx Attacks (Phishing + Session Hijacking)

- **Man-in-the-Middle proxy** intercepts login + OTP.
    
- Attacker steals cookies/session tokens → bypass MFA.
    

### 🌀 MFA Fatigue (Push Notification Abuse)

- Attackers spam push login requests until user accepts one → compromise account.
    

---

## 🧪 Methodology: Testing MFA

1. **Find where MFA is enforced**
    
    - Only at login? Or also at sensitive actions (e.g., password change, transfers)?
        
2. **Check delivery channels**
    
    - If SMS/email: can you intercept or reuse OTPs?
        
3. **Look for OTP leakage**
    
    - Inspect API/XHR responses in DevTools.
        
    - Example: `/token` endpoint returning OTP in response.
        
4. **Bypass attempts**
    
    - Try accessing sensitive endpoints directly (e.g., `/dashboard`).
        
    - Look for weak session logic (authenticated flag before MFA).
        
5. **Brute force testing**
    
    - Test if OTP inputs allow unlimited guesses.
        
    - Check for lockouts, rate limiting, or auto-logout.
        
6. **Phishing resilience**
    
    - Evaluate if tokens can be stolen/replayed.
        
    - Evilginx or proxy-based phishing possible?
        
7. **Test backup mechanisms**
    
    - Permanent backup codes? Stored insecurely?
        

---

## 🧑‍💻 Practical Exploits (From THM Labs)

- **OTP Leakage**: API returns OTP in XHR → copy token → bypass.
    
- **Insecure Coding**: Dashboard accepts session authenticated=true even without MFA → bypass login.
    
- **Auto-Logout + Brute Force**:
    
    - Some apps reset login after failed OTPs.
        
    - Automate with script (login → submit OTP → retry until success).
        

---

## 🛡️ Mitigations

- Strong OTP generation algorithms.
    
- Never return OTPs in API responses.
    
- Enforce MFA at all sensitive actions.
    
- Use rate limiting + lockouts on OTP attempts.
    
- Session state must separate **pre-MFA** and **post-MFA**.
    
- Avoid SMS/email → prefer TOTP or hardware keys.
    
- Educate users against MFA fatigue (limit push retries).
    
- Monitor for phishing proxies (Evilginx, Modlishka).
    

---

## 📌 Key Takeaways

- MFA ≠ bulletproof → weak implementations are exploitable.
    
- OTPs are only secure if generated, delivered, and validated properly.
    
- Logic flaws (bypassing MFA checks) are as dangerous as weak delivery channels.
    
- Evilginx-style phishing bypasses MFA entirely → tokens must be protected, not just credentials.
    
- Secure MFA = strong OTPs, enforced everywhere, rate limiting, no leaks, phishing-resistant factors (hardware keys).
    