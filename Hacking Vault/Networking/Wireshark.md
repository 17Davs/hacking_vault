# 🌐 Wireshark Usage & Purpose

## 📋 Purpose

Wireshark is a **network protocol analyzer** used to capture and inspect network traffic in real-time or from saved files. It helps in:

- **Troubleshooting** network issues (e.g., latency, packet loss).
- **Security analysis** (e.g., detecting malicious traffic or intrusions).
- **Protocol debugging** (e.g., analyzing HTTP, DNS, or TCP behavior).
- **Learning** network protocols and traffic patterns.

## 🚀 Getting Started

### Installation

- Download from [wireshark.org](https://www.wireshark.org/).
- Install on Windows, macOS, or Linux.
- Requires `npcap` (Windows) or `libpcap` (Linux/macOS) for packet capture.

### Launch Wireshark

```bash
wireshark  # Start Wireshark GUI
```

Or, for terminal-based capture:

```bash
tshark  # Command-line version of Wireshark
```

## 🔎 Basic Usage

### 1. Select Network Interface

- Open Wireshark and choose an interface (e.g., `eth0`, `Wi-Fi`) to capture traffic.
- Use `ifconfig` (Linux) or `ipconfig` (Windows) to identify active interfaces.

### 2. Start Packet Capture

- Click the green shark fin icon or:

```bash
tshark -i eth0  # Capture on interface eth0
```

### 3. Apply Filters

Use **capture filters** (before capturing) or **display filters** (after capturing) to narrow down traffic.

#### Common Capture Filters

```bash
host 192.168.1.1         # Capture traffic to/from a specific IP
port 80                  # Capture traffic on port 80 (HTTP)
tcp                      # Capture only TCP traffic
not broadcast            # Exclude broadcast traffic
```

#### Common Display Filters

```bash
ip.addr == 192.168.1.1   # Show traffic to/from a specific IP
http                     # Show HTTP traffic
tcp.port == 443          # Show HTTPS traffic
dns                      # Show DNS queries
```

### 4. Save Captured Packets

- Save to a `.pcap` file for later analysis:

```bash
tshark -i eth0 -w capture.pcap  # Save capture to file
```

### 5. Analyze Saved Capture

- Open a `.pcap` file in Wireshark GUI or:

```bash
tshark -r capture.pcap  # Read and display packets from file
```

## 🔍 Common Analysis Tasks

### Inspect Packet Details

- Click a packet in Wireshark to view:
    - **Frame**: Metadata (timestamp, size).
    - **Protocol layers**: Ethernet, IP, TCP/UDP, application data.
    - **Hex/ASCII dump**: Raw packet content.

### Follow Streams

- Right-click a packet > `Follow > TCP Stream` to view the entire conversation (e.g., HTTP request/response).

### Export Data

- Export specific packets or objects (e.g., files from HTTP):
    - Go to `File > Export Objects > HTTP`.

## ✅ Quick Notes

- **Permissions**: On Linux, run Wireshark as root or configure non-root access for packet capture.
- **Filters**: Learn display filters for efficient analysis (see [wireshark.org/docs](https://www.wireshark.org/docs)).
- **Security**: Avoid capturing sensitive data (e.g., passwords) unless necessary; use encrypted protocols.
- **Performance**: Limit capture duration or use filters to avoid overwhelming large networks.