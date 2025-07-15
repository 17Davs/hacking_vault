   

Users and Privileges

# **Users and Privileges in Kali Linux**

## **1. Viewing Current User**

To view the current logged-in user:

whoami

```
whoami
```

## **2. Viewing All Users**

To view all users on the system:

cat /etc/passwd

```
cat /etc/passwd
```

The `/etc/passwd` file contains information about users, including their associated shell and home directory path.

## **3. Viewing Password Hashes**

To view user password hashes:

cat /etc/shadow

```
cat /etc/shadow
```

The `/etc/shadow` file stores password hashes and other user authentication details.

## **4. Viewing Sudoers File**

To view the sudoers file, which lists users allowed to execute sudo commands and what commands they can run:

sudo visudo

```
sudo visudo
```

## **5. Listing Files and Directories with Permissions**

To list files and directories along with their permissions:

ls -la

```
ls -la
```

This command shows file permissions, owners, and groups.

## **6. Changing File Permissions with `chmod`**

To change the permissions of a file or directory:

chmod 700 <file|directory>

```
chmod 700 <file|directory>
```

This gives the owner full permissions (read, write, execute), but no permissions to others.

## **7. Adding a New User**

To add a new user:

sudo useradd <username>

```
sudo useradd <username>
```

To add a user with specific home directory and shell:

sudo useradd -m -s /bin/bash <username>

```
sudo useradd -m -s /bin/bash <username>
```

## **8. Changing User Password**

To change the password for a user:

sudo passwd <username>

```
sudo passwd <username>
```

## **9. User Privileges**

### **Viewing User Groups**

To view the groups a user belongs to:

groups <username>

```
groups <username>
```

### **Adding User to Group**

To add a user to a group:

sudo usermod -aG <groupname> <username>

```
sudo usermod -aG <groupname> <username>
```

### **Removing User from Group**

To remove a user from a group:

sudo gpasswd -d <username> <groupname>

```
sudo gpasswd -d <username> <groupname>
```

## **10. Sudo Privileges**

### **Checking Sudo Privileges**

To check if a user has `sudo` privileges:

sudo -l

```
sudo -l
```

### **Granting Sudo Privileges**

To grant `sudo` privileges to a user, add the user to the `sudo` group:

sudo usermod -aG sudo <username>

```
sudo usermod -aG sudo <username>
```

## **11. Changing User Privileges (Root Access)**

To switch to the **root** user:

sudo su

```
sudo su
```

Or use:

sudo -i

```
sudo -i
```

## **12. Removing a User**

To remove a user:

sudo userdel <username>

```
sudo userdel <username>
```

To remove a user and their home directory:

sudo userdel -r <username>

```
sudo userdel -r <username>
```

---