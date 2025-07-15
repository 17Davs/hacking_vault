# 🌐 Shell Listeners

## 📋 Purpose

Shell listeners are tools used on an attacker’s machine to handle incoming connections from reverse shells, allowing interaction with the compromised target’s shell.

## 🔍 Tools for Shell Listeners

### Rlwrap

- **Purpose**: Enhances shell interaction with editing (arrow keys) and command history using the GNU readline library.
- **Example**:
    
    ```bash
    rlwrap nc -lvnp 443  # Wraps Netcat for better interaction
    ```
    

### Ncat

- **Purpose**: Improved Netcat version from the Nmap project, with features like SSL encryption.
- **Example (Basic Listener)**:
    
    ```bash
    ncat -lvnp 4444  # Listens for reverse shells
    ```
    
- **Example (SSL Listener)**:
    
    ```bash
    ncat --ssl -lvnp 4444  # Listens with SSL encryption
    ```
    

### Socat

- **Purpose**: Flexible tool for creating socket connections between two data sources (e.g., hosts).
- **Example**:
    
    ```bash
    socat -d -d TCP-LISTEN:443 STDOUT  # Listens on port 443 with verbose output
    ```
    
    - `-d -d`: Increases verbosity.
    - `TCP-LISTEN:443`: Creates TCP listener on port 443.
    - `STDOUT`: Directs incoming data to the terminal.

## ✅ Quick Notes

- **Socat**: A flexible networking tool that creates socket connections between two data sources.
- **Rlwrap**: A command-line utility providing readline-style editing and command history for shell listeners.
- **Ncat**: The improved Netcat version from the Nmap project, supporting SSL for encrypted shells.
- **Use Case**: Essential for receiving and interacting with reverse shells from compromised targets.