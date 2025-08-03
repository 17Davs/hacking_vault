 
Burp Suite: Using Macros to Grab Session & CSRF Tokens
## 🧠 Purpose
Some login forms use **dynamic tokens** that must be refreshed per request:
- `session` (Set-Cookie)
- `loginToken` (hidden CSRF field)

➡️ These values must be updated **before every login attempt**.

Use **Burp Macros** + **Session Handling Rules** to automate this in **Intruder** attacks.

---
## 🔄 Key Takeaways
- **CSRF tokens** and **session cookies** are often dynamic.
- Found in:
  - `Set-Cookie` headers (`session=...`)
  - Hidden fields (`<input name="loginToken" value="...">`)
- You cannot use Intruder alone if the tokens change – must use **Macros**.
- Macros send a GET request to grab fresh tokens.
- Session Handling Rules inject those values into the brute-force request.

---
## 🔧 Step-by-Step Setup

### 1. Capture and Prepare the Attack
- Go to `/admin/login/` and attempt login.
- Intercept the **POST** request, send to **Intruder**.
- In **Intruder → Positions**:
  - Clear all markers.
  - Set positions on `username` and `password` only.
- Set **Attack Type**: `Pitchfork`
- In **Payloads tab**, load your wordlists.

---
### 2. Create a Macro
1. Go to **Settings → Sessions → Macros → Add**
2. If missing, visit `/admin/login/` in browser to generate a GET request.
3. Select the GET request and click **OK**.
4. Name the macro (e.g., `Get CSRF + Session`) and save.

---
### 3. Add a Session Handling Rule
1. **Settings → Sessions → Session Handling Rules → Add**
2. In **Details tab**:
   - Description: `Update CSRF and session via macro`
   - Click **Add Action → Run a Macro**
   - Choose the macro created earlier
   - Set options:
     - ☑️ `Update only the following parameters` → Add `loginToken`
     - ☑️ `Update only the following cookies` → Add `session`
3. In **Scope tab**:
   - **Tool Scope**: Only check `Intruder`
   - **URL Scope**: Add `http://10.10.122.101/` or use suite scope

---
### 4. Run the Attack
- Go back to **Intruder**.
- Start the attack.
- Look for **302** responses (expected).
  - If getting **403**, macro is likely misconfigured.
- Sort responses by **Length** to find anomalies (possible successful login).

---
## ✅ Troubleshooting

- **403 errors** → Macro isn't injecting tokens.
  - Check if GET request in macro is valid and recent.
  - Confirm parameter/cookie names are exactly `loginToken` and `session`.
- **Logger++ or HTTP history** can help verify token updates.

---
## 💡 Tips
- Use **Pitchfork** to keep `username` and `password` aligned.
- Response **length** is a great indicator for successful login.
- You can **test the macro manually** before running a full attack.

