# FortiGate 7.6 – Section 07: Antivirus

## Overview

FortiGate's Antivirus (AV) engine provides threat protection by detecting and blocking malware in real-time. It scans traffic for known viruses, trojans, worms, spyware, and other malicious software.

## Antivirus Operation Modes

### 1. Flow-based Inspection
- Scans packets as they flow through the firewall.
- Lower latency.
- May miss certain threats if the file is incomplete or fragmented.

### 2. Proxy-based Inspection
- Buffers full content before scanning.
- Higher accuracy, especially with compressed or fragmented content.
- Higher latency compared to flow-based.

## Supported Protocols for AV Scanning
- HTTP/HTTPS (with SSL inspection)
- SMTP, POP3, IMAP
- FTP
- SMB
- IM protocols

## Virus Definition Updates

- Delivered via FortiGuard Antivirus service.
- Updates include signatures, heuristics, and behavior patterns.
- AV engine can be configured to auto-update at regular intervals.
- Command to check versions:
  ```bash
  diagnose autoupdate versions
  ```

## Antivirus Profile Components

### File Filter
- Block files by type, extension, or size.

### Quarantine
- Suspect files can be quarantined for further analysis.
- Requires disk or FortiAnalyzer integration.

### Heuristics and Emulation
- Detect unknown threats using behavior-based analysis.
- Sandbox integration (FortiSandbox or FortiCloud) for advanced inspection.

### Inline Block
- Drops infected files before delivery to user.

### Logging and Alerts
- Detailed logs for all blocked threats and actions taken.
- Can forward logs to FortiAnalyzer or Syslog for central analysis.

## Integration with Other Security Features

- Works with:
  - Web Filter
  - Application Control
  - Data Leak Prevention (DLP)
  - SSL Inspection (to scan encrypted traffic)

## Configuring AV in Firewall Policies

- Apply AV profiles to security policies.
- Can enable different profiles per traffic direction (e.g., LAN to WAN).
- AV profile options controlled via:
  - GUI: Security Profiles > Antivirus
  - CLI: `config antivirus profile`

## Best Practices

- Enable AV on all internet-bound traffic.
- Use proxy-based inspection for higher accuracy where latency is acceptable.
- Regularly update AV definitions and monitor quarantine/logs.
- Combine AV with Web Filter and SSL Inspection for full protection.

## Troubleshooting

- Check logs for blocked or quarantined files.
- Use diagnostic tools:
  ```bash
  diagnose debug application scanunit -1
  diagnose debug enable
  ```
- Test detection using known malware test files (e.g., EICAR test file).
