   

Custom rules

## 🔧 Custom Rules in John the Ripper

### 🧠 What Are Custom Rules?

Custom rules allow you to define **how John the Ripper transforms (mangles)** words in a wordlist to match **common or known password patterns**.

Useful when:

- You know likely password structures (e.g., `Summer2024!`).
    
- You want to make smarter guesses than basic brute-force or raw dictionary attacks.
    

---

### 🧪 Why Use Them?

Most users **follow predictable patterns** to meet complexity rules, like:

- One capital letter
    
- One digit
    
- One special character  
    ✅ Example:
    

Password1!

```
Password1!
```

Attackers can exploit **where** these changes usually occur:

- Capital at the **start**
    
- Numbers/symbols at the **end**
    

---

### 🧱 Custom Rule Components

**Location:**

- Usually defined in `john.conf`
    
    - TryHackMe: `/opt/john/john.conf`
        
    - Common: `/etc/john/john.conf`
        

---

### 🏗️ Rule Syntax Basics

[List.Rules:<RuleName>]
<commands>

```
[List.Rules:<RuleName>]
<commands>
```

**Commands Overview:**

|Command|Meaning|
|---|---|
|`c`|Capitalize the first letter|
|`C`|Capitalize all letters|
|`Az"X"`|Append characters X|
|`A0"X"`|Prepend characters X|
|`l`|Lowercase all|
|`d`|Duplicate the word|
|`r`|Reverse the word|

**Character Set Examples:**

- `[0-9]` → All digits
    
- `[A-Z]` → Uppercase
    
- `[a-z]` → Lowercase
    
- `[!@#$]` → Custom symbols
    
- `[a]` → Just the letter `a`
    

---

### 🔍 Practical Example

We want to match passwords like:

polopassword → Polopassword1!

```
polopassword → Polopassword1!
```

**Step 1: Add this to `john.conf`:**

[List.Rules:PoloPassword]
cAz"[0-9][!@#]"

```
[List.Rules:PoloPassword]
cAz"[0-9][!@#]"
```

**Explanation:**

- `c` → Capitalize first letter → `Polopassword`
    
- `Az"[0-9][!@#]"` → Append one digit and one symbol → `Polopassword1!`
    

**Step 2: Use it in a crack:**

john --wordlist=/path/wordlist.txt --rules=PoloPassword hashes.txt

```
john --wordlist=/path/wordlist.txt --rules=PoloPassword hashes.txt
```

---

### 🎯 More Rule Examples

**Capitalize + add 123**

[List.Rules:Cap123]
cAz"123"

```
[List.Rules:Cap123]
cAz"123"
```

Turns `summer` → `Summer123`

---

**Prepend "2024" + symbol**

[List.Rules:YearSym]
A0"2024"Az"[!$]"

```
[List.Rules:YearSym]
A0"2024"Az"[!$]"
```

Turns `password` → `2024password!`

---

**Reverse + append digit**

[List.Rules:RevNum]
rAz"[0-9]"

```
[List.Rules:RevNum]
rAz"[0-9]"
```

Turns `admin` → `nimda4`

---

### 🧰 Built-in Rule Sets

Jumbo John has many predefined rules in `john.conf`.  
You can explore or reuse them (look around line ~678):

john --list=rules

```
john --list=rules
```

Try using:

--rules=Single
--rules=Wordlist
--rules=All

```
--rules=Single
--rules=Wordlist
--rules=All
```

---

### 💡 Tips

- Use custom rules when cracking known targets (e.g., internal corp passwords).
    
- Stack commands together to make powerful combos.
    
- If a rule isn’t working, check for **syntax errors** or test it manually.
    
- Speak the pattern out loud: “capitalize, then append a number and symbol.”
    

[https://www.openwall.com/john/doc/RULES.shtml](https://www.openwall.com/john/doc/RULES.shtml "https://www.openwall.com/john/doc/RULES.shtml")