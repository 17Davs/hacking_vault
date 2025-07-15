   

Networking commands

# **Networking Commands**

## **1. Check IP Address**

To check the IP address of your machine:

ip a

```
ip a
```

or

ifconfig

```
ifconfig
```

## **2. Wireless Connections**

To view wireless network information:

iwconfig

```
iwconfig
```

## **3. Check IP Neighbours (ARP Table)**

To show the IP-to-MAC address mapping (equivalent to `arp -a`):

ip n

```
ip n
```

or

arp -a

```
arp -a
```

## **4. Routing Table**

To view the routing table of your network (equivalent to `route`):

ip r

```
ip r
```

or

route -n

```
route -n
```

## **5. Ping a Target**

To check connectivity to a target IP or domain:

ping <target-ip-or-domain>

```
ping <target-ip-or-domain>
```

Example:

ping 8.8.8.8

```
ping 8.8.8.8
```

## **6. Traceroute**

To trace the route packets take to a destination:

traceroute <target-ip-or-domain>

```
traceroute <target-ip-or-domain>
```

Example:

traceroute google.com

```
traceroute google.com
```

## **7. Network Configuration**

To view network interfaces and their configuration:

nmcli device show

```
nmcli device show
```

## **8. DNS Lookup**

To query DNS and get details about a domain:

nslookup <domain-name>

```
nslookup <domain-name>
```

Example:

nslookup google.com

```
nslookup google.com
```

## **9. Netstat**

To view open ports and network connections:

netstat -tuln

```
netstat -tuln
```

## **10. Netcat (nc)**

To open a listener on a port:

nc -lvp <port-number>

```
nc -lvp <port-number>
```

Example:

nc -lvp 4444

```
nc -lvp 4444
```

To connect to a remote server:

nc <target-ip> <port-number>

```
nc <target-ip> <port-number>
```

## **11. Nmap**

To scan open ports on a target:

nmap <target-ip>

```
nmap <target-ip>
```

Example:

nmap 192.168.1.1

```
nmap 192.168.1.1
```

## **12. Curl**

To make HTTP requests and test web servers:

curl <target-url>

```
curl <target-url>
```

Example:

curl http://example.com

```
curl http://example.com
```