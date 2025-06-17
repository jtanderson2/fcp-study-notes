# FortiGate 7.6 – Section 13: Diagnostics

## Overview

FortiGate provides powerful diagnostic tools via CLI and GUI to troubleshoot network, system, and security issues. These tools are essential for administrators to maintain optimal operation and identify problems quickly.

## System Diagnostic Tools

### Basic CLI Commands
- View system status:
  ```bash
  get system status
  ```
- Show interface status and IPs:
  ```bash
  get system interface
  ```
- Ping test:
  ```bash
  execute ping <IP/FQDN>
  ```
- Traceroute test:
  ```bash
  execute traceroute <IP/FQDN>
  ```
- DNS resolution test:
  ```bash
  execute dns lookup <domain>
  ```

## Log Diagnostics

### View Logs
- GUI: Log & Report section
- CLI:
  ```bash
  execute log display
  ```

### Configure Log Filters
- Filter by time, severity, message ID, etc.:
  ```bash
  execute log filter field <field> <value>
  ```

## Packet Capture

- Captures packets on specified interface:
  ```bash
  diagnose sniffer packet <interface> '<filter>' <verbose> <count>
  ```
- Example:
  ```bash
  diagnose sniffer packet any 'host 192.168.1.10' 4 10
  ```
- Output Levels:
  - 1: brief headers
  - 2: headers with addresses and ports
  - 4: full packet details

## Debugging

### Enable Debugging
1. Enable debugging:
   ```bash
   diagnose debug enable
   ```
2. Set filters (optional):
   ```bash
   diagnose debug flow filter addr <IP>
   ```
3. Start flow debugging:
   ```bash
   diagnose debug flow show function-name enable
   diagnose debug flow trace start <count>
   ```

### Disable Debugging
```bash
diagnose debug disable
diagnose debug reset
```

## Network Tools

- Check ARP table:
  ```bash
  get system arp
  ```
- View routing table:
  ```bash
  get router info routing-table all
  ```
- IPsec tunnel status:
  ```bash
  diagnose vpn tunnel list
  ```

## CPU and Memory Monitoring

- CPU usage:
  ```bash
  get system performance top
  ```
- Memory usage:
  ```bash
  diagnose sys top
  ```

## Session Table

- View sessions:
  ```bash
  diagnose sys session list
  ```
- Filter by source or destination:
  ```bash
  diagnose sys session filter src <IP>
  diagnose sys session filter dst <IP>
  ```

## Best Practices

- Use filters to reduce debug output and focus on relevant data.
- Always disable debug after use to prevent performance impact.
- Save important log files before rebooting.
- Regularly monitor resource usage to preempt issues.

