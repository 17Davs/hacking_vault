   

PASSWORDS OSINT

# **Password OSINT (Open Source Intelligence)**

## **1. What is Password OSINT?**

Password OSINT involves gathering publicly available information to discover or guess passwords. This is a common technique in ethical hacking, where attackers or penetration testers use this information to gain unauthorized access.

---

## **2. Key Sources for Password OSINT**

### **Public Databases**

- **Have I Been Pwned** ([haveibeenpwned.com](https://haveibeenpwned.com/ "https://haveibeenpwned.com/")): A site where you can check if an email or password has been exposed in a data breach.

### **Social Media Platforms**

- **Facebook**, **Twitter**, **LinkedIn**: These platforms can provide clues about a person’s password, such as pet names, birthdays, favorite sports teams, or common password patterns.

### **Public Leaked Password Databases**

- **RockYou Database**: A leaked database from a 2009 breach, containing millions of passwords. It’s still commonly used by attackers for password cracking.

### **Company Leaks**

- **Pastebin**: An anonymous text-sharing platform where users may leak information, including passwords.
- **GitHub**: Sometimes, developers mistakenly upload sensitive credentials (including passwords) in their repositories.

### **Breach Credentials**

- **Breach-Parse GitHub**: A collection of over **44GB** of leaked credentials and breach data. This can be used to identify exposed passwords for analysis.
    - [Breach-Parse on GitHub](https://github.com/hmaverickadams/breach-parse/tree/master "https://github.com/hmaverickadams/breach-parse/tree/master")
- **Dehashed**: A search engine for finding leaked databases and exposed credentials.
    - [Dehashed](https://www.dehashed.com/ "https://www.dehashed.com/")
- **Hashes.org**: A website offering a hash lookup service, helping to identify exposed or cracked passwords.
    - [Hashes.org](https://hashes.org/ "https://hashes.org/")

---

## **3. Tools for Password OSINT**

|Tool|Description|Link|
|---|---|---|
|**Have I Been Pwned**|Check if an email or password is exposed in known data breaches.|[haveibeenpwned.com](https://haveibeenpwned.com/ "https://haveibeenpwned.com/")|
|**LeakBase**|A database of breached login information.|[LeakBase](https://www.leakbase.pw/ "https://www.leakbase.pw/")|
|**Dehashed**|A search engine for leaked databases.|[Dehashed](https://www.dehashed.com/ "https://www.dehashed.com/")|
|**Pwned Passwords**|A service by Have I Been Pwned to check if a password is compromised.|[Pwned Passwords](https://haveibeenpwned.com/Passwords "https://haveibeenpwned.com/Passwords")|
|**Hashes.org**|A site for looking up cracked or exposed password hashes.|[Hashes.org](https://hashes.org/ "https://hashes.org/")|
|**Breach-Parse**|A collection of over 44GB of breached credentials for analysis.|[Breach-Parse on GitHub](https://github.com/hmaverickadams/breach-parse/tree/master "https://github.com/hmaverickadams/breach-parse/tree/master")|

---

## **4. Techniques for Password Discovery**

### **1. Brute-Force Using Leaked Password Lists**

- Use common passwords from breached datasets (e.g., RockYou) or custom wordlists to attempt brute-forcing accounts.

Example of a brute-force attack using **Hydra**:

hydra -l user@example.com -P /path/to/wordlist.txt ssh://target-ip

```
hydra -l user@example.com -P /path/to/wordlist.txt ssh://target-ip
```

### **2. Social Engineering**

- Gather information about a target through social media, email, and public profiles. Use this info to guess passwords (e.g., pet names, birthdates).

Example:

hydra -l target_user -p "target_petname123" ssh://target-ip

```
hydra -l target_user -p "target_petname123" ssh://target-ip
```

### **3. Password Pattern Recognition**

- Recognize common password patterns such as `Password123`, `admin123`, or variations of a company name or year.

---

## **5. Password Cracking Using OSINT Data**

- After gathering a list of likely passwords (through leaks or social media), use tools like **John the Ripper** or **Hashcat** to attempt cracking hashes.

Example with **John the Ripper**:

john --wordlist=/path/to/wordlist.txt --format=raw-md5 password_hashes.txt

```
john --wordlist=/path/to/wordlist.txt --format=raw-md5 password_hashes.txt
```