   

tcpdump

✅ Basic `tcpdump` Options

|Command|Explanation|
|---|---|
|`tcpdump -i INTERFACE`|Capture packets on a specific network interface|
|`tcpdump -w FILE`|Write captured packets to a file|
|`tcpdump -r FILE`|Read captured packets from a file|
|`tcpdump -c COUNT`|Capture a specific number of packets|
|`tcpdump -n`|Don’t resolve IP addresses|
|`tcpdump -nn`|Don’t resolve IP & protocol numbers|
|`tcpdump -v`, `-vv`, `-vvv`|Verbose output (increase verbosity)|

### 📝 Examples

tcpdump -i eth0 -c 50 -v
# Capture & display 50 packets on eth0 with verbose output

tcpdump -i wlo1 -w data.pcap
# Capture packets on wlo1 (WiFi) & write to data.pcap

tcpdump -i any -nn
# Capture on all interfaces, no DNS or protocol resolution

```
tcpdump -i eth0 -c 50 -v
# Capture & display 50 packets on eth0 with verbose output

tcpdump -i wlo1 -w data.pcap
# Capture packets on wlo1 (WiFi) & write to data.pcap

tcpdump -i any -nn
# Capture on all interfaces, no DNS or protocol resolution
```

---

## 🔍 Filtering by Host, Port & Protocol

|Command|Explanation|
|---|---|
|`tcpdump host IP/HOSTNAME`|Filter packets by IP or hostname|
|`tcpdump src host IP`|Filter packets by source IP|
|`tcpdump dst host IP`|Filter packets by destination IP|
|`tcpdump port PORT`|Filter packets by port|
|`tcpdump src port PORT`|Filter by source port|
|`tcpdump dst port PORT`|Filter by destination port|
|`tcpdump PROTOCOL`|Filter by protocol (e.g., `ip`, `ip6`, `icmp`)|

### 📝 Examples

tcpdump -i any tcp port 22
# SSH traffic on all interfaces

tcpdump -i wlo1 udp port 123
# NTP traffic on wlo1

tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
# HTTPS traffic with example.com on eth0, write to file

```
tcpdump -i any tcp port 22
# SSH traffic on all interfaces

tcpdump -i wlo1 udp port 123
# NTP traffic on wlo1

tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
# HTTPS traffic with example.com on eth0, write to file
```

---

## 🗃 Reading & Counting from Files

tcpdump -r traffic.pcap -c 5 -n
# Read first 5 packets from file, no DNS resolution

tcpdump -r traffic.pcap | grep "192.168.124.1" | wc -l
# Count packets with source IP 192.168.124.1

```
tcpdump -r traffic.pcap -c 5 -n
# Read first 5 packets from file, no DNS resolution

tcpdump -r traffic.pcap | grep "192.168.124.1" | wc -l
# Count packets with source IP 192.168.124.1
```

---

## ⚖ Filtering by Packet Length

|Filter|Explanation|
|---|---|
|`greater LENGTH`|Packets ≥ specified length|
|`less LENGTH`|Packets ≤ specified length|

---

## 🏗 Advanced: Filtering by Header Bytes

- Syntax: `proto[expr:size]`
    
    - `proto`: `arp`, `ether`, `icmp`, `ip`, `ip6`, `tcp`, `udp`
        
    - `expr`: byte offset (0 is first byte)
        
    - `size`: optional; 1 (default), 2, or 4 bytes
        

### Examples

tcpdump 'ether[0] & 1 != 0'
# Ethernet multicast addresses

tcpdump 'ip[0] & 0xf != 5'
# IP packets with options

```
tcpdump 'ether[0] & 1 != 0'
# Ethernet multicast addresses

tcpdump 'ip[0] & 0xf != 5'
# IP packets with options
```

---

## 🚩 Filtering by TCP Flags

|Flag|Explanation|
|---|---|
|`tcp-syn`|Synchronize|
|`tcp-ack`|Acknowledge|
|`tcp-fin`|Finish|
|`tcp-rst`|Reset|
|`tcp-push`|Push|

### 📝 Examples

tcpdump 'tcp[tcpflags] == tcp-syn'
# Only SYN set, others unset

tcpdump 'tcp[tcpflags] & tcp-syn != 0'
# SYN set (others may also be set)

tcpdump 'tcp[tcpflags] & (tcp-syn|tcp-ack) != 0'
# SYN or ACK set

```
tcpdump 'tcp[tcpflags] == tcp-syn'
# Only SYN set, others unset

tcpdump 'tcp[tcpflags] & tcp-syn != 0'
# SYN set (others may also be set)

tcpdump 'tcp[tcpflags] & (tcp-syn|tcp-ack) != 0'
# SYN or ACK set
```

---

## 🔎 More Display Options

|Command|Explanation|
|---|---|
|`tcpdump -q`|Quick & quiet: brief output|
|`tcpdump -e`|Include Ethernet (MAC) addresses|
|`tcpdump -A`|Print packets in ASCII|
|`tcpdump -xx`|Hexadecimal dump|
|`tcpdump -X`|Hex + ASCII dump|

---

## 📖 Reference

- `man tcpdump`
    
- `man pcap-filter`