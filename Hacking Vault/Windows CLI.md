   

Windows CLI

## Basic System Information

- `ver`: Shows the operating system version.
- `systeminfo`: Provides detailed system info like OS, processor, and memory.
- `driverquery | more`: Lists installed drivers, showing one page at a time.
- `help`: Displays help for specific commands.
- `cls`: Clears the command prompt screen.

# Network Troubleshooting

## Network Configuration

- `ipconfig`: Shows basic network info like IP address and subnet mask.
- `ipconfig /all`: Displays detailed network info, including DNS servers and DHCP status.

## Network Troubleshooting

- `ping [target_name]`: Tests network connectivity by sending ICMP packets.
- `tracert [target_name]`: Traces the network route to a target, showing each hop along the way.

## More Networking Commands

- `nslookup [domain]`: Finds the IP address for a domain name.
- `netstat -abon`: Displays current network connections, listening ports, and the associated programs/process IDs.

# File and Disk Management

## Working With Directories

- `cd`: Displays the current directory or changes directories.
- `dir`: Lists the files in a directory.
- `dir /a`: Shows hidden files.
- `dir /s`: Lists files in the current directory and subdirectories.
- `mkdir [directory_name]`: Creates a new directory.
- `rmdir [directory_name]`: Removes a directory.
- `tree`: Shows a visual representation of directories and subdirectories.

## Working With Files

- `type [file]`: Displays the contents of a text file.
- `more [file]`: Shows a file's content one page at a time.
- `copy [file] [destination]`: Copies a file to a new location.
- `move [file] [destination]`: Moves a file to a new location.
- `del [file]` or `erase [file]`: Deletes a file.
- `copy *.md [destination]`: Copies all files with the `.md` extension to the destination folder.

## Task and Process Management

- `tasklist`: Displays a list of running processes.
- `tasklist /FI "imagename eq [process_name]"`: Filters the tasklist for a specific process (e.g., `notepad.exe`).
- `taskkill /PID [pid]`: Terminates a process by its process ID (PID).