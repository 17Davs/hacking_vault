   

zip2john

## 🔐 Cracking ZIP Passwords with Zip2John

### 📦 What is `zip2john`?

`zip2john` extracts password hash data from a **ZIP archive**, converting it into a format that **John the Ripper** can process and crack.

It's similar in concept to `unshadow`, but specifically for `.zip` files.

---

### ⚙️ Basic Usage

zip2john [options] [zipfile] > [outputfile]

```
zip2john [options] [zipfile] > [outputfile]
```

**Parameters:**

- `[zipfile]`: Path to the `.zip` archive.
    
- `[outputfile]`: File to save the extracted hash.
    
- `>`: Redirects output to a file.
    

🧪 **Example:**

zip2john secret.zip > zip_hash.txt

```
zip2john secret.zip > zip_hash.txt
```

This extracts the hash and saves it to `zip_hash.txt`.

---

### 🔓 Cracking the Password

Once the hash is extracted, use **John** to crack it:

john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt

```
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

John will use the **RockYou** wordlist to attempt cracking the hash from the `.zip` file.

---

### 📁 Practical Challenge

💼 **Try it yourself!**  
A test file is provided at:

~/John-the-Ripper-The-Basics/Task09/

```
~/John-the-Ripper-The-Basics/Task09/
```

1. Extract the hash:

zip2john secure.zip > zip_hash.txt

```
zip2john secure.zip > zip_hash.txt
```

2. Run John to crack:

john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt

```
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

3. To see the cracked password:

john --show zip_hash.txt

```
john --show zip_hash.txt
```

4. Unzip the file

`unzip -P password secure.zip`

---

### 📝 Notes

- `zip2john` works with encrypted ZIP files that use a password for extraction.
    
- If the file isn't encrypted, there won’t be any hash to extract.
    
- For ZIP files with multiple entries, hashes may be extracted for each file inside.
    

---