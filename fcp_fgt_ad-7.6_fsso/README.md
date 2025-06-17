# FortiGate 7.6 – Section 05: Fortinet Single Sign-On (FSSO)

## Overview

Fortinet Single Sign-On (FSSO) allows FortiGate devices to associate user identity with IP addresses by monitoring authentication events from directory services like Microsoft Active Directory. This enables user-based policy enforcement without requiring users to reauthenticate at the firewall.

## FSSO Architecture

### Key Components

1. **FSSO Collector Agent**
   - Installed on a Windows server (typically a Domain Controller).
   - Collects user logon events from the AD event logs or using polling.
   - Sends login information to FortiGate using proprietary protocol.

2. **FSSO Polling Agent**
   - Lightweight option built into FortiGate.
   - Polls AD servers for user login sessions.
   - Less scalable than Collector Agent, suitable for small deployments.

3. **FortiGate**
   - Receives user-IP mappings from FSSO agent.
   - Applies identity-based policies based on user or group.

## Collector Agent Installation and Configuration

- Install on a Windows AD Domain Controller.
- Select method of logon event collection:
  - **DC Agent Mode**: Reads event logs via WMI or WinSec APIs.
  - **Logon Event Collector (LEC) Mode**: Uses Windows security logs.
- Configure groups to include/exclude.
- Set FortiGate(s) as trusted recipients of user-IP mappings.
- Secure communication with a shared password.

## FortiGate FSSO Configuration

- Add FSSO Agent under **Security Fabric > Fabric Connectors > Single Sign-On**.
- Define:
  - IP of Collector Agent
  - Password
  - Polling interval
  - Monitored group filters

## User Group Mapping

- Create user groups on FortiGate linked to FSSO groups from AD.
- Groups are used in identity-based policies.

## Authentication Flow

1. User logs into Windows domain.
2. FSSO agent detects login and extracts:
   - Username
   - User group
   - IP address
   - Logon timestamp
3. Agent sends this mapping to FortiGate.
4. FortiGate uses the mapping for identity-based policy enforcement.

## Monitoring and Diagnostics

### CLI Tools
- View FSSO status:
  ```bash
  diagnose debug enable
  diagnose debug authd fsso list
  ```
- Show learned users:
  ```bash
  get user fsso list
  ```

### GUI
- Go to **User & Authentication > Monitor > Firewall Users** to see active sessions.
- Check logs for FSSO login and logout events.

## Security Considerations

- Secure communications with collector agent using strong shared secrets.
- Minimize agent permissions on AD (read-only is sufficient).
- Limit FSSO to necessary user groups only.
- Configure idle timeouts and session aging to keep mappings accurate.

## Best Practices

- Deploy the collector agent on a reliable, always-on Domain Controller.
- Use secure transport and dedicated management network if possible.
- Validate group mappings regularly.
- Monitor FSSO logs and user mappings for accuracy.
- Test with various group membership scenarios before enforcing policies.

## Limitations and Notes

- FSSO relies on accurate user logon records; roaming or mobile users may present challenges.
- Not ideal for non-domain joined devices.
- Integrate with FortiAuthenticator for advanced identity options (e.g., guest access, MFA).

