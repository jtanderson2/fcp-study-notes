# FortiGate 7.6 – Section 13: Security Fabric

## Overview

The Fortinet Security Fabric is an integrated cybersecurity platform that allows Fortinet products to communicate, share intelligence, and coordinate threat responses across the entire network infrastructure.

## Key Concepts

### 1. Fabric Connectors
- Predefined integrations with third-party platforms (e.g., AWS, Azure, SDN).
- Enable API-based communication and dynamic object updates.

### 2. Fabric Devices
- Fortinet devices that participate in the Security Fabric:
  - FortiGate
  - FortiAnalyzer
  - FortiManager
  - FortiAP, FortiSwitch, FortiClient
- Devices are authorized and connected to share telemetry and policies.

### 3. Root and Downstream Devices
- **Root FortiGate**: Central device managing the Security Fabric topology.
- **Downstream Devices**: Other FortiGates or Fortinet devices connected to the root.

## Configuration Steps

1. **Enable Security Fabric**:
   - System > Fabric Management
2. **Authorize Devices**:
   - Detect new devices and authorize them from the root.
3. **Configure Interfaces**:
   - Define which interfaces are part of the fabric.
4. **Set Role**:
   - Determine if FortiGate is root or downstream.

## Security Fabric Features

### Automation
- Create triggers and actions to respond to threats:
  - Quarantine host
  - Block IP
  - Send alert/email
- Integrated with threat intelligence and event handling.

### Fabric Telemetry
- Shares endpoint and network information across fabric devices.
- Improves threat visibility and correlation.

### Threat Intelligence Sharing
- Exchange IOC (Indicators of Compromise) between devices.
- Integrates with FortiGuard and third-party feeds.

### Dynamic Address Objects
- Shared object definitions between devices.
- Updated dynamically based on tags or IP changes.

## FortiAnalyzer and FortiManager Integration

- **FortiAnalyzer**:
  - Centralized log collection and reporting.
  - Fabric-aware analytics and incident response.
- **FortiManager**:
  - Central policy and configuration management.
  - Supports automation scripts and global objects.

## Zero Trust Network Access (ZTNA)

- Security Fabric supports ZTNA policy enforcement.
- Integrates with FortiClient and EMS for endpoint compliance.

## Monitoring and Visualization

- Fabric Topology view in GUI.
- Device statuses, firmware versions, and connectivity.
- Alerts for disconnected or unauthenticated devices.

## Best Practices

- Always use the latest firmware for full feature compatibility.
- Monitor Fabric status regularly via GUI or CLI.
- Use FortiAnalyzer for enhanced correlation and reporting.
- Enable automation rules for rapid threat mitigation.
- Secure communications between fabric devices using trusted certificates.

## CLI Commands

- View fabric topology:
  ```bash
  get system csf
  ```
- Authorize/unlink devices:
  ```bash
  execute csf device
  ```

## Troubleshooting

- Check for mismatched firmware versions.
- Validate communication between root and downstream devices.
- Inspect automation logs and fabric telemetry for errors.

