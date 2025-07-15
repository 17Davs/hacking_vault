   

SMB Enumeration

# **SMB Enumeration in Ethical Hacking**

## **1. What is SMB?**

SMB (Server Message Block) is a protocol used for sharing files, printers, and other network resources on Windows-based systems. It operates over TCP ports **445** and **139**.

### **Common SMB Versions**

- **SMBv1** (Deprecated, vulnerable to EternalBlue)
- **SMBv2 & SMBv3** (More secure, but can still have misconfigurations)

---

## **2. Identifying SMB Services**

### **Port Scanning**

Use **Nmap** to check if SMB is running on a target system:

nmap -p 139,445 -sC -sV <target-ip>

```
nmap -p 139,445 -sC -sV <target-ip>
```

or

nmap --script smb* -p 445 <target-ip>

```
nmap --script smb* -p 445 <target-ip>
```

### **Checking SMB Version**

nmap --script smb-os-discovery -p 445 <target-ip>

```
nmap --script smb-os-discovery -p 445 <target-ip>
```

or

smbclient -L //<target-ip> -N

```
smbclient -L //<target-ip> -N
```

---

## **3. SMB Enumeration Techniques**

### **Enumerating SMB Shares**

#### **Using smbclient**

smbclient -L //<target-ip> -N

```
smbclient -L //<target-ip> -N
```

(Use `-N` to avoid password prompt if authentication isn’t needed.)

#### **Using enum4linux**

enum4linux -a <target-ip>

```
enum4linux -a <target-ip>
```

(`-a` runs all checks, including users, shares, and OS info.)

#### **Using CrackMapExec**

crackmapexec smb <target-ip> --shares

```
crackmapexec smb <target-ip> --shares
```

This tool also checks for weak credentials.

---

### **4. Enumerating Users**

#### **Using enum4linux**

enum4linux -U <target-ip>

```
enum4linux -U <target-ip>
```

#### **Using Nmap**

nmap --script smb-enum-users -p 445 <target-ip>

```
nmap --script smb-enum-users -p 445 <target-ip>
```

#### **Using rpcclient**

If guest access is enabled:

rpcclient -U "" <target-ip>

```
rpcclient -U "" <target-ip>
```

Then try:

enumdomusers

```
enumdomusers
```

---

### **5. Anonymous Authentication & Guest Access**

Try logging in as a guest:

smbclient //target-ip/share -U anonymous

```
smbclient //target-ip/share -U anonymous
```

or

smbclient //target-ip/share -N

```
smbclient //target-ip/share -N
```

If login is successful, you may have access to sensitive files.

---

## **6. Exploiting SMB Misconfigurations**

### **Null Sessions (No Authentication Required)**

If **null sessions** are allowed, you can extract information like users, shares, and policies:

smbclient -L //<target-ip> -N

```
smbclient -L //<target-ip> -N
```

If **null sessions** are restricted but guest access is enabled, try:

smbclient //target-ip/share -U guest

```
smbclient //target-ip/share -U guest
```

---

### **7. Checking for SMB Vulnerabilities**

#### **Using Nmap**

nmap --script smb-vuln* -p 445 <target-ip>

```
nmap --script smb-vuln* -p 445 <target-ip>
```

This scans for vulnerabilities like:

- **EternalBlue (MS17-010)**
- **SMB Signing Disabled**
- **SMBv1 Exploits**

#### **Using Metasploit**

Check for **MS17-010 (EternalBlue)** vulnerability:

msfconsole
use auxiliary/scanner/smb/smb_ms17_010
set RHOSTS <target-ip>
run

```
msfconsole
use auxiliary/scanner/smb/smb_ms17_010
set RHOSTS <target-ip>
run
```

---

## **8. Brute-Forcing SMB Credentials**

If authentication is required, use **Hydra** or **CrackMapExec** to brute-force login:

#### **Hydra**

hydra -L users.txt -P passwords.txt smb://<target-ip>

```
hydra -L users.txt -P passwords.txt smb://<target-ip>
```

#### **CrackMapExec**

crackmapexec smb <target-ip> -u users.txt -p passwords.txt

```
crackmapexec smb <target-ip> -u users.txt -p passwords.txt
```

---

## **9. Mitigation and Hardening SMB**

- Disable **SMBv1** (`sc.exe config lanmanworkstation depend= bowser/mrxsmb20/nsi`)
- Enable **SMB Signing**
- Restrict **Anonymous Access**
- Use **Strong Passwords**
- Apply **Security Patches** (e.g., MS17-010)

---

## **10. Tools for SMB Enumeration**

|Tool|Description|
|---|---|
|**Nmap**|Port scanning, script-based enumeration|
|**smbclient**|Connect to SMB shares manually|
|**enum4linux**|Automated SMB enumeration for Linux|
|**CrackMapExec**|Check SMB shares, users, and brute-force authentication|
|**rpcclient**|Interact with Windows RPC services|
|**Metasploit**|Exploit SMB vulnerabilities|

---