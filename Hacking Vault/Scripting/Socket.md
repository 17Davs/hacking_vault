   

Socket

python sockets notes

import socket

HOST = '127.0.0.1'
PORT = 7777

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)   
#af_inet is ipv4 and sock_strea, is a port

s.connect((HOST,PORT))

```
import socket

HOST = '127.0.0.1'
PORT = 7777

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)   
#af_inet is ipv4 and sock_strea, is a port

s.connect((HOST,PORT))
```

scanner.py

#!/bin/python3

import sys
import socket
from datetime import datetime

#define target
if len(sys.argv) == 2:
       target = socket.hethostbyname(sys.argv[1]) # translate hostname to ipv4
else: 
       print("Syntax: python3 scanner.py <ip>")  
 
#banner
print( "-" * 50)
print("Scanning target:  " + target)
print("Time started: " + str(datetime.now()))
print( "-" * 50)

try: 
    for port in range(50,85):
        s= socket.socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        socket.setdefaulttimeout(1)
        result = s.connect_ex((target,port))
        if result == 0:
            print(f"Port {port} is open")
        s.close()	 
except KeyboardInterrupt:
    print("\nExisting program...")
    sys.exit()
except socket.gaierror:
    print("Hostname could not be resolved.")
    sys.exit()
except socket.error:
    print("Could not connect to server.")
    sys.exit()		

```
#!/bin/python3

import sys
import socket
from datetime import datetime

#define target
if len(sys.argv) == 2:
       target = socket.hethostbyname(sys.argv[1]) # translate hostname to ipv4
else: 
       print("Syntax: python3 scanner.py <ip>")  
 
#banner
print( "-" * 50)
print("Scanning target:  " + target)
print("Time started: " + str(datetime.now()))
print( "-" * 50)

try: 
    for port in range(50,85):
        s= socket.socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        socket.setdefaulttimeout(1)
        result = s.connect_ex((target,port))
        if result == 0:
            print(f"Port {port} is open")
        s.close()	 
except KeyboardInterrupt:
    print("\nExisting program...")
    sys.exit()
except socket.gaierror:
    print("Hostname could not be resolved.")
    sys.exit()
except socket.error:
    print("Could not connect to server.")
    sys.exit()		
```