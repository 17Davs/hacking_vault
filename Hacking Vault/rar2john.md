   

rar2john

## 🗃️ Cracking Password-Protected RAR Archives with John the Ripper

### 📦 What is a RAR File?

RAR is a popular archive format (used by **WinRAR**) for compressing and encrypting files. Like ZIP files, RAR archives can be password-protected — and **John the Ripper** can crack them.

---

### 🛠️ Tool: `rar2john`

Used to extract the **password hash** from a RAR archive so John can attempt to crack it.

#### 🔧 Basic Syntax:

rar2john [rarfile] > [outputfile]

```
rar2john [rarfile] > [outputfile]
```

- `rarfile`: Path to the `.rar` archive
    
- `outputfile`: File to save the hash
    
- `>`: Redirects the output to the file
    

#### 🧪 Example:

rar2john secure.rar > rar_hash.txt

```
rar2john secure.rar > rar_hash.txt
```

---

### 🔓 Cracking the Password

Use John with a wordlist to attempt cracking:

john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt

```
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
```

This tells John to use the `rockyou.txt` wordlist against the extracted hash.

---

### 🔍 Viewing the Cracked Password

After cracking is complete, view the result:

john --show rar_hash.txt

```
john --show rar_hash.txt
```

Example output:

secure.rar:hunter2

```
secure.rar:hunter2
```

---

### 📁 Extracting the RAR File

Once the password is cracked, use it to extract the archive with the `unrar` tool:

unrar x -p[password] secure.rar

```
unrar x -p[password] secure.rar
```

🧪 **Example** (if the password is `hunter2`):

unrar x -phunter2 secure.rar

```
unrar x -phunter2 secure.rar
```

- `x`: Extracts with full paths
    
- `-p[password]`: Supplies the cracked password
    

If `unrar` is not installed, you can install it with:

sudo apt install unrar

```
sudo apt install unrar
```

---

### 🧪 Practical Challenge

📁 Try it out with the sample file in:

~/John-the-Ripper-The-Basics/Task10/

```
~/John-the-Ripper-The-Basics/Task10/
```

**Steps Recap:**

1. Extract hash:
    
    rar2john secure.rar > rar_hash.txt
    
    ```
    rar2john secure.rar > rar_hash.txt
    ```
    
2. Crack it:
    
    john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
    
    ```
    john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
    ```
    
3. View password:
    
    john --show rar_hash.txt
    
    ```
    john --show rar_hash.txt
    ```
    
4. Extract files:
    
    unrar x -p[crackedpassword] secure.rar
    
    ```
    unrar x -p[crackedpassword] secure.rar
    ```
    

---