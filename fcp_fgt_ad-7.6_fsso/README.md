# FortiGate 7.6 – Fortinet Single Sign-On (FSSO)

## Overview

- FSSO provides transparent user authentication for FortiGate policies.
- Automatically associates user identity with IP address.
- Useful in enterprise environments to apply user-based security policies without manual login.

## Components

- **FSSO Collector Agent**:
  - Installed on a Windows domain controller.
  - Collects logon events and forwards to FortiGate.
  - Uses Windows Event Log, polling, or WMI.

- **FortiGate FSSO Agent**:
  - Built-in FSSO client.
  - Communicates with the Collector Agent to receive user login info.

- **Polling Mode**:
  - FortiGate polls domain controllers directly for logon events.
  - No need for external Collector Agent.

## User Information Sources

- Windows Active Directory (AD)
- Novell eDirectory (via LDAP)
- Citrix or Terminal Server environments

## Configuration Steps

1. Install and configure Collector Agent on domain controller.
2. Define FSSO user groups in FortiGate.
3. Create policies using identity-based rules referencing FSSO groups.

## Advanced Settings

- **Group Filters**: Limit which groups are reported to FortiGate.
- **Workstation Checks**: Confirm that the IP belongs to the logged-in user.
- **Time-Out Settings**: Define how long user sessions remain valid.

## Troubleshooting Tools

- CLI: `diagnose debug authd fsso list`
- View active FSSO users in GUI
- Check connectivity between FortiGate and Collector Agent

## Best Practices

- Use Collector Agent for larger environments for better performance.
- Secure communication between Collector Agent and FortiGate (use encryption).
- Regularly monitor login events for accuracy and performance.
- Avoid overlapping user group definitions in policies.
