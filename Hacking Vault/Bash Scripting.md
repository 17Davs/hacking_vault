   

Bash Scripting

# **Bash Scripting for Ethical Hackers and General Purpose**

## **1. What is Bash Scripting?**

Bash scripting is a way to automate tasks in Unix-like systems using the Bash shell. It's commonly used in penetration testing, system administration, and general automation.

---

## **2. Why Use Bash Scripting in Ethical Hacking?**

- **Automation**: Automate repetitive tasks, such as scanning, vulnerability assessments, or information gathering.
- **Efficiency**: Save time by automating the execution of multiple commands.
- **Custom Tools**: Create your own tools or scripts to streamline penetration testing processes.

---

## **3. Basic Bash Scripting Syntax**

### **Creating a Script**

1. Open a text editor and create a new file, for example:
    
    nano script.sh
    
    ```
    nano script.sh
    ```
    
2. Add the shebang to specify which shell to use:
    
    #!/bin/bash
    
    ```
    #!/bin/bash
    ```
    
3. Write your script content:
    
    echo "Hello, world!"
    
    ```
    echo "Hello, world!"
    ```
    
4. Save and close the editor.
    

### **Making the Script Executable**

chmod +x script.sh

```
chmod +x script.sh
```

### **Running the Script**

./script.sh

```
./script.sh
```

---

## **4. Variables and Input**

### **Setting Variables**

my_variable="value"
echo $my_variable

```
my_variable="value"
echo $my_variable
```

### **Reading User Input**

echo "Enter your name: "
read name
echo "Hello, $name!"

```
echo "Enter your name: "
read name
echo "Hello, $name!"
```

---

## **5. Conditional Statements**

### **If-Else Example**

if [ $my_variable == "value" ]; then
    echo "Variable is correct!"
else
    echo "Variable is incorrect."
fi

```
if [ $my_variable == "value" ]; then
    echo "Variable is correct!"
else
    echo "Variable is incorrect."
fi
```

### **Case Example**

case $option in
    1) echo "Option 1 selected";;
    2) echo "Option 2 selected";;
    *) echo "Invalid option";;
esac

```
case $option in
    1) echo "Option 1 selected";;
    2) echo "Option 2 selected";;
    *) echo "Invalid option";;
esac
```

---

## **6. Loops**

### **For Loop Example**

for i in {1..5}; do
    echo "Iteration $i"
done

```
for i in {1..5}; do
    echo "Iteration $i"
done
```

### **While Loop Example**

count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done

```
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

---

## **7. Common Bash Commands for Hacking Tasks**

|Command|Description|
|---|---|
|`curl`|Fetch content from URLs (useful for web scraping or testing endpoints).|
|`wget`|Download files from the internet.|
|`nmap`|Network exploration and vulnerability scanning.|
|`netstat`|Show network connections.|
|`grep`|Search text in files.|
|`awk`|Pattern scanning and processing.|
|`sed`|Stream editor for text manipulation.|

---

## **8. Practical Bash Scripting for Ethical Hacking**

### **Automating Nmap Scans**

#!/bin/bash
echo "Enter target IP: "
read target_ip
nmap -sS $target_ip

```
#!/bin/bash
echo "Enter target IP: "
read target_ip
nmap -sS $target_ip
```

### **Brute-Force Script (example)**

#!/bin/bash
usernames=("admin" "user" "test")
passwords=("password1" "123456" "admin123")

for username in "${usernames[@]}"; do
    for password in "${passwords[@]}"; do
        echo "Trying $username:$password"
        sshpass -p $password ssh -o StrictHostKeyChecking=no $username@target_ip
    done
done

```
#!/bin/bash
usernames=("admin" "user" "test")
passwords=("password1" "123456" "admin123")

for username in "${usernames[@]}"; do
    for password in "${passwords[@]}"; do
        echo "Trying $username:$password"
        sshpass -p $password ssh -o StrictHostKeyChecking=no $username@target_ip
    done
done
```

---

---

#!/bin/bash

if [ "$1" == "" ]
then
    echo "Forgot de IP address"
    echo "./script 192.168.4" 
else
    for $ip in `seq 1 254`
    ping -C 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" &
    done
fi

```
#!/bin/bash

if [ "$1" == "" ]
then
    echo "Forgot de IP address"
    echo "./script 192.168.4" 
else
    for $ip in `seq 1 254`
    ping -C 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" &
    done
fi
```

`./ipsweep.sh 192.168.4 > ips.txt`

use nmap to scan exacly the online hosts from ping sweep

`for ip in $(cat ips.txt); do nmap #ip; done`