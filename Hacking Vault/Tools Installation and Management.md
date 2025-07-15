   

Tools Installation and Management

# **Tools Installation and Management**

## **1. Installing, Removing, Updating, and Managing Tools**

|Action|Command|
|---|---|
|**Install**|`sudo apt install <tool-name>`|
|**Remove**|`sudo apt remove <tool-name>`|
|**Update**|`sudo apt update`|
|**Upgrade**|`sudo apt upgrade`|
|**Upgrade All**|`sudo apt full-upgrade`|
|**Search for Tools**|`apt search <tool-name>`|
|**Depackage (remove configuration files)**|`sudo apt purge <tool-name>`|
|**Clean**|`sudo apt clean`|

---

## **2. Working with Archives (Zip/Unzip)**

|Action|Command|
|---|---|
|**Install unzip**|`sudo apt install unzip`|
|**Install zip**|`sudo apt install zip`|
|**Zip a File**|`zip <archive-name>.zip <file-name>`|
|**Unzip a File**|`unzip <archive-name>.zip`|
|**Extract to Specific Folder**|`unzip <archive-name>.zip -d <folder-path>`|
|**List Zip Contents**|`unzip -l <archive-name>.zip`|
|**Remove a Zip Archive**|`rm <archive-name>.zip`|

---

## **3. PimpMyKali for New VM Setup**

**PimpMyKali** is a script that automates the setup of tools and configurations on Kali Linux, making it ideal for new VM installations.

- **GitHub Link**: [PimpMyKali](https://github.com/mitchellkrogza/pimpmykali "https://github.com/mitchellkrogza/pimpmykali")
    
- **How to Use**:  
    Run the following commands to clone the repository and execute the script:
    
    git clone https://github.com/mitchellkrogza/pimpmykali.git
    cd pimpmykali
    sudo ./pimpmykali.sh -N
    
    ```
    git clone https://github.com/mitchellkrogza/pimpmykali.git
    cd pimpmykali
    sudo ./pimpmykali.sh -N
    ```
    
    **Explanation of `-N` Option**:  
    The `-N` option performs a **fresh setup**, installing essential tools and configurations tailored for a new Kali VM environment.
    
- **Additional Options in PimpMyKali**:
    
    - `-U`: Updates an existing Kali system with the latest tools.
    - `-T`: Install all recommended tools (including penetration testing tools).
    - `-S`: Configure and tweak system settings for better performance.

---

## **4. Managing Git Repositories**

Git is essential for downloading tools and scripts. Here’s how to work with repositories:

|Action|Command|
|---|---|
|**Clone a Repository**|`git clone <repository-url>`|
|**Update Repository**|`git pull`|
|**Install Dependencies**|`sudo apt install <dependencies>` (check README for tool-specific dependencies)|
|**Remove a Repo**|Simply delete the folder with `rm -rf <repo-name>`|

---

## **5. System Maintenance and Tools Management**

It's crucial to keep your system updated and clean for security and optimal performance:

- **Check Disk Usage**:  
    `df -h`
- **Clean Up Unnecessary Files**:  
    `sudo apt autoremove` (removes unneeded dependencies)