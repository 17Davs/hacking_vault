   

ssh2john

🔑 Cracking SSH Private Key Passwords with John the Ripper

### 📄 What is an `id_rsa` File?

- It’s a **private key file** used for **SSH key-based authentication**.
    
- Often protected with a passphrase for security.
    
- We can crack this passphrase using `John`.
    

---

### 🛠️ Tool: `ssh2john`

This tool **converts the SSH private key** (`id_rsa`) into a hash format that John can process.

#### 🧪 Syntax:

ssh2john [id_rsa file] > [output file]

```
ssh2john [id_rsa file] > [output file]
```

- `ssh2john`: Tool (or Python script) that reads the private key and outputs a crackable hash
    
- `id_rsa`: Path to the private key
    
- `>`: Redirects output
    
- `output file`: File to store the generated hash
    

---

### 🐍 Note: Script Path (if not in $PATH)

Use the full path if needed:

- **On TryHackMe AttackBox**:
    
    python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
    
    ```
    python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
    ```
    
- **On Kali Linux**:
    
    python /usr/share/john/ssh2john.py id_rsa > id_rsa_hash.txt
    
    ```
    python /usr/share/john/ssh2john.py id_rsa > id_rsa_hash.txt
    ```
    

---

### 🔓 Cracking the SSH Key Password

Now run `john` with your preferred wordlist (e.g., `rockyou.txt`):

john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt

```
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```

Wait for John to brute-force the passphrase.

---

### 🔍 View Cracked Password

After John completes, view the result with:

john --show id_rsa_hash.txt

```
john --show id_rsa_hash.txt
```

Example output:

id_rsa: mysupersecurepass

```
id_rsa: mysupersecurepass
```

---

### 💻 Using the Cracked Key to SSH

Once you have the passphrase, use the key to SSH into a remote machine:

ssh -i id_rsa user@ip_address

```
ssh -i id_rsa user@ip_address
```

You'll be prompted for the **cracked passphrase** — enter it to authenticate.

---

### 🧪 Practical Challenge

Crack the password of a private key located at:

~/John-the-Ripper-The-Basics/Task11/id_rsa

```
~/John-the-Ripper-The-Basics/Task11/id_rsa
```

#### Full Steps Recap:

1. **Convert key to hash**:
    
    python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
    
    ```
    python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
    ```
    
2. **Crack the hash**:
    
    john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
    
    ```
    john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
    ```
    
3. **View password**:
    
    john --show id_rsa_hash.txt
    
    ```
    john --show id_rsa_hash.txt
    ```
    
4. **SSH into target (after chmod)**:
    
    chmod 600 id_rsa
    ssh -i id_rsa user@target_ip
    
    ```
    chmod 600 id_rsa
    ssh -i id_rsa user@target_ip
    ```
    

---