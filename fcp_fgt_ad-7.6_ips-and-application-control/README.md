# FortiGate 7.6 – Section 09: Intrusion Prevention and Application Control

## Overview

Intrusion Prevention System (IPS) and Application Control provide advanced threat detection and granular control over network traffic by inspecting packets for known attack signatures, anomalies, and application behaviors.

## Intrusion Prevention System (IPS)

### Function
- Detects and blocks exploits, known vulnerabilities, and suspicious patterns.
- Protects against:
  - Buffer overflows
  - Malware callbacks
  - Unauthorized access attempts
  - Exploits for OS and software vulnerabilities

### Signature Database
- Maintained by FortiGuard Labs.
- Updated frequently with new threat signatures.
- Categories: Critical, High, Medium, Low.

### IPS Operation
- Flow-based or proxy-based inspection.
- Can log, block, or allow matching traffic.
- Uses threat feeds and dynamic updates.

### IPS Sensor
- A profile that defines:
  - Which signatures to enable
  - Filters by severity, target, protocol
  - Exception handling

### Tuning
- Reduce false positives by refining filters.
- Use filters based on operating systems or network services.

### Logging
- Detailed logs include signature ID, source/destination, action taken.
- Forward logs to FortiAnalyzer for correlation and forensics.

## Application Control

### Function
- Identifies and controls application traffic by behavior and patterns.
- Recognizes thousands of applications including:
  - Social media
  - Messaging
  - Cloud services
  - VPNs and proxies

### Application Signature Database
- Updated regularly via FortiGuard.
- Applications categorized by risk and type.

### Application Sensor
- Defines which apps to allow, block, monitor, or shape.
- Uses filters by category, risk, and technology.

### Deep Packet Inspection
- Required to detect app-layer protocols.
- Works alongside SSL inspection for encrypted traffic.

### Logging and Visibility
- Logs show application name, category, action, and user.
- Useful for bandwidth management and security enforcement.

## Deployment and Configuration

### Creating Profiles
- GUI: Security Profiles > IPS / Application Control
- CLI:
  ```bash
  config ips sensor
  config application list
  ```

### Applying Profiles
- Attach to firewall policies.
- May differ per direction or user group.

### Performance Considerations
- Use flow-based inspection for high throughput.
- Balance security with system resources.

## Best Practices

- Regularly update IPS and application signatures.
- Customize sensors to match network environment.
- Enable logging for all blocked and monitored actions.
- Use app control to restrict risky or non-business apps.
- Tune IPS policies to reduce noise and improve relevance.

## Troubleshooting

- IPS:
  ```bash
  diagnose ips anomaly list
  diagnose debug application ipsmonitor -1

  # various ips toggle and stat options
diagnose test application ipsmonitor 

IPS Engine Test Usage:

    1: Display IPS engine information
    2: Toggle IPS engine enable/disable status
    3: Display restart log
    4: Clear restart log
    5: Toggle bypass status
    6: Submit attack characteristics now
   10: IPS queue length
   11: Clear IPS queue length
   12: IPS L7 socket statistics
   13: IPS session list
   14: IPS NTurbo statistics
   15: IPSA statistics
   18: Display session info cache
   19: Clear session info cache
   21: Reload FSA malicious URL database
   22: Reload allowlist URL database
   24: Display Flow AV statistics
   25: Reset Flow AV statistics
   32: Reload certificate blocklist database
   40: Display packet log statistics
   41: Reset packet log statistics
   42: Device notification statistics
   43: AV exempt statistics
   44: Dump IPS stack backtrace
   45: Virtual patch query statistics
   96: Toggle IPS engines watchdog timer
   97: Start all IPS engines
   98: Stop all IPS engines
   99: Restart all IPS engines and monitor
  ```

- Application Control:
  ```bash
  diagnose debug application app-ctrl -1
  diagnose debug enable
  ```

- Use FortiView and log reports to investigate blocked traffic and app usage.
