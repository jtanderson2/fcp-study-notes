# FortiGate 7.6 – Section 15: Diagnostics and Troubleshooting

## Overview

FortiGate provides comprehensive diagnostic tools through both the CLI and GUI for resolving configuration issues, performance problems, and security event analysis. Proactive monitoring and regular diagnostics help ensure optimal firewall operation.

## System and Interface Diagnostics

### Basic Checks
- View firmware and system status:
  ```bash
  get system status
  ```
- List all configured interfaces and their states:
  ```bash
  get system interface physical
  get system interface
  ```

### Ping and Traceroute
- Test connectivity:
  ```bash
  execute ping <destination>
  execute traceroute <destination>
  ```

### DNS Resolution
- Test name resolution:
  ```bash
  execute dns lookup <hostname>
  ```

## Traffic Flow Debugging

### Enabling Debug Flow
```bash
diagnose debug reset
diagnose debug enable
diagnose debug flow show function-name enable
diagnose debug flow filter addr <IP>
diagnose debug flow trace start <count>
```
- Observe flow handling, route lookup, NAT policy application, and session creation.

### Disabling Debug
```bash
diagnose debug disable
```

## Packet Capture (Sniffer)

### Capture Commands
```bash
diagnose sniffer packet <interface> '<filter>' <verbosity> <count>
```
- Common filters: `host 192.168.1.1`, `port 443`
- Verbosity levels:
  - 1: summary
  - 2: headers
  - 4: full packet details

### Save for Offline Analysis
- Export via GUI or:
  ```bash
  execute packet-capture
  ```

## VPN Diagnostics

### SSL VPN
- View session info:
  ```bash
  diagnose vpn ssl monitor
  ```
- Debug:
  ```bash
  diagnose debug application sslvpn -1
  diagnose debug enable
  ```

### IPsec VPN
- Show tunnel summary:
  ```bash
  get vpn ipsec tunnel summary
  ```
- Debug IKE negotiation:
  ```bash
  diagnose debug application ike -1
  diagnose debug enable
  ```

## Routing and Session Table Analysis

### Routing Table
- View active routes:
  ```bash
  get router info routing-table all
  ```

### Session Table
- List active sessions:
  ```bash
  diagnose sys session list
  ```
- Apply filters:
  ```bash
  diagnose sys session filter src <IP>
  ```

## Performance Monitoring

- CPU and memory usage:
  ```bash
  get system performance status
  diagnose sys top
  ```
- Per-process CPU usage:
  ```bash
  diagnose sys process top
  ```

## Log Analysis

- View real-time logs:
  ```bash
  execute log display
  ```
- Filter logs:
  ```bash
  execute log filter field <field> <value>
  ```

## CLI Command Tips

- Use `?` for command help.
- Pipe output with `| grep <keyword>` to filter long outputs.
- Log all debug output to memory with `diagnose debug console timestamp enable`.

## Best Practices

- Always disable debug after use.
- Use filters to reduce output volume and focus on relevant data.
- Collect logs before rebooting or upgrading.
- Maintain out-of-band access via console port for recovery.
- Document and automate common diagnostic workflows.

