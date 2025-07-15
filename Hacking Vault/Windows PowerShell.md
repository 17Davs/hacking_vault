   

Windows PowerShell

## **PowerShell Fundamentals**

### **Object-Oriented Shell**

PowerShell is a task-based command-line shell and scripting language built on the .NET framework. Unlike traditional shells that handle only text, PowerShell deals with **objects**, allowing for more precise and powerful manipulation of system data.

---

### **Cmdlets: The Building Blocks**

PowerShell commands are known as **cmdlets** (pronounced _command-lets_). Each follows a consistent `Verb-Noun` naming convention, which improves readability and usability.

- **Verb**: The action being performed
    
- **Noun**: The target object
    

Examples:

- `Get-Content`: Retrieves the contents of a file.
    
- `Set-Location`: Changes the current working directory.
    

---

### **Essential Cmdlets**

#### **Discovering Cmdlets**

Use `Get-Command` to list all available commands:

Get-Command

```
Get-Command
```

You can filter by command type:

Get-Command -CommandType Function

```
Get-Command -CommandType Function
```

#### **Getting Help**

To understand a cmdlet in detail:

Get-Help <Cmdlet-Name>

```
Get-Help <Cmdlet-Name>
```

To see usage examples:

Get-Help <Cmdlet-Name> -Examples

```
Get-Help <Cmdlet-Name> -Examples
```

#### **Aliases**

PowerShell supports aliases for commonly used cmdlets:

Get-Alias

```
Get-Alias
```

Examples:

- `dir` → `Get-ChildItem`
    
- `cd` → `Set-Location`
    

---

### **Extending PowerShell**

PowerShell can be extended with additional modules from online repositories like the PowerShell Gallery.

- **Search for a module:**

Find-Module -Name "*pattern*"

```
Find-Module -Name "*pattern*"
```

- **Install a module:**

Install-Module -Name ModuleName

```
Install-Module -Name ModuleName
```

This makes new cmdlets available for use.

---

### **File System Navigation & File Operations**

|Cmdlet|Description|
|---|---|
|`Get-ChildItem -Path`|Lists files/directories in a path|
|`Set-Location -Path`|Changes current directory|
|`New-Item -Path -ItemType`|Creates new file/folder|
|`Copy-Item -Path -Destination`|Copies files|
|`Move-Item`|Moves files|
|`Get-Content`|Reads file content|

---

### **Filtering, Piping & Sorting**

PowerShell passes **objects** through the pipeline, not just text. This enhances filtering and transformation capabilities.

Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"

```
Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"
```

#### **Comparison Operators**

|Operator|Meaning|
|---|---|
|`-eq`|Equal|
|`-ne`|Not Equal|
|`-gt`|Greater Than|
|`-ge`|Greater or Equal|
|`-lt`|Less Than|
|`-le`|Less or Equal|
|`-like`|Pattern Matching (wildcards supported)|

Examples:

Get-ChildItem | Where-Object -Property "Name" -like "ship*"
Get-ChildItem | Where-Object Length -gt 100
Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1
Select-String -Path ".\captain-hat.txt" -Pattern "hat"

```
Get-ChildItem | Where-Object -Property "Name" -like "ship*"
Get-ChildItem | Where-Object Length -gt 100
Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1
Select-String -Path ".\captain-hat.txt" -Pattern "hat"
```

---

### **System & Network Information**

|Cmdlet|Purpose|
|---|---|
|`Get-ComputerInfo`|More detailed than `systeminfo`|
|`Get-LocalUser`|Lists local user accounts|
|`Get-NetIPConfiguration`|Shows IP, DNS, Gateway info|
|`Get-NetIPAddress`|Displays all IP addresses (active/inactive)|

---

### **Real-Time System Analysis**

|Cmdlet|Description|
|---|---|
|`Get-Process`|Lists running processes with CPU/RAM usage|
|`Get-Service`|Displays status of services|
|`Get-NetTCPConnection`|Shows active TCP connections|
|`Get-FileHash`|Generates hashes for file integrity checks|

Example:

Get-Service | Where-Object -Property "DisplayName" -like "*merry life*"

```
Get-Service | Where-Object -Property "DisplayName" -like "*merry life*"
```

---

### **Scripting & Remote Execution**

PowerShell scripting is powerful in both system administration and offensive security.

#### **Remote Execution: `Invoke-Command`**

Runs scripts or commands on local or remote systems.

Examples:

- Run a local script on a remote machine:

Invoke-Command -FilePath "C:\scripts\test.ps1" -ComputerName Server01

```
Invoke-Command -FilePath "C:\scripts\test.ps1" -ComputerName Server01
```

- Execute a command block with credentials:

Invoke-Command -ComputerName Server01 -Credential Domain01\User01 -ScriptBlock { Get-Culture }

```
Invoke-Command -ComputerName Server01 -Credential Domain01\User01 -ScriptBlock { Get-Culture }
```

- Execute `Get-Service` on a remote machine:

Invoke-Command -ComputerName RoyalFortune -ScriptBlock { Get-Service }

```
Invoke-Command -ComputerName RoyalFortune -ScriptBlock { Get-Service }
```

---